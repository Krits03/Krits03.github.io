import { Worker } from "node:worker_threads";
import { createWorkerQueue, parseWorkerTimeout } from "../worker-queue.js";
const workerCode = `
const { createRequire } = require('node:module')
const _require = createRequire(process.cwd() + '/')
const { parentPort } = require('node:worker_threads')
const { Resvg } = _require('@resvg/resvg-js')

parentPort.on('message', ({ id, svg, options }) => {
  try {
    const resvg = new Resvg(svg, options)
    const png = resvg.render().asPng()
    // Always slice to create a standard ArrayBuffer \u2014 native addon buffers
    // use external memory that can't be transferred via postMessage
    const ab = png.buffer.slice(png.byteOffset, png.byteOffset + png.byteLength)
    parentPort.postMessage({ _tag: 'response', id, payload: { _tag: 'success', png: ab } }, [ab])
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
  label: "resvg"
});
function renderPng(svg, options) {
  return workerQueue.enqueue(({ id }) => ({ id, svg, options })).then((result) => {
    if (result._tag === "failure")
      throw new Error(result.error);
    return Buffer.from(result.png);
  });
}
const signalKey = Symbol.for("og-image:resvg-worker-cleanup");
if (!globalThis[signalKey]) {
  globalThis[signalKey] = true;
  process.on("exit", workerQueue.shutdown);
}
class ResvgWorkerProxy {
  svg;
  options;
  pngPromise = null;
  constructor(svg, options) {
    this.svg = svg;
    this.options = options;
  }
  render() {
    if (!this.pngPromise)
      this.pngPromise = renderPng(this.svg, this.options);
    return {
      asPng: () => this.pngPromise
    };
  }
}
export default {
  initWasmPromise: Promise.resolve(),
  Resvg: ResvgWorkerProxy
};
