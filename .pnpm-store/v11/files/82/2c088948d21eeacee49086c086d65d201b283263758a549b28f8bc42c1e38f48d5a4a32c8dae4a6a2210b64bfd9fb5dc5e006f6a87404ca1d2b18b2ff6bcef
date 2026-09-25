import { getNitroOrigin as _getNitroOrigin } from "nuxt-site-config-kit/util";
import { getRequestHost, getRequestProtocol } from "#nuxtseo/h3";
export function getNitroOrigin(e) {
  return _getNitroOrigin({
    isDev: import.meta.dev,
    isPrerender: import.meta.prerender,
    requestHost: e ? getRequestHost(e, { xForwardedHost: true }) : void 0,
    requestProtocol: e ? getRequestProtocol(e, { xForwardedProto: true }) : void 0
  });
}
