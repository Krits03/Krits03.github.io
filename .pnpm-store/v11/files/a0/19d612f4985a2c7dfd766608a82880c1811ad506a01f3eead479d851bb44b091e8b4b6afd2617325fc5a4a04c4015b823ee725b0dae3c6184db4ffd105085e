import type { H3Event } from '#nuxtseo/h3';
interface Browser {
    connected: boolean;
    newPage: () => Promise<any>;
    close: () => Promise<void>;
    on: (event: string, handler: () => void) => void;
}
export declare function createBrowser(event?: H3Event): Promise<Browser>;
export {};
