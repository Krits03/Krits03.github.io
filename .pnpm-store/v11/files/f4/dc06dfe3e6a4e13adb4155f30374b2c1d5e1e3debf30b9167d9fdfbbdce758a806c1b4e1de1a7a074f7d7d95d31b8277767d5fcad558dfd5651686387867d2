import { getCloudflareEnv } from "../../../util/cloudflare.js";
import { withTimeout } from "../../../util/withTimeout.js";
import { useOgImageRuntimeConfig } from "../../../utils.js";
let puppeteer;
async function getPuppeteer() {
  if (!puppeteer) {
    puppeteer = (await import("@cloudflare/puppeteer")).default;
  }
  return puppeteer;
}
let browser = null;
let browserPromise = null;
export async function createBrowser(event) {
  if (browser?.connected)
    return browser;
  if (browserPromise)
    return browserPromise;
  const bindingName = useOgImageRuntimeConfig().browser?.binding;
  if (!bindingName) {
    throw new Error(
      "[Nuxt OG Image] Browser binding name not configured. Set `ogImage.browser.binding` in nuxt.config."
    );
  }
  const binding = getCloudflareEnv(event)?.[bindingName];
  if (!binding) {
    throw new Error(
      `[Nuxt OG Image] Cloudflare browser binding "${bindingName}" not found. Ensure it's configured in wrangler.toml and the request has cloudflare context.`
    );
  }
  const launchTimeout = useOgImageRuntimeConfig().security?.renderTimeout ?? 15e3;
  browserPromise = withTimeout((async () => {
    const pptr = await getPuppeteer();
    const sessions = await pptr.sessions(binding);
    const existingSession = sessions.find((s) => !s.connected);
    if (existingSession) {
      browser = await pptr.connect(binding, existingSession.id);
    } else {
      browser = await pptr.launch(binding);
    }
    browser.on("disconnected", () => {
      browser = null;
    });
    return browser;
  })(), launchTimeout, "cloudflare browser launch");
  browser = await browserPromise;
  browserPromise = null;
  return browser;
}
