const sharpInstance = { instance: void 0 };
const resvgInstance = { instance: void 0 };
const satoriInstance = { instance: void 0 };
let resvgImportPromise;
let satoriImportPromise;
export async function getResvg() {
  if (!resvgImportPromise) {
    resvgImportPromise = import("#og-image/bindings/resvg").then((m) => {
      resvgInstance.instance = m.default;
    });
  }
  await resvgImportPromise;
  await resvgInstance.instance.initWasmPromise;
  const Resvg = resvgInstance.instance.Resvg;
  if (!Resvg)
    throw new Error("[Nuxt OG Image] Resvg class is undefined after WASM initialization \u2014 the @resvg/resvg-wasm binding may have failed to load.");
  return Resvg;
}
export async function getSatori() {
  if (!satoriImportPromise) {
    satoriImportPromise = import("#og-image/bindings/satori").then((m) => {
      satoriInstance.instance = m.default;
    });
  }
  await satoriImportPromise;
  await satoriInstance.instance.initWasmPromise;
  const { satori } = satoriInstance.instance;
  if (!satori)
    throw new Error("[Nuxt OG Image] satori is undefined after WASM initialization \u2014 the satori binding may have failed to load.");
  return satori;
}
export async function getSharp() {
  sharpInstance.instance = sharpInstance.instance || await import("#og-image/bindings/sharp").then((m) => m.default);
  return sharpInstance.instance;
}
