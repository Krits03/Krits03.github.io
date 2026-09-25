const RE_SOCIAL_META_TAG = /<meta[^>]+(property|name)="(twitter|og):([^"]+)"[^>]*>/g;
const RE_SOCIAL_META_KEY = /(property|name)="(twitter|og):([^"]+)"/;
const RE_META_CONTENT = /content="([^"]+)"/;
const RE_OG_KEY_PARAM = /[,/]k_([^,./]+)/;
export function extractSocialPreviewTags(html) {
  const data = [];
  const rootData = {};
  const socialMetaTags = html.match(RE_SOCIAL_META_TAG) || [];
  let currentArrayIdx = -1;
  socialMetaTags.forEach((tag) => {
    const [, , type, key] = tag.match(RE_SOCIAL_META_KEY);
    const value = tag.match(RE_META_CONTENT)?.[1];
    if (!value) {
      return;
    }
    if (key === "title" || key === "description") {
      rootData[`${type}:${key}`] = value;
      return;
    }
    if (type === "og" && key === "image") {
      currentArrayIdx++;
    }
    if (!data[currentArrayIdx])
      data[currentArrayIdx] = {};
    if (!data[currentArrayIdx][type])
      data[currentArrayIdx][type] = {};
    data[currentArrayIdx][type][key] = value;
  });
  data.forEach((preview) => {
    if (preview.og?.image && preview.og?.image.includes("/_og/")) {
      const url = withoutQuery(preview.og.image);
      const keyMatch = url.match(RE_OG_KEY_PARAM);
      preview.key = keyMatch?.[1] || "og";
    }
  });
  return [rootData, data];
}
export function detectBase64MimeType(data) {
  const signatures = {
    "R0lGODdh": "image/gif",
    "R0lGODlh": "image/gif",
    "iVBORw0KGgo": "image/png",
    "/9j/": "image/jpeg",
    "UklGR": "image/webp",
    "AAABAA": "image/x-icon",
    "PHN2Zy": "image/svg+xml",
    // <svg
    "PD94bW": "image/svg+xml",
    // <?xml
    "PCEt": "image/svg+xml"
    // <!--
  };
  for (const s in signatures) {
    if (data.startsWith(s)) {
      return signatures[s];
    }
  }
  return "image/svg+xml";
}
export function toBase64Image(data) {
  const base64 = typeof data === "string" ? data : Buffer.from(data).toString("base64");
  const type = detectBase64MimeType(base64);
  return `data:${type};base64,${base64}`;
}
export function withoutQuery(path) {
  return path.split("?")[0];
}
