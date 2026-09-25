import { robotsDirectivesFromObject } from "@nuxtjs/robots/util";
import { setHeader } from "h3";
import {
  useRequestEvent,
  useRuntimeConfig
} from "nuxt/app";
import { computed, getCurrentInstance, onBeforeUnmount, ref, toValue } from "vue";
import { devRootDir } from "#build/nuxt.config.mjs";
import { injectHead, useHead } from "#imports";
export function useRobotsRule(rule) {
  const head = injectHead();
  const vm = getCurrentInstance();
  if (import.meta.client && head) {
    const robotsRef = ref(document.querySelector('meta[name="robots"]')?.getAttribute("content") || "");
    const _ = head.hooks?.hook("dom:rendered", () => {
      robotsRef.value = document.querySelector('meta[name="robots"]')?.getAttribute("content") || "";
    });
    onBeforeUnmount(_);
    return robotsRef;
  }
  const config = useRuntimeConfig();
  const event = useRequestEvent();
  function setRobotsRule(rule2) {
    const _rule = toValue(rule2);
    if (!event || typeof _rule === "undefined")
      return;
    let finalRule;
    if (typeof _rule === "boolean") {
      const robotsConfig2 = config["nuxt-robots"];
      finalRule = _rule ? robotsConfig2.robotsEnabledValue : robotsConfig2.robotsDisabledValue;
    } else if (typeof _rule === "object" && _rule !== null) {
      const robotsConfig2 = config["nuxt-robots"];
      finalRule = robotsDirectivesFromObject(_rule).join(", ") || robotsConfig2.robotsEnabledValue;
    } else {
      finalRule = _rule;
    }
    event.context.robots.rule = finalRule;
    const robotsConfig = config["nuxt-robots"];
    if (robotsConfig.header) {
      setHeader(event, "X-Robots-Tag", finalRule);
    }
    const vmFile = vm?.type?.__file;
    useHead({
      meta: [
        {
          "name": "robots",
          "content": finalRule,
          "data-hint": import.meta.dev ? ["useRobotsRule", `.${vmFile ? vm.type?.__file?.split(devRootDir || "")[1] || "" : ""}`].filter(Boolean).join(",") : void 0
        }
      ]
    }, {
      head
    });
  }
  setRobotsRule(rule);
  return computed({
    set(val) {
      setRobotsRule(val);
    },
    get() {
      return event?.context?.robots?.rule;
    }
  });
}
