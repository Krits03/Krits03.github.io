import { defineNuxtComponent as _defineNuxtComponent, defineComponent as _defineComponent } from "#imports";
import { useHydrationCheck } from "./composables.js";
export const defineNuxtComponent = function defineNuxtComponent2(...args) {
  const [options, key] = args;
  const { setup } = options;
  options.setup = function(props, ctx) {
    useHydrationCheck();
    return setup ? setup(props, ctx) : void 0;
  };
  return _defineNuxtComponent(options, key);
};
export const defineComponent = function defineComponent2(...args) {
  const [options] = args;
  if (typeof options === "object" && options !== null) {
    const { setup } = options;
    options.setup = function(props, ctx) {
      useHydrationCheck();
      return setup ? setup(props, ctx) : void 0;
    };
  }
  return _defineComponent(options);
};
