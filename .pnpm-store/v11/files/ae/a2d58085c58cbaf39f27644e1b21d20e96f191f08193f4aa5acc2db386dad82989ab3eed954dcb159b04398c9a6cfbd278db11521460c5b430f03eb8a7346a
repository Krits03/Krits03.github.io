import playwright from "playwright";
export async function createBrowser(_event) {
  return await playwright.chromium.launch({
    headless: true,
    timeout: 15e3
  });
}
