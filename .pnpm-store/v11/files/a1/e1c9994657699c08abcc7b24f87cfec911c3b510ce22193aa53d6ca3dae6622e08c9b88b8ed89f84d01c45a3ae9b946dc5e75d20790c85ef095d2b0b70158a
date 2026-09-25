import { createError, defineEventHandler, readBody, setResponseStatus } from "h3";
import { getRPC } from "../core/rpc.js";
export const hydrationMismatches = [];
export function getHydrationMismatches() {
  return { mismatches: hydrationMismatches };
}
export function clearHydrationMismatches(ids) {
  for (const id of ids) {
    const index = hydrationMismatches.findIndex((m) => m.id === id);
    if (index !== -1) {
      hydrationMismatches.splice(index, 1);
    }
  }
  getRPC()?.onHydrationCleared(ids);
}
export const getHandler = defineEventHandler(() => getHydrationMismatches());
export const postHandler = defineEventHandler(async (event) => {
  const body = await readBody(event);
  assertPayload(body);
  const payload = {
    id: crypto.randomUUID(),
    htmlPreHydration: body.htmlPreHydration,
    htmlPostHydration: body.htmlPostHydration,
    componentName: body.componentName,
    fileLocation: body.fileLocation
  };
  hydrationMismatches.push(payload);
  if (hydrationMismatches.length > 20) {
    const evicted = hydrationMismatches.shift();
    if (evicted) {
      getRPC()?.onHydrationCleared([evicted.id]);
    }
  }
  getRPC()?.onHydrationMismatch(payload);
  setResponseStatus(event, 201);
  return payload;
});
export const deleteHandler = defineEventHandler(async (event) => {
  const body = await readBody(event);
  if (!body || !Array.isArray(body.id)) {
    throw createError({ statusCode: 400, statusMessage: "Invalid payload" });
  }
  clearHydrationMismatches(body.id);
  setResponseStatus(event, 204);
});
function assertPayload(body) {
  if (!body || typeof body !== "object" || body.htmlPreHydration !== void 0 && typeof body.htmlPreHydration !== "string" || body.htmlPostHydration !== void 0 && typeof body.htmlPostHydration !== "string" || typeof body.componentName !== "string" || typeof body.fileLocation !== "string") {
    throw createError({ statusCode: 400, statusMessage: "Invalid payload" });
  }
}
