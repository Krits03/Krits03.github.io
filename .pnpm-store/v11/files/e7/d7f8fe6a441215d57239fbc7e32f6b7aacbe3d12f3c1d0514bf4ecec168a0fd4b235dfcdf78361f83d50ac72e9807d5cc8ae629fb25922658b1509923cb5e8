import type { ComponentLazyLoadData } from './schema.js';
export declare const lazyLoadData: ComponentLazyLoadData[];
export declare function getLazyLoadHints(): {
    id: string;
    route: string;
    state: {
        pageLoaded: boolean;
        hasReported: boolean;
        directImports: {
            componentName: string;
            importSource: string;
            importedBy: string;
            rendered: boolean;
        }[];
    };
}[];
export declare function clearLazyLoadHint(id: string): void;
export declare const getHandler: import("h3").EventHandler<import("h3").EventHandlerRequest, {
    id: string;
    route: string;
    state: {
        pageLoaded: boolean;
        hasReported: boolean;
        directImports: {
            componentName: string;
            importSource: string;
            importedBy: string;
            rendered: boolean;
        }[];
    };
}[]>;
export declare const postHandler: import("h3").EventHandler<import("h3").EventHandlerRequest, Promise<{
    error: string;
    message: string;
} | undefined>>;
export declare const deleteHandler: import("h3").EventHandler<import("h3").EventHandlerRequest, Promise<void>>;
