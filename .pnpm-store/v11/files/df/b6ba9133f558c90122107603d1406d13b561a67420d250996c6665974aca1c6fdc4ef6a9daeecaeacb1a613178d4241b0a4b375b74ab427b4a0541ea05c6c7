/**
 * Hash an arbitrary value into a short, stable string key.
 *
 * Values are serialized to a canonical representation (equal structures hash
 * equally regardless of key order), then digested with fnv1a-64. Matches the
 * approach Nuxt uses for `useAsyncData`/`useFetch` keys.
 *
 * Non-cryptographic — never use for signatures or integrity checks.
 */
export declare function hashKey(value: unknown): string;
