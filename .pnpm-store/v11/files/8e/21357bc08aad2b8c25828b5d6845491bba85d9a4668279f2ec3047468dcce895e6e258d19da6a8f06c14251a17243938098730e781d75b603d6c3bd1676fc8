import { createStorage } from "unstorage";
import lruCacheDriver from "unstorage/drivers/lru-cache";
export const htmlPayloadCache = createStorage({
  // short cache time so we don't need many entries at runtime
  driver: lruCacheDriver({ max: import.meta.prerender ? 1e4 : 50 })
});
export const prerenderOptionsCache = import.meta.prerender ? createStorage({
  driver: lruCacheDriver({ max: 1e4 })
}) : void 0;
export const emojiCache = createStorage({
  driver: lruCacheDriver({ max: 1e3 })
});
class BoundedMap {
  constructor(max) {
    this.max = max;
  }
  map = /* @__PURE__ */ new Map();
  get(key) {
    return this.map.get(key);
  }
  set(key, value) {
    if (this.map.size >= this.max)
      this.map.delete(this.map.keys().next().value);
    this.map.set(key, value);
  }
}
export const fontCache = new BoundedMap(100);
export const fontArrayCache = new BoundedMap(20);
