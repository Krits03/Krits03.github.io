import { fileURLToPath } from "node:url";
import { createIPX, createIPXNodeHandler, parseIPXURL, ipxFSStorage, ipxHttpStorage } from "ipx";
import { lazyEventHandler, fromNodeMiddleware } from "h3";
import { isAbsolute } from "pathe";
import { useRuntimeConfig } from "#imports";
export default lazyEventHandler(() => {
  const opts = useRuntimeConfig().ipx || {};
  const fsDir = opts?.fs?.dir ? (Array.isArray(opts.fs.dir) ? opts.fs.dir : [opts.fs.dir]).map((dir) => isAbsolute(dir) ? dir : fileURLToPath(new URL(dir, import.meta.url))) : void 0;
  const fsStorage = opts.fs?.dir ? ipxFSStorage({ ...opts.fs, dir: fsDir }) : void 0;
  const httpStorage = opts.http?.domains ? ipxHttpStorage({ ...opts.http }) : void 0;
  if (!fsStorage && !httpStorage) {
    throw new Error("IPX storage is not configured!");
  }
  const ipxOptions = {
    ...opts,
    storage: fsStorage || httpStorage,
    httpStorage
  };
  const baseURL = (opts.baseURL || "/_ipx").replace(/\/+$/, "");
  const ipx = createIPX(ipxOptions);
  const nodeHandler = createIPXNodeHandler(ipx, {
    parseURL(url) {
      const parsedURL = new URL(url);
      let pathname = parsedURL.pathname;
      if (baseURL && (pathname === baseURL || pathname.startsWith(`${baseURL}/`))) {
        pathname = pathname.slice(baseURL.length) || "/";
      }
      return parseIPXURL(parsedURL.origin + pathname + parsedURL.search);
    }
  });
  return fromNodeMiddleware(nodeHandler);
});
