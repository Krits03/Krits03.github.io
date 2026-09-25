import { createError, defineEventHandler, readBody, setResponseStatus } from "h3";
import { getRPC } from "../core/rpc.js";
export const htmlValidateReports = [];
export function storeHtmlValidateReport(report) {
  if (htmlValidateReports.some((existing) => existing.id === report.id)) {
    return false;
  }
  htmlValidateReports.push(report);
  getRPC()?.onHtmlValidateReport(report);
  return true;
}
export function getHtmlValidateReports() {
  return htmlValidateReports;
}
export function clearHtmlValidateReport(id) {
  const index = htmlValidateReports.findIndex((r) => r.id === id);
  if (index !== -1) {
    htmlValidateReports.splice(index, 1);
  }
  getRPC()?.onHtmlValidateDeleted(id);
}
export const getHandler = defineEventHandler(() => getHtmlValidateReports());
export const postHandler = defineEventHandler(async (event) => {
  const body = await readBody(event);
  if (!body || typeof body.id !== "string") {
    throw createError({ statusCode: 400, statusMessage: "Invalid payload" });
  }
  storeHtmlValidateReport(body);
  setResponseStatus(event, 201);
});
export const deleteHandler = defineEventHandler(async (event) => {
  const id = event.context.params?.id;
  if (typeof id !== "string") {
    throw createError({ statusCode: 404, statusMessage: "Not Found" });
  }
  clearHtmlValidateReport(id);
  setResponseStatus(event, 204);
});
