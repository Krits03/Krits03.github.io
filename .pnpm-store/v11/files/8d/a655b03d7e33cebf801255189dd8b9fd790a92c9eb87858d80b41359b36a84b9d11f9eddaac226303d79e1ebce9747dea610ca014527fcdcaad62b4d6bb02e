const RE_TOKEN = /[^\w-]/g;
function sanitizeName(name) {
  return name.replace(RE_TOKEN, "_");
}
export function createTimings() {
  const totals = /* @__PURE__ */ new Map();
  const spans = /* @__PURE__ */ new Map();
  const record = (name, ms) => {
    const key = sanitizeName(name);
    const existing = totals.get(key);
    if (existing) {
      existing.dur += ms;
      existing.count += 1;
    } else {
      totals.set(key, { dur: ms, count: 1 });
    }
  };
  const start = (name) => {
    const key = sanitizeName(name);
    const t0 = performance.now();
    const span = spans.get(key) ?? { open: 0, windowStart: 0, wall: 0 };
    if (span.open === 0)
      span.windowStart = t0;
    span.open += 1;
    spans.set(key, span);
    let ended = false;
    return () => {
      if (ended)
        return 0;
      ended = true;
      const t1 = performance.now();
      const ms = t1 - t0;
      span.open -= 1;
      if (span.open === 0) {
        span.wall += t1 - span.windowStart;
        const existing = totals.get(key);
        if (existing) {
          existing.dur = span.wall;
          existing.count += 1;
        } else {
          totals.set(key, { dur: span.wall, count: 1 });
        }
      } else {
        const existing = totals.get(key);
        if (existing)
          existing.count += 1;
        else
          totals.set(key, { dur: 0, count: 1 });
      }
      return ms;
    };
  };
  const measure = async (name, fn) => {
    const end = start(name);
    try {
      return await fn();
    } finally {
      end();
    }
  };
  const entries = () => Array.from(totals.entries()).map(([name, v]) => ({
    name,
    dur: Math.round(v.dur * 1e3) / 1e3,
    count: v.count > 1 ? v.count : void 0
  }));
  const header = () => entries().map(({ name, dur, count }) => {
    const desc = count ? `;desc="n=${count}"` : "";
    return `${name}${desc};dur=${dur}`;
  }).join(", ");
  return { start, record, measure, entries, header };
}
export const TIMING_CTX_KEY = "_ogImageTimings";
