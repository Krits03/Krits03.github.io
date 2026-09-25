import { tw4Breakpoints } from "#og-image-virtual/tw4-theme.mjs";
import { defineTransformer } from "../plugins.js";
const DEFAULT_BREAKPOINTS = {
  "sm": 640,
  "md": 768,
  "lg": 1024,
  "xl": 1280,
  "2xl": 1536
};
const BREAKPOINTS = { ...DEFAULT_BREAKPOINTS, ...tw4Breakpoints };
const RESPONSIVE_PREFIX_RE = /^(sm|md|lg|xl|2xl):(.+)$/;
const DARK_MODE_PREFIX_RE = /^dark:(.+)$/;
const GAP_CLASS_RE = /^gap(?:-(x|y))?-(\d+(?:\.\d+)?)$/;
const GAP_ARBITRARY_RE = /^gap(?:-(x|y))?-\[(.+)\]$/;
const TEXT_SIZE_RE = /^(?:xs|sm|base|lg|xl|\d+xl)$/;
const BORDER_WIDTH_RE = /^\d+$/;
const BORDER_SIDE_RE = /^[trblxy](?:-\d+)?$/;
const RING_WIDTH_RE = /^\d+$/;
const DIVIDE_SIDE_RE = /^[xy](?:-\d+)?$/;
const DIVIDE_NUMERIC_RE = /^\d+$/;
const OUTLINE_NUMERIC_RE = /^\d+$/;
const OUTLINE_STYLE_RE = /^(?:none|dashed|dotted|double)$/;
function resolveGapToStyle(cls, style) {
  const match = cls.match(GAP_CLASS_RE);
  if (match) {
    const axis = match[1];
    const value = Number(match[2]);
    if (axis === "x")
      style.columnGap = value;
    else if (axis === "y")
      style.rowGap = value;
    else style.gap = value;
    return true;
  }
  const arbMatch = cls.match(GAP_ARBITRARY_RE);
  if (arbMatch) {
    const axis = arbMatch[1];
    const value = arbMatch[2];
    if (axis === "x")
      style.columnGap = value;
    else if (axis === "y")
      style.rowGap = value;
    else style.gap = value;
    return true;
  }
  return false;
}
const DISPLAY_CLASSES = /* @__PURE__ */ new Set([
  "hidden",
  "block",
  "flex",
  "grid",
  "inline",
  "inline-flex",
  "inline-block",
  "inline-grid",
  "contents",
  "table",
  "flow-root",
  "list-item"
]);
const OVERLOADED_GROUPS = [
  ["text-", (v) => TEXT_SIZE_RE.test(v) ? "text-size" : "text-color"],
  ["border-", (v) => BORDER_WIDTH_RE.test(v) || BORDER_SIDE_RE.test(v) ? "border-width" : "border-color"],
  ["ring-", (v) => RING_WIDTH_RE.test(v) ? "ring-width" : "ring-color"],
  ["divide-", (v) => DIVIDE_SIDE_RE.test(v) || DIVIDE_NUMERIC_RE.test(v) || v === "reverse" ? "divide-width" : "divide-color"],
  ["outline-", (v) => OUTLINE_NUMERIC_RE.test(v) || OUTLINE_STYLE_RE.test(v) ? "outline-style" : "outline-color"]
];
function getUtilityGroup(cls) {
  if (DISPLAY_CLASSES.has(cls))
    return "display";
  if (cls.includes("["))
    return `${cls.slice(0, cls.indexOf("["))}-arbitrary`;
  for (const [prefix, resolver] of OVERLOADED_GROUPS) {
    if (cls === prefix.slice(0, -1) || cls.startsWith(prefix)) {
      return resolver(cls.slice(prefix.length));
    }
  }
  const dashIdx = cls.indexOf("-");
  return dashIdx === -1 ? cls : cls.slice(0, dashIdx);
}
function resolveDarkToken(baseClass, renderWidth) {
  const respMatch = baseClass.match(RESPONSIVE_PREFIX_RE);
  if (respMatch) {
    const bp = respMatch[1];
    const finalClass = respMatch[2];
    const breakpointWidth = BREAKPOINTS[bp];
    return breakpointWidth && renderWidth >= breakpointWidth ? finalClass : null;
  }
  return baseClass;
}
export default defineTransformer({
  filter: (node) => !!node.props?.class,
  transform: (node, ctx) => {
    const classes = node.props.class || "";
    const renderWidth = Number(ctx.options.width) || 1200;
    const isDarkMode = ctx.options.props?.colorMode === "dark";
    const tokens = classes.split(" ").filter((c) => c.trim());
    const darkOverrideGroups = /* @__PURE__ */ new Set();
    const responsiveOverrideGroups = /* @__PURE__ */ new Set();
    for (const token of tokens) {
      if (isDarkMode) {
        const darkMatch = token.match(DARK_MODE_PREFIX_RE);
        if (darkMatch) {
          const resolved = resolveDarkToken(darkMatch[1], renderWidth);
          if (resolved)
            darkOverrideGroups.add(getUtilityGroup(resolved));
          continue;
        }
      }
      const respMatch = token.match(RESPONSIVE_PREFIX_RE);
      if (respMatch) {
        const bp = respMatch[1];
        const baseClass = respMatch[2];
        const breakpointWidth = BREAKPOINTS[bp];
        if (breakpointWidth && renderWidth >= breakpointWidth)
          responsiveOverrideGroups.add(getUtilityGroup(baseClass));
      }
    }
    const processedClasses = [];
    const gapStyles = {};
    for (const token of tokens) {
      const darkMatch = token.match(DARK_MODE_PREFIX_RE);
      if (darkMatch) {
        if (isDarkMode) {
          const resolved = resolveDarkToken(darkMatch[1], renderWidth);
          if (resolved) {
            if (!resolveGapToStyle(resolved, gapStyles))
              processedClasses.push(resolved);
          }
        }
        continue;
      }
      const respMatch = token.match(RESPONSIVE_PREFIX_RE);
      if (respMatch) {
        const bp = respMatch[1];
        const baseClass = respMatch[2];
        const breakpointWidth = BREAKPOINTS[bp];
        if (breakpointWidth && renderWidth >= breakpointWidth) {
          if (isDarkMode && darkOverrideGroups.has(getUtilityGroup(baseClass)))
            continue;
          if (!resolveGapToStyle(baseClass, gapStyles))
            processedClasses.push(baseClass);
        }
      } else {
        const group = getUtilityGroup(token);
        if (isDarkMode && darkOverrideGroups.has(group) || responsiveOverrideGroups.has(group))
          continue;
        if (!resolveGapToStyle(token, gapStyles))
          processedClasses.push(token);
      }
    }
    if (Object.keys(gapStyles).length > 0) {
      node.props.style = { ...node.props.style, ...gapStyles };
    }
    node.props.class = processedClasses.join(" ");
  }
});
