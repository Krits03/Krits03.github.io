import init, { Renderer } from "@takumi-rs/wasm/no-bundler";
import { extractResourceUrls } from "./resource-urls.js";
const wasmBinary = import("@takumi-rs/wasm/takumi_wasm_bg.wasm?module").then((m) => m.default || m);
export default {
  initWasmPromise: wasmBinary.then((wasm) => init({ module_or_path: wasm })),
  Renderer,
  extractResourceUrls
};
