import { joinURL } from "ufo";
import { createOperationsGenerator } from "../utils/index.js";
import { defineProvider } from "../utils/provider.js";
import { hmac } from "@noble/hashes/hmac.js";
import { sha256 } from "@noble/hashes/sha2.js";
const booleanMap = (value) => {
  if (typeof value === "boolean") {
    return value ? 1 : 0;
  }
  switch (value) {
    case "t":
    case 1:
    case "true":
      return 1;
    default:
      return 0;
  }
};
const operationsGenerator = createOperationsGenerator({
  keyMap: {
    resize: "rs",
    size: "s",
    resizingType: "rt",
    width: "w",
    height: "h",
    minWidth: "mw",
    minHeight: "mh",
    zoom: "z",
    dpr: "dpr",
    enlarge: "el",
    extend: "ex",
    extendAspectRatio: "exar",
    gravity: "g",
    crop: "c",
    autoRotate: "ar",
    rotate: "rot",
    background: "bg",
    blur: "bl",
    sharpen: "sh",
    pixelate: "pix",
    stripMetadata: "sm",
    keepCopyright: "kcr",
    stripColorProfile: "scp",
    enforceThumbnail: "eth",
    quality: "q",
    maxBytes: "mb",
    format: "f",
    raw: "raw",
    cachebuster: "cb",
    expires: "exp",
    filename: "fn",
    returnAttachment: "att",
    preset: "pr",
    maxSrcResolution: "msr",
    maxSrcFileSize: "msfs",
    maxAnimationFrames: "maf",
    maxAnimationFrameResolution: "mafr",
    maxResultDimension: "mrd"
  },
  valueMap: {
    /**
     * Converting the image cropping configuration object into primitives for imgproxy.
     *
     * @param value
     */
    crop: (value) => {
      if (typeof value === "object" && value !== null) {
        return `${value.width}:${value.height}${value.gravity ? `:${value.gravity}` : ""}`;
      }
      return value;
    },
    enlarge: booleanMap,
    extend: booleanMap,
    autoRotate: booleanMap,
    stripMetadata: booleanMap,
    keepCopyright: booleanMap,
    stripColorProfile: booleanMap,
    enforceThumbnail: booleanMap,
    raw: booleanMap,
    returnAttachment: booleanMap,
    /**
     * imgproxy only supports rotation by multiples of 90 degrees, so numeric
     * values are normalised into the 0-359 range and floored to the nearest
     * multiple of 90.
     *
     * @see https://docs.imgproxy.net/usage/processing#rotate
     *
     * @param value
     */
    rotate: (value) => {
      if (typeof value !== "number" || !Number.isFinite(value)) {
        return value;
      }
      const normalized = (value % 360 + 360) % 360;
      return normalized - normalized % 90;
    }
  },
  formatter: (key, value) => `${key}:${value}`,
  joinWith: "/"
});
function hexToBytes(hex, label = "signing key/salt") {
  if (hex.length === 0 || hex.length % 2 !== 0 || !/^[0-9a-f]+$/i.test(hex)) {
    throw new Error(`Invalid hex string for ${label}: must be non-empty, even-length hex`);
  }
  const bytes = new Uint8Array(hex.length / 2);
  for (let i = 0; i < hex.length; i += 2) {
    bytes[i / 2] = Number.parseInt(hex.slice(i, i + 2), 16);
  }
  return bytes;
}
function urlSafeBase64(input) {
  const bytes = typeof input === "string" ? new TextEncoder().encode(input) : input;
  let binaryString = "";
  for (const byte of bytes) {
    binaryString += String.fromCharCode(byte);
  }
  const base64 = btoa(binaryString);
  return base64.replace(/=/g, "").replace(/\+/g, "-").replace(/\//g, "_");
}
function sign(salt, target, secret) {
  if (!secret || !salt) {
    return "unsafe";
  }
  const signature = hmac.create(sha256, hexToBytes(secret, "signing key"));
  signature.update(hexToBytes(salt, "signing salt"));
  signature.update(new TextEncoder().encode(target));
  return urlSafeBase64(signature.digest());
}
function resolveModifiers(modifiers) {
  if (modifiers?.fit) {
    const hasW = typeof modifiers?.width === "number" && modifiers.width > 0;
    const hasH = typeof modifiers?.height === "number" && modifiers.height > 0;
    const hasBoth = hasW && hasH;
    switch (modifiers.fit) {
      case "cover":
        modifiers.resizingType = hasBoth ? "fill" : "fit";
        break;
      case "contain":
        modifiers.resizingType = "fit";
        if (hasBoth) {
          modifiers.extend = true;
        }
        break;
      case "fill":
        modifiers.resizingType = hasBoth ? "force" : "fit";
        break;
      case "inside":
        modifiers.resizingType = "fit";
        break;
      case "outside":
        modifiers.resizingType = hasBoth ? "fill" : "fit";
        break;
    }
    delete modifiers.fit;
  }
  return modifiers;
}
export default defineProvider({
  getImage: (src, { modifiers, baseURL, key, salt }) => {
    const resolvedModifiers = resolveModifiers({ ...modifiers });
    const encodedUrl = urlSafeBase64(src);
    const path = joinURL("/", operationsGenerator(resolvedModifiers), encodedUrl);
    const signature = sign(salt, path, key);
    return {
      url: joinURL(baseURL, signature, path)
    };
  }
});
