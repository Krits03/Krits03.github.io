const naturalCompare = new Intl.Collator(void 0, { numeric: true }).compare;
function countPathSegments(loc) {
  let segments = 1;
  for (let i = 0; i < loc.length; i++) {
    if (loc.charCodeAt(i) === 47)
      segments++;
  }
  return segments;
}
export function sortInPlace(urls) {
  urls.sort((a, b) => {
    const aLoc = typeof a === "string" ? a : a.loc;
    const bLoc = typeof b === "string" ? b : b.loc;
    const aSegments = countPathSegments(aLoc);
    const bSegments = countPathSegments(bLoc);
    if (aSegments !== bSegments) {
      return aSegments - bSegments;
    }
    return naturalCompare(aLoc, bLoc);
  });
  return urls;
}
