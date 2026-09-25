import { Worker } from "node:worker_threads";
import { createWorkerQueue, parseWorkerTimeout } from "../worker-queue.js";
import { extractResourceUrls as extractTakumiResourceUrls } from "./resource-urls.js";
const workerCode = `
const { createRequire } = require('node:module')
const _require = createRequire(process.cwd() + '/')
const { parentPort } = require('node:worker_threads')
const { Renderer } = _require('@takumi-rs/core')

let renderer = new Renderer()

parentPort.on('message', async ({ id, type, newFonts, nodes, options }) => {
  try {
    const fontWarnings = []
    for (const font of (newFonts || [])) {
      try {
        const registerFont = renderer.registerFont || renderer.loadFont
        if (typeof registerFont !== 'function')
          throw new Error('renderer does not expose loadFont/registerFont')
        await registerFont.call(renderer, {
          name: font.name,
          data: font.data,
          weight: font.weight,
          style: font.style,
        })
      } catch (e) {
        fontWarnings.push({ name: font.name, weight: font.weight, error: e?.message || String(e) })
      }
    }
    const image = await renderer.render(nodes, options)
    // Always slice to create a standard ArrayBuffer \u2014 native addon buffers
    // use external memory that can't be transferred via postMessage
    const ab = image.buffer.slice(image.byteOffset, image.byteOffset + image.byteLength)
    parentPort.postMessage({ _tag: 'response', id, payload: { _tag: 'success', image: ab, fontWarnings } }, [ab])
  } catch (err) {
    parentPort.postMessage({ _tag: 'response', id, payload: { _tag: 'failure', error: err?.message || String(err) } })
  }
})
parentPort.postMessage({ _tag: 'ready' })
`;
const workerTimeout = parseWorkerTimeout(process.env.NUXT_OG_IMAGE_WORKER_TIMEOUT);
const workerQueue = createWorkerQueue({
  createWorker: () => new Worker(workerCode, { eval: true }),
  executionTimeout: workerTimeout,
  startupTimeout: workerTimeout,
  label: "takumi"
});
const signalKey = Symbol.for("og-image:takumi-worker-cleanup");
if (!globalThis[signalKey]) {
  globalThis[signalKey] = true;
  process.on("exit", workerQueue.shutdown);
}
function extractResourceUrls(nodes) {
  return Promise.resolve(extractTakumiResourceUrls(nodes));
}
class RendererWorkerProxy {
  allFonts = [];
  allFontKeys = /* @__PURE__ */ new Set();
  pendingFonts = [];
  syncedGeneration = -1;
  loadFont(font) {
    const key = `${font.name}|${font.weight || 400}|${font.style || "normal"}`;
    if (this.allFontKeys.has(key))
      return;
    this.allFontKeys.add(key);
    this.allFonts.push(font);
    this.pendingFonts.push(font);
  }
  registerFont(font) {
    this.loadFont(font);
  }
  render(nodes, options) {
    return workerQueue.enqueue(({ id, generation }) => {
      let fontsToSend;
      if (this.syncedGeneration !== generation) {
        fontsToSend = [...this.allFonts];
        this.pendingFonts = [];
      } else {
        fontsToSend = this.pendingFonts.splice(0);
      }
      this.syncedGeneration = generation;
      return { id, type: "render", newFonts: fontsToSend, nodes, options };
    }).then((result) => {
      if (result._tag === "failure")
        throw new Error(result.error);
      if (result.fontWarnings?.length) {
        for (const w of result.fontWarnings)
          console.warn(`[nuxt-og-image] Failed to load font "${w.name}" (weight: ${w.weight}) into takumi renderer: ${w.error}`);
      }
      return Buffer.from(result.image);
    });
  }
}
export default {
  initWasmPromise: Promise.resolve(),
  Renderer: RendererWorkerProxy,
  extractResourceUrls
};
