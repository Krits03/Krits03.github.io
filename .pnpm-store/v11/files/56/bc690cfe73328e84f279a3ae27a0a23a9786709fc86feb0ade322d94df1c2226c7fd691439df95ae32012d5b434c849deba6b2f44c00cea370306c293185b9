import { withBase } from 'ufo';
import { d as defineSchemaOrgResolver, a9 as IdentityId, a6 as setIfEmpty, a7 as idReference, e as resolveRelation, ab as resolvableDateToDate, a8 as resolvableDateToIso } from '../shared/schema-org.BygE6hLl.mjs';
import { offerResolver } from './index23.mjs';
import { p as personResolver, o as organizationResolver } from './index3.mjs';
import { placeResolver } from './index8.mjs';
import { virtualLocationResolver } from './index9.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import '../shared/schema-org.Ba1paCCL.mjs';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const PrimaryEventId = "#event";
const eventResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "Event"
  },
  inheritMeta: [
    "inLanguage",
    "description",
    "image",
    { meta: "title", key: "name" }
  ],
  idPrefix: ["url", PrimaryEventId],
  resolve(node, ctx) {
    if (node.location) {
      const isVirtual = node.location === "string" || node.location?.url !== "undefined";
      node.location = resolveRelation(node.location, ctx, isVirtual ? virtualLocationResolver : placeResolver);
    }
    node.performer = resolveRelation(node.performer, ctx, personResolver, {
      root: true
    });
    node.organizer = resolveRelation(node.organizer, ctx, organizationResolver, {
      root: true
    });
    node.offers = resolveRelation(node.offers, ctx, offerResolver);
    if (node.eventAttendanceMode)
      node.eventAttendanceMode = withBase(node.eventAttendanceMode, "https://schema.org/");
    if (node.eventStatus)
      node.eventStatus = withBase(node.eventStatus, "https://schema.org/");
    const isOnline = node.eventStatus === "https://schema.org/EventMovedOnline";
    const dates = ["startDate", "previousStartDate", "endDate"];
    dates.forEach((date) => {
      if (!isOnline) {
        if (node[date] instanceof Date && node[date].getHours() === 0 && node[date].getMinutes() === 0)
          node[date] = resolvableDateToDate(node[date]);
      } else {
        node[date] = resolvableDateToIso(node[date]);
      }
    });
    setIfEmpty(node, "endDate", node.startDate);
    return node;
  },
  resolveRootNode(node, { find }) {
    const identity = find(IdentityId);
    if (identity)
      setIfEmpty(node, "organizer", idReference(identity));
  }
});

export { PrimaryEventId, eventResolver, placeResolver, virtualLocationResolver };
