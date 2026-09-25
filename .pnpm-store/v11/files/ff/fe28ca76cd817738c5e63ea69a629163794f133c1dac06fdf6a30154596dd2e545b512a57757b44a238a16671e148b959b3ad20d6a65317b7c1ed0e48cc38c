const MIN_TIMEOUT_MS = 100;
export function getFetchTimeout(runtimeConfig) {
  const value = runtimeConfig.security?.imageFetchTimeout ?? 3e3;
  if (!Number.isFinite(value) || value < MIN_TIMEOUT_MS)
    return MIN_TIMEOUT_MS;
  return value;
}
