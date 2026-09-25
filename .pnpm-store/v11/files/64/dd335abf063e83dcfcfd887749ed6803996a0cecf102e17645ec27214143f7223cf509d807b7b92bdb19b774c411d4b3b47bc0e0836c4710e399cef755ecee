import { Launcher } from "chrome-launcher";
import playwrightCore from "playwright-core";
const chromePath = Launcher.getFirstInstallation();
export async function createBrowser(_event) {
  return playwrightCore.chromium.launch({
    headless: true,
    executablePath: chromePath,
    timeout: 15e3
  });
}
