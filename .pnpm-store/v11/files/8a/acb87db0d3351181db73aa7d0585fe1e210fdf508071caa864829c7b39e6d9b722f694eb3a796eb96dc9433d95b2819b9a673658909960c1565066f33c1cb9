interface NitroRouteRulesRuntimeConfig<TRouteRules extends object> {
    app?: {
        baseURL?: string;
    };
    nitro?: {
        routeRules?: Record<string, TRouteRules>;
    };
}
declare function withoutQuery(path: string): string;
declare function createNitroRouteRuleMatcher<TRouteRules extends object = Record<string, unknown>>(runtimeConfig: NitroRouteRulesRuntimeConfig<object>): (pathOrUrl: string) => TRouteRules;
declare function normalizeNitroMatchedRouteRules<TMatchedRouteRules extends Record<string, {
    options: unknown;
}> = Record<string, {
    options: unknown;
}>>(matchedRouteRules?: TMatchedRouteRules): {
    [Key in keyof TMatchedRouteRules]: TMatchedRouteRules[Key]['options'];
};

export { createNitroRouteRuleMatcher, normalizeNitroMatchedRouteRules, withoutQuery };
export type { NitroRouteRulesRuntimeConfig };
