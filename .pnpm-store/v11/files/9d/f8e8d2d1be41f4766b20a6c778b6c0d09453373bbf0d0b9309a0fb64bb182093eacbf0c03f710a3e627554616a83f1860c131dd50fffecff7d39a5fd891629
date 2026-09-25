import type { InferOutput } from 'valibot';
export declare const ComponentLazyLoadImportSchema: import("valibot").ObjectSchema<{
    readonly componentName: import("valibot").StringSchema<undefined>;
    readonly importSource: import("valibot").StringSchema<undefined>;
    readonly importedBy: import("valibot").StringSchema<undefined>;
    readonly rendered: import("valibot").BooleanSchema<undefined>;
}, undefined>;
export type DirectImportInfo = InferOutput<typeof ComponentLazyLoadImportSchema>;
export declare const ComponentLazyLoadDataSchema: import("valibot").ObjectSchema<{
    readonly id: import("valibot").StringSchema<undefined>;
    readonly route: import("valibot").StringSchema<undefined>;
    readonly state: import("valibot").ObjectSchema<{
        readonly pageLoaded: import("valibot").BooleanSchema<undefined>;
        readonly hasReported: import("valibot").BooleanSchema<undefined>;
        readonly directImports: import("valibot").ArraySchema<import("valibot").ObjectSchema<{
            readonly componentName: import("valibot").StringSchema<undefined>;
            readonly importSource: import("valibot").StringSchema<undefined>;
            readonly importedBy: import("valibot").StringSchema<undefined>;
            readonly rendered: import("valibot").BooleanSchema<undefined>;
        }, undefined>, undefined>;
    }, undefined>;
}, undefined>;
export type ComponentLazyLoadData = InferOutput<typeof ComponentLazyLoadDataSchema>;
export type ComponentLazyLoadState = {
    directImports: Map<string, DirectImportInfo>;
    hasReported: boolean;
    pageLoaded: boolean;
};
