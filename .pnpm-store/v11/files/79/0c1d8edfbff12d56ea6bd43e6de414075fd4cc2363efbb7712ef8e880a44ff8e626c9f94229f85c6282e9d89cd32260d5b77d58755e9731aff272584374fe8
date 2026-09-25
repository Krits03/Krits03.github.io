interface WorkerHandle {
    on: {
        (event: 'message', listener: (message: unknown) => void): WorkerHandle;
        (event: 'error', listener: (error: Error) => void): WorkerHandle;
        (event: 'exit', listener: (code: number) => void): WorkerHandle;
    };
    postMessage: (message: unknown) => void;
    removeAllListeners: () => WorkerHandle;
    terminate: () => Promise<number>;
    unref: () => void;
}
interface QueueOptions {
    createWorker: () => WorkerHandle;
    executionTimeout: number;
    startupTimeout: number;
    label: string;
    maxAttempts?: number;
}
interface Job<TMessage, TResponse> {
    id: number;
    buildMessage: (context: {
        id: number;
        generation: number;
    }) => TMessage;
    resolve: (response: TResponse) => void;
    reject: (error: Error) => void;
    attempts: number;
}
export declare function parseWorkerTimeout(value: string | undefined, fallback?: number): number;
export declare function createWorkerQueue<TMessage, TResponse>(options: QueueOptions): {
    enqueue: (buildMessage: Job<TMessage, TResponse>["buildMessage"]) => Promise<TResponse>;
    shutdown: () => void;
};
export {};
