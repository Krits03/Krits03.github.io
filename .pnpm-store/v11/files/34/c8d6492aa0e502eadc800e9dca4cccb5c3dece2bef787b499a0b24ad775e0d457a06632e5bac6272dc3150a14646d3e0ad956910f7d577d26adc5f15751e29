function wrapBroadcast(rpc) {
  return new Proxy(rpc, {
    get(target, prop, receiver) {
      const value = Reflect.get(target, prop, receiver);
      if (typeof value !== "function") return value;
      return (...args) => {
        try {
          const result = value.apply(target, args);
          if (result && typeof result.catch === "function") {
            ;
            result.catch((e) => {
              console.debug(e);
            });
          }
          return result;
        } catch (error) {
          console.debug(error);
        }
      };
    }
  });
}
export function getRPC() {
  const rpc = globalThis.__nuxtHintsRpcBroadcast;
  if (!rpc) return void 0;
  return wrapBroadcast(rpc);
}
