import { createConsola } from "consola";
import playwrightCore from "playwright-core";
import { exec } from "tinyexec";
let installedChromium = false;
let installChromiumPromise;
export async function createBrowser(_event) {
  if (installChromiumPromise)
    await installChromiumPromise;
  if (!installedChromium) {
    installChromiumPromise = (async () => {
      const logger = createConsola().withTag("Nuxt OG Image");
      logger.info("Installing Chromium install for og:image generation...");
      const result = exec("npx", ["playwright", "install", "chromium"]);
      const output = await result;
      if (output.stderr) {
        result.process?.stderr?.pipe(process.stderr);
      }
      if (output.stdout) {
        result.process?.stdout?.pipe(process.stdout);
      }
      if (output.exitCode !== 0) {
        logger.error("Failed to install Playwright dependency for og:image generation. Trying anyway...");
      }
      result.kill();
      logger.info("Installed Chromium install for og:image generation.");
      installedChromium = true;
    })();
  }
  return await playwrightCore.chromium.launch({
    headless: true,
    timeout: 15e3
  });
}
