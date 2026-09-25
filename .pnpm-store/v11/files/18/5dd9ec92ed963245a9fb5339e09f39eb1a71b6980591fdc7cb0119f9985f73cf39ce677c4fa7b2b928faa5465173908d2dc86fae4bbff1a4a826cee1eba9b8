import type { HydrationMismatchPayload, HydrationMismatchResponse } from '../hydration/types.js';
import type { ComponentLazyLoadData } from '../lazy-load/schema.js';
import type { HtmlValidateReport } from '../html-validate/types.js';
export interface HintsClientFunctions {
    onHydrationMismatch: (mismatch: HydrationMismatchPayload) => void;
    onHydrationCleared: (ids: string[]) => void;
    onLazyLoadReport: (data: ComponentLazyLoadData) => void;
    onLazyLoadCleared: (id: string) => void;
    onHtmlValidateReport: (report: HtmlValidateReport) => void;
    onHtmlValidateDeleted: (id: string) => void;
}
export interface HintsServerFunctions {
    getHydrationMismatches: () => HydrationMismatchResponse;
    clearHydrationMismatches: (ids: string[]) => void;
    getLazyLoadHints: () => ComponentLazyLoadData[];
    clearLazyLoadHint: (id: string) => void;
    getHtmlValidateReports: () => HtmlValidateReport[];
    clearHtmlValidateReport: (id: string) => void;
}
export declare const RPC_NAMESPACE = "nuxt-hints";
