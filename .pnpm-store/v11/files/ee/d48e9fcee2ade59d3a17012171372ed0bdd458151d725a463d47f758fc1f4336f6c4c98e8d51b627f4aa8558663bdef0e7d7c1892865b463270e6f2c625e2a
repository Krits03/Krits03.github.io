import { readFile } from "node:fs/promises";
import { resolveModulePath } from "exsolve";
export async function importWasm(input) {
  const _input = await input;
  const _module = _input.default || _input;
  if (typeof _module === "function") {
    const fnRes = await _module();
    const _instance = fnRes.instance || fnRes;
    return _instance.exports || _instance || _module;
  }
  return _module;
}
export async function readWasmFile(input) {
  const path = resolveModulePath(input);
  return readFile(path);
}
