export interface TimingEntry {
    name: string;
    dur: number;
    count?: number;
}
export interface Timings {
    start: (name: string) => () => number;
    record: (name: string, ms: number) => void;
    measure: <T>(name: string, fn: () => Promise<T> | T) => Promise<T>;
    entries: () => TimingEntry[];
    header: () => string;
}
export declare function createTimings(): Timings;
export declare const TIMING_CTX_KEY = "_ogImageTimings";
