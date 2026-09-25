const RE_UNICODE_RANGE_PART = /^U\+([0-9A-Fa-f]+)(?:-([0-9A-Fa-f]+))?$/;
export function parseUnicodeRange(range) {
  const parts = range.split(",").map((s) => s.trim()).filter(Boolean);
  const result = [];
  for (const part of parts) {
    const match = part.match(RE_UNICODE_RANGE_PART);
    if (!match)
      return null;
    const start = Number.parseInt(match[1], 16);
    const end = match[2] ? Number.parseInt(match[2], 16) : start;
    result.push([start, end]);
  }
  return result.length > 0 ? result : null;
}
export function codepointsIntersectRanges(codepoints, ranges) {
  for (const cp of codepoints) {
    for (const [start, end] of ranges) {
      if (cp >= start && cp <= end)
        return true;
    }
  }
  return false;
}
function addCodepointsFromString(str, codepoints) {
  for (const ch of str)
    codepoints.add(ch.codePointAt(0));
}
export function extractCodepoints(node) {
  const codepoints = /* @__PURE__ */ new Set();
  const walk = (n) => {
    if (typeof n.text === "string")
      addCodepointsFromString(n.text, codepoints);
    const children = n.props?.children ?? n.children;
    if (typeof children === "string") {
      addCodepointsFromString(children, codepoints);
    } else if (Array.isArray(children)) {
      for (const child of children) {
        if (child == null)
          continue;
        if (typeof child === "string")
          addCodepointsFromString(child, codepoints);
        else
          walk(child);
      }
    }
  };
  walk(node);
  return codepoints;
}
