import { features } from "#shared/hints-config";
export function isFeatureDevtoolsEnabled(feature) {
  return features[feature] != null && typeof features[feature] === "object" ? features[feature].devtools !== false : !!features[feature];
}
export function isFeatureLogsEnabled(feature) {
  return features[feature] != null && typeof features[feature] === "object" ? features[feature].logs !== false : !!features[feature];
}
export function isFeatureEnabled(feature) {
  return !!features[feature];
}
export function getFeatureOptions(feature) {
  const val = features[feature];
  if (typeof val === "object" && val.options) {
    return val.options;
  }
  return void 0;
}
