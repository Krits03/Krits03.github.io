const satoriRendererInstance = { instance: void 0 };
const browserRendererInstance = { instance: void 0 };
const takumiRendererInstance = { instance: void 0 };
export async function getSatoriRenderer() {
  satoriRendererInstance.instance = satoriRendererInstance.instance || await import("#og-image/renderers/satori").then((m) => m.default);
  return satoriRendererInstance.instance;
}
export async function getBrowserRenderer() {
  browserRendererInstance.instance = browserRendererInstance.instance || await import("#og-image/renderers/browser").then((m) => m.default);
  return browserRendererInstance.instance;
}
export async function getTakumiRenderer() {
  takumiRendererInstance.instance = takumiRendererInstance.instance || await import("#og-image/renderers/takumi").then((m) => m.default);
  return takumiRendererInstance.instance;
}
