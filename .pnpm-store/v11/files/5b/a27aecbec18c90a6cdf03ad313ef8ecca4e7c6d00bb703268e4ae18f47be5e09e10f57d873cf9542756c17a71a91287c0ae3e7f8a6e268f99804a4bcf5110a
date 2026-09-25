import { existsSync, mkdirSync, readFileSync, writeFileSync } from "node:fs";
import { join } from "pathe";
import { componentNames } from "#og-image-virtual/component-names.mjs";
import { hashOgImageOptions } from "../../../shared/urlEncoding.js";
import { useOgImageRuntimeConfig } from "../../utils.js";
export function getComponentHash(componentName) {
  const components = componentNames;
  const component = components.find(
    (c) => c.pascalName === componentName || c.kebabName === componentName
  );
  return component?.hash || "";
}
export function generateBuildCacheKey(options, extension) {
  const { version } = useOgImageRuntimeConfig();
  const componentHash = getComponentHash(options.component || "default");
  const hash = hashOgImageOptions(options, componentHash, version);
  return `${hash}.${extension}`;
}
export function getBuildCachedImage(options, extension) {
  const { buildCacheDir } = useOgImageRuntimeConfig();
  if (!buildCacheDir)
    return null;
  const cacheKey = generateBuildCacheKey(options, extension);
  const cachePath = join(buildCacheDir, cacheKey);
  if (!existsSync(cachePath))
    return null;
  const cached = JSON.parse(readFileSync(cachePath, "utf-8"));
  if (cached.expiresAt && cached.expiresAt < Date.now()) {
    return null;
  }
  return Buffer.from(cached.data, "base64");
}
export function setBuildCachedImage(options, extension, data, maxAgeSeconds) {
  const { buildCacheDir } = useOgImageRuntimeConfig();
  if (!buildCacheDir)
    return;
  const cacheKey = generateBuildCacheKey(options, extension);
  const cachePath = join(buildCacheDir, cacheKey);
  if (!existsSync(buildCacheDir)) {
    mkdirSync(buildCacheDir, { recursive: true });
  }
  const cached = {
    data: Buffer.from(data).toString("base64"),
    expiresAt: Date.now() + maxAgeSeconds * 1e3,
    createdAt: Date.now()
  };
  writeFileSync(cachePath, JSON.stringify(cached));
}
