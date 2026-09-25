import { defineOgImageRaw } from "./_defineOgImageRaw.js";
export function defineOgImage(component, propsOrOptions = {}, options = {}) {
  if (Array.isArray(propsOrOptions)) {
    return defineOgImageRaw(propsOrOptions.map((opt) => ({
      ...opt,
      component
    })));
  }
  const sharedProps = propsOrOptions && Object.keys(propsOrOptions).length > 0 ? propsOrOptions : void 0;
  if (Array.isArray(options)) {
    return defineOgImageRaw(options.map((opt) => {
      const input2 = {
        ...opt,
        component
      };
      if (sharedProps) {
        input2.props = opt.props ? { ...sharedProps, ...opt.props } : { ...sharedProps };
      }
      return input2;
    }));
  }
  const input = {
    ...options,
    component
  };
  if (sharedProps)
    input.props = sharedProps;
  return defineOgImageRaw(input);
}
