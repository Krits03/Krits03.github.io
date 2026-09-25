import { fnv1a64Base36 } from "fnv1a-64";
import { identify } from "object-identity";
export function hashKey(value) {
  return fnv1a64Base36(identify(value));
}
