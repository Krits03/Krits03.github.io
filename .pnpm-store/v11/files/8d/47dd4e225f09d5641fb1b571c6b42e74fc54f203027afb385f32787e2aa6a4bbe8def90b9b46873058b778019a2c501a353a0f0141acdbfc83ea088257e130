import { ConsolaInstance } from 'consola';

interface SerializedRegExp {
    regex: string;
}
interface SourceFlagsRegExp {
    source: string;
    flags?: string;
}
type FilterEntry = string | RegExp;
type SerializedFilterEntry = string | SerializedRegExp | SourceFlagsRegExp;
type FilterEntryInput = FilterEntry | SerializedRegExp | SourceFlagsRegExp;
declare function serializeFilters(filters: unknown[], tag?: string): SerializedFilterEntry[];
declare function deserializeFilters(filters: FilterEntryInput[]): FilterEntry[];
interface CreateFilterOptions {
    include?: FilterEntryInput[];
    exclude?: FilterEntryInput[];
}
declare function createFilter(options?: CreateFilterOptions): (path: string) => boolean;
declare function withoutQuery(path: string): string;
declare function createModuleLogger(tag: string, debug?: boolean): ConsolaInstance;

export { createFilter, createModuleLogger, deserializeFilters, serializeFilters, withoutQuery };
export type { CreateFilterOptions, FilterEntry, FilterEntryInput, SerializedFilterEntry, SerializedRegExp, SourceFlagsRegExp };
