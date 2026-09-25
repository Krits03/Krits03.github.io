import { createDefu } from 'defu';
import { withoutLeadingSlash } from 'ufo';

const NonHelpfulBots = [
  "Nuclei",
  "WikiDo",
  "Riddler",
  "PetalBot",
  "Zoominfobot",
  "Go-http-client",
  "Node/simplecrawler",
  "CazoodleBot",
  "dotbot/1.0",
  "Gigabot",
  "Barkrowler",
  "BLEXBot",
  "magpie-crawler"
];
const AiBots = [
  // OpenAI
  "GPTBot",
  "OAI-SearchBot",
  "ChatGPT-User",
  // Anthropic
  "ClaudeBot",
  "Claude-SearchBot",
  "Claude-User",
  "Claude-Web",
  "anthropic-ai",
  // Google
  "Google-Extended",
  "Google-CloudVertexBot",
  "Google-GeminiNotebook",
  "Google-NotebookLM",
  "Google-Agent",
  // Meta
  "meta-externalagent",
  "meta-externalfetcher",
  "FacebookBot",
  // Amazon
  "Amazonbot",
  "Amzn-SearchBot",
  "Amzn-User",
  "bedrockbot",
  // Apple
  "Applebot-Extended",
  // Perplexity
  "PerplexityBot",
  "Perplexity-User",
  // ByteDance
  "Bytespider",
  // Webz.io
  "omgili",
  "omgilibot",
  "Webzio-Extended",
  // Yandex
  "YandexAdditional",
  "YandexAdditionalBot",
  // Others
  "CCBot",
  "cohere-ai",
  "Diffbot",
  "ImagesiftBot",
  "MistralAI-User",
  "MistralAI-Index",
  "AI2Bot",
  "DuckAssistBot",
  "FirecrawlAgent",
  "ICC-Crawler",
  "SemrushBot-OCOB"
];

function mapBotKindToCategory(botKind) {
  switch (botKind) {
    // Browser automation tools
    case "selenium":
    case "webdriver":
    case "webdriverio":
    case "phantomjs":
    case "phantomas":
    case "nightmarejs":
    case "slimerjs":
      return "automation";
    // Headless browsers
    case "headless_chrome":
    case "electron":
    case "cef":
    case "cefsharp":
      return "automation";
    // Data collection/scraping tools
    case "fminer":
    case "sequentum":
    case "geb":
      return "scraping";
    // Security/testing tools
    case "awesomium":
    case "coachjs":
      return "security-scanner";
    // Script engines
    case "rhino":
      return "automation";
    // Unknown/generic
    case "unknown":
    default:
      return "generic";
  }
}
const KNOWN_SEARCH_BOTS = [
  {
    pattern: "googlebot",
    name: "googlebot",
    secondaryPatterns: ["google.com/bot.html"]
  },
  {
    pattern: "bingbot",
    name: "bingbot",
    secondaryPatterns: ["msnbot"]
  },
  {
    pattern: "yandexbot",
    name: "yandexbot"
  },
  {
    pattern: "baiduspider",
    name: "baiduspider",
    secondaryPatterns: ["baidu.com"]
  },
  {
    pattern: "duckduckbot",
    name: "duckduckbot",
    secondaryPatterns: ["duckduckgo.com"]
  },
  {
    pattern: "slurp",
    name: "yahoo"
  },
  {
    pattern: "applebot",
    name: "applebot",
    secondaryPatterns: ["apple.com/go/applebot"]
  }
];
const SOCIAL_BOTS = [
  {
    pattern: "twitterbot",
    name: "twitter",
    secondaryPatterns: ["twitter"]
  },
  {
    pattern: "facebookexternalhit",
    name: "facebook",
    secondaryPatterns: ["facebook.com"]
  },
  {
    pattern: "linkedinbot",
    name: "linkedin",
    secondaryPatterns: ["linkedin"]
  },
  {
    pattern: "pinterestbot",
    name: "pinterest",
    secondaryPatterns: ["pinterest"]
  },
  {
    pattern: "discordbot",
    name: "discord",
    secondaryPatterns: ["discordapp"]
  }
];
const SEO_BOTS = [
  {
    pattern: "mj12bot",
    name: "majestic12",
    secondaryPatterns: ["majestic12.co.uk/bot"]
  },
  {
    pattern: "ahrefsbot",
    name: "ahrefs",
    secondaryPatterns: ["ahrefs.com"]
  },
  {
    pattern: "semrushbot",
    name: "semrush",
    secondaryPatterns: ["semrush.com/bot"]
  },
  {
    pattern: "screaming frog",
    name: "screaming-frog",
    secondaryPatterns: ["screamingfrog.co.uk"]
  },
  {
    pattern: "rogerbot",
    name: "moz"
  }
];
const AI_BOTS = [
  {
    pattern: "anthropic",
    name: "anthropic"
  },
  {
    pattern: "claude",
    name: "claude"
  },
  {
    pattern: "gptbot",
    name: "gpt",
    secondaryPatterns: ["openai.com"]
  },
  {
    pattern: "google-extended",
    name: "google-extended"
  },
  {
    pattern: "applebot-extended",
    name: "applebot-extended"
  },
  {
    pattern: "bytespider",
    name: "bytespider"
  },
  {
    pattern: "diffbot",
    name: "diffbot"
  },
  {
    pattern: "googlebot-news",
    name: "google-news"
  },
  {
    pattern: "cohere",
    name: "cohere",
    secondaryPatterns: ["cohere.com"]
  },
  {
    pattern: "ccbot",
    name: "commoncrawl",
    secondaryPatterns: ["commoncrawl.org"]
  },
  {
    pattern: "perplexitybot",
    name: "perplexity",
    secondaryPatterns: ["perplexity.ai"]
  }
];
const HTTP_TOOL_BOTS = [
  {
    pattern: "python-requests",
    name: "requests",
    secondaryPatterns: ["python"]
  },
  {
    pattern: "wget",
    name: "wget"
  },
  {
    pattern: "curl",
    name: "curl",
    secondaryPatterns: ["curl"]
  }
];
const SECURITY_SCANNING_BOTS = [
  {
    pattern: "zgrab",
    name: "zgrab"
  },
  {
    pattern: "masscan",
    name: "masscan"
  },
  {
    pattern: "nmap",
    name: "nmap",
    secondaryPatterns: ["insecure.org"]
  },
  {
    pattern: "nikto",
    name: "nikto"
  },
  {
    pattern: "wpscan",
    name: "wpscan"
  }
];
const SCRAPING_BOTS = [
  {
    pattern: "scrapy",
    name: "scrapy",
    secondaryPatterns: ["scrapy.org"]
  }
];
const AUTOMATION_BOTS = [
  {
    pattern: "phantomjs",
    name: "phantomjs"
  },
  {
    pattern: "headless",
    name: "headless-browser"
  },
  {
    pattern: "playwright",
    name: "playwright"
  },
  {
    pattern: "selenium",
    name: "selenium",
    secondaryPatterns: ["webdriver"]
  },
  {
    pattern: "puppeteer",
    name: "puppeteer",
    secondaryPatterns: ["headless"]
  }
];
const GENERIC_BOTS = [
  {
    pattern: "bot",
    name: "generic-bot"
  },
  {
    pattern: "spider",
    name: "generic-spider"
  },
  {
    pattern: "crawler",
    name: "generic-crawler"
  },
  {
    pattern: "scraper",
    name: "generic-scraper"
  }
];
const BOT_MAP = [
  {
    type: "search-engine",
    bots: KNOWN_SEARCH_BOTS,
    trusted: true
  },
  {
    type: "social",
    bots: SOCIAL_BOTS,
    trusted: true
  },
  {
    type: "seo",
    bots: SEO_BOTS,
    trusted: true
  },
  {
    type: "ai",
    bots: AI_BOTS,
    trusted: true
  },
  {
    type: "generic",
    bots: GENERIC_BOTS,
    trusted: false
  },
  {
    type: "automation",
    bots: AUTOMATION_BOTS,
    trusted: false
  },
  {
    type: "http-tool",
    bots: HTTP_TOOL_BOTS,
    trusted: false
  },
  {
    type: "security-scanner",
    bots: SECURITY_SCANNING_BOTS,
    trusted: false
  },
  {
    type: "scraping",
    bots: SCRAPING_BOTS,
    trusted: false
  }
];

const defaultBotPattern = /(?=(googlebot)|(google\.com\/bot\.html)|(bingbot)|(msnbot)|(yandexbot)|(baiduspider)|(baidu\.com)|(duckduckbot)|(duckduckgo\.com)|(slurp)|(applebot)|(twitterbot)|(twitter)|(facebookexternalhit)|(facebook\.com)|(linkedinbot)|(linkedin)|(pinterestbot)|(pinterest)|(discordbot)|(discordapp)|(mj12bot)|(majestic12\.co\.uk\/bot)|(ahrefsbot)|(ahrefs\.com)|(semrushbot)|(semrush\.com\/bot)|(screaming frog)|(screamingfrog\.co\.uk)|(rogerbot)|(anthropic)|(claude)|(gptbot)|(openai\.com)|(google-extended)|(bytespider)|(diffbot)|(cohere)|(ccbot)|(commoncrawl\.org)|(perplexitybot)|(perplexity\.ai)|(bot)|(spider)|(crawler)|(scraper)|(phantomjs)|(headless)|(playwright)|(selenium)|(webdriver)|(puppeteer)|(python-requests)|(python)|(wget)|(curl)|(zgrab)|(masscan)|(nmap)|(insecure\.org)|(nikto)|(wpscan)|(scrapy))/g;
const botTargets = [0, 0, 1, 1, 2, 3, 3, 4, 4, 5, 6, 256, 256, 257, 257, 258, 258, 259, 259, 260, 260, 512, 512, 513, 513, 514, 514, 515, 515, 516, 768, 769, 770, 770, 771, 773, 774, 776, 777, 777, 778, 778, 1024, 1025, 1026, 1027, 1280, 1284, 1282, 1283, 1283, 1284, 1536, 1536, 1537, 1538, 1792, 1793, 1794, 1794, 1795, 1796, 2048];
function matchDefaultBotTarget(value) {
  let bestPriority = -1;
  defaultBotPattern.lastIndex = 0;
  let match = defaultBotPattern.exec(value);
  while (match) {
    let priority = 0;
    while (typeof match[priority + 1] === "undefined")
      priority++;
    if (bestPriority === -1 || priority < bestPriority)
      bestPriority = priority;
    if (bestPriority === 0)
      break;
    defaultBotPattern.lastIndex = match.index + 1;
    match = defaultBotPattern.exec(value);
  }
  return bestPriority === -1 ? void 0 : botTargets[bestPriority];
}

const ROBOT_DIRECTIVE_VALUES = {
  // Standard directives
  enabled: "index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1",
  disabled: "noindex, nofollow",
  index: "index",
  noindex: "noindex",
  follow: "follow",
  nofollow: "nofollow",
  none: "none",
  all: "all",
  // Non-standard directives (not part of official robots spec)
  noai: "noai",
  noimageai: "noimageai"
};
function formatMaxImagePreview(value) {
  return `max-image-preview:${value}`;
}
function formatMaxSnippet(value) {
  return `max-snippet:${value}`;
}
function formatMaxVideoPreview(value) {
  return `max-video-preview:${value}`;
}
function parseRobotsTxt(s) {
  const groups = [];
  const sitemaps = [];
  const errors = [];
  const warnings = [];
  let createNewGroup = false;
  let currentGroup = {
    comment: [],
    // comments are too hard to parse in a logical order, we'll just omit them
    disallow: [],
    allow: [],
    userAgent: [],
    contentUsage: [],
    contentSignal: []
  };
  let ln = -1;
  for (const _line of s.split("\n")) {
    ln++;
    const [preComment] = _line.split("#").map((s2) => s2.trim());
    const line = String(preComment);
    const sepIndex = line.indexOf(":");
    if (sepIndex === -1)
      continue;
    const rule = line.substring(0, sepIndex).trim().toLowerCase();
    const val = line.substring(sepIndex + 1).trim();
    switch (rule) {
      case "user-agent":
      case "useragent":
      case "user agent":
        if (createNewGroup) {
          groups.push({
            ...currentGroup
          });
          currentGroup = {
            comment: [],
            disallow: [],
            allow: [],
            userAgent: [],
            contentUsage: [],
            contentSignal: []
          };
          createNewGroup = false;
        }
        currentGroup.userAgent.push(val);
        break;
      case "allow":
        currentGroup.allow.push(val);
        createNewGroup = true;
        break;
      case "disallow":
      case "dissallow":
      case "dissalow":
      case "disalow":
      case "diasllow":
      case "disallaw":
        currentGroup.disallow.push(val);
        createNewGroup = true;
        break;
      case "sitemap":
      case "site-map":
        sitemaps.push(val);
        break;
      case "host":
        currentGroup.host = val;
        break;
      case "clean-param":
        if (currentGroup.userAgent.some((u) => u.toLowerCase().includes("yandex"))) {
          currentGroup.cleanParam = currentGroup.cleanParam || [];
          currentGroup.cleanParam.push(val);
        } else {
          errors.push(`L${ln}: Clean-param directive is only when targeting Yandex user agent.`);
        }
        break;
      case "content-usage":
        currentGroup.contentUsage = currentGroup.contentUsage || [];
        currentGroup.contentUsage.push(val);
        break;
      case "content-signal":
        currentGroup.contentSignal = currentGroup.contentSignal || [];
        currentGroup.contentSignal.push(val);
        break;
      default:
        errors.push(`L${ln}: Unknown directive ${rule} `);
        break;
    }
  }
  groups.push({
    ...currentGroup
  });
  return {
    groups,
    sitemaps,
    errors,
    warnings
  };
}
function validateContentPreferenceRules(rules, directiveName, validCategories, validValues, example, errors) {
  rules.forEach((rule) => {
    if (rule === "") {
      errors.push(`${directiveName} rule cannot be empty.`);
      return;
    }
    const parts = rule.trim().split(/\s+/);
    const validatePreferences = (preferences) => {
      preferences.forEach((pref) => {
        const [category, value] = pref.split("=").map((s) => s.trim());
        if (!validCategories.includes(category || "")) {
          errors.push(`${directiveName} category "${category}" is invalid. Valid categories: ${validCategories.join(", ")}.`);
        }
        if (!validValues.includes(value || "")) {
          errors.push(`${directiveName} value "${value}" for "${category}" is invalid. Valid values: ${validValues.join(", ")}.`);
        }
      });
    };
    if (parts.length === 1) {
      if (!parts[0]?.includes("=")) {
        errors.push(`${directiveName} rule "${rule}" must contain a preference assignment (e.g., "${example}").`);
        return;
      }
      validatePreferences(parts[0].split(",").map((p) => p.trim()));
    } else if (parts.length >= 2) {
      const firstPart = parts[0];
      if (firstPart?.includes("=")) {
        const allPreferences = rule.split(",").map((p) => p.trim());
        allPreferences.forEach((pref) => {
          if (!pref.includes("=")) {
            errors.push(`${directiveName} rule "${pref}" must contain a preference assignment (e.g., "${example}").`);
            return;
          }
          validatePreferences([pref]);
        });
      } else {
        const path = firstPart;
        const preference = parts.slice(1).join(" ");
        if (!path?.startsWith("/")) {
          errors.push(`${directiveName} path "${path}" must start with a \`/\`.`);
        }
        if (!preference.includes("=")) {
          errors.push(`${directiveName} preference "${preference}" must contain an assignment (e.g., "${example}").`);
        } else {
          validatePreferences(preference.split(",").map((p) => p.trim()));
        }
      }
    }
  });
}
function validateGroupRules(group, errors, warnings) {
  const toCheck = ["allow", "disallow"];
  toCheck.forEach((key) => {
    (group[key] || []).filter((rule) => {
      if (rule === "")
        return true;
      if (!rule.startsWith("/") && !rule.startsWith("*")) {
        errors.push(`Disallow rule "${rule}" must start with a \`/\` or be a \`*\`.`);
        return false;
      }
      if (key === "disallow" && (rule === "/api" || rule === "/api/")) {
        warnings.push(`Disallow rule "${rule}" blocks API routes which may prevent crawlers from functioning correctly (e.g. sitemaps, OG image generation).`);
      }
      return true;
    });
  });
  if (group.contentUsage) {
    validateContentPreferenceRules(group.contentUsage, "Content-Usage", ["bots", "train-ai", "ai-output", "search"], ["y", "n"], "train-ai=n", errors);
  }
  if (group.contentSignal) {
    validateContentPreferenceRules(group.contentSignal, "Content-Signal", ["search", "ai-input", "ai-train"], ["yes", "no"], "ai-train=no", errors);
  }
}
function matches(pattern, path) {
  const pathLength = path.length;
  const patternLength = pattern.length;
  const matchingLengths = Array.from({ length: pathLength + 1 }).fill(0);
  let numMatchingLengths = 1;
  let p = 0;
  while (p < patternLength) {
    if (pattern[p] === "$" && p + 1 === patternLength) {
      return matchingLengths[numMatchingLengths - 1] === pathLength;
    }
    if (pattern[p] === "*") {
      numMatchingLengths = pathLength - matchingLengths[0] + 1;
      for (let i = 1; i < numMatchingLengths; i++) {
        matchingLengths[i] = matchingLengths[i - 1] + 1;
      }
    } else {
      let numMatches = 0;
      for (let i = 0; i < numMatchingLengths; i++) {
        const matchLength = matchingLengths[i];
        if (matchLength < pathLength && path[matchLength] === pattern[p]) {
          matchingLengths[numMatches++] = matchLength + 1;
        }
      }
      if (numMatches === 0) {
        return false;
      }
      numMatchingLengths = numMatches;
    }
    p++;
  }
  return true;
}
function matchPathToRule(path, _rules) {
  let matchedRule = null;
  const rules = _rules.filter(Boolean);
  const rulesLength = rules.length;
  let i = 0;
  while (i < rulesLength) {
    const rule = rules[i];
    if (!rule || !matches(rule.pattern, path)) {
      i++;
      continue;
    }
    if (!matchedRule || rule.pattern.length > matchedRule.pattern.length) {
      matchedRule = rule;
    } else if (rule.pattern.length === matchedRule.pattern.length && rule.allow && !matchedRule.allow) {
      matchedRule = rule;
    }
    i++;
  }
  return matchedRule;
}
function validateRobots(robotsTxt) {
  robotsTxt.groups = robotsTxt.groups.filter((group) => {
    if (!group.allow.length && !group.disallow.length) {
      robotsTxt.errors.push(`Group "${group.userAgent.join(", ")}" has no allow or disallow rules. You must provide one of either.`);
      return false;
    }
    validateGroupRules(group, robotsTxt.errors, robotsTxt.warnings);
    return true;
  });
  return robotsTxt;
}
function asArray(v) {
  return typeof v === "undefined" ? [] : Array.isArray(v) ? v : [v];
}
function contentUsageToString(prefs) {
  return Object.entries(prefs).filter(([_, value]) => value !== void 0).map(([key, value]) => `${key}=${value}`).join(", ");
}
function normalizeContentPreferences(value) {
  if (!value)
    return [];
  if (Array.isArray(value))
    return value.filter((rule) => Boolean(rule));
  if (typeof value === "object" && !Array.isArray(value)) {
    const str = contentUsageToString(value);
    return str ? [str] : [];
  }
  if (typeof value === "string")
    return value ? [value] : [];
  return [];
}
function normalizeGroup(group) {
  if (group._normalized) {
    const resolvedGroup = group;
    const disallow2 = asArray(resolvedGroup.disallow);
    resolvedGroup._indexable = !disallow2.includes("/");
    resolvedGroup._rules = [
      ...resolvedGroup.disallow.filter(Boolean).map((r) => ({ pattern: r, allow: false })),
      ...resolvedGroup.allow.map((r) => ({ pattern: r, allow: true }))
    ];
    return resolvedGroup;
  }
  const disallow = asArray(group.disallow);
  const allow = asArray(group.allow).filter((rule) => Boolean(rule));
  const contentUsage = normalizeContentPreferences(group.contentUsage);
  const contentSignal = normalizeContentPreferences(group.contentSignal);
  return {
    ...group,
    userAgent: group.userAgent ? asArray(group.userAgent) : ["*"],
    disallow,
    allow,
    contentUsage,
    contentSignal,
    _indexable: !disallow.includes("/"),
    _rules: [
      ...disallow.filter(Boolean).map((r) => ({ pattern: r, allow: false })),
      ...allow.map((r) => ({ pattern: r, allow: true }))
    ],
    _normalized: true
  };
}
function generateRobotsTxt({ groups, sitemaps }) {
  const lines = [];
  for (const group of groups) {
    for (const comment of group.comment || [])
      lines.push(`# ${comment}`);
    for (const userAgent of group.userAgent || ["*"])
      lines.push(`User-agent: ${userAgent}`);
    for (const allow of group.allow || [])
      lines.push(`Allow: ${allow}`);
    for (const disallow of group.disallow || [])
      lines.push(`Disallow: ${disallow}`);
    for (const cleanParam of group.cleanParam || [])
      lines.push(`Clean-param: ${cleanParam}`);
    for (const contentUsage of group.contentUsage || [])
      lines.push(`Content-Usage: ${contentUsage}`);
    for (const contentSignal of group.contentSignal || [])
      lines.push(`Content-Signal: ${contentSignal}`);
    lines.push("");
  }
  for (const sitemap of sitemaps)
    lines.push(`Sitemap: ${sitemap}`);
  return lines.join("\n");
}
const merger = createDefu((obj, key, value) => {
  if (Array.isArray(obj[key]) && Array.isArray(value))
    obj[key] = Array.from(/* @__PURE__ */ new Set([...obj[key], ...value]));
  return obj[key];
});
function mergeOnKey(arr, key) {
  const res = {};
  arr.forEach((item) => {
    const k = item[key];
    res[k] = merger(res[k] || {}, item);
  });
  return Object.values(res);
}
function isInternalRoute(_path) {
  const path = withoutLeadingSlash(_path);
  if (path.startsWith(".") || path.startsWith("_"))
    return true;
  if (path.startsWith("cgi-bin") || path.startsWith("cdn-cgi") || path.startsWith("api"))
    return true;
  const lastSegment = path.split("/").pop() || path;
  return lastSegment.includes(".") || path.startsWith("@");
}
function createPatternMap() {
  const patternMap = /* @__PURE__ */ new Map();
  for (const def of BOT_MAP) {
    for (const bot of def.bots) {
      const patterns = [bot.pattern, ...bot.secondaryPatterns || []];
      for (const pattern of patterns) {
        patternMap.set(pattern.toLowerCase(), {
          botName: bot.name,
          botCategory: def.type,
          trusted: def.trusted
        });
      }
    }
  }
  return patternMap;
}
function isBotFromHeaders(headers, patternMap) {
  const userAgent = Array.isArray(headers["user-agent"]) ? headers["user-agent"][0] : headers["user-agent"];
  if (!userAgent) {
    return { isBot: false };
  }
  const userAgentLower = userAgent.toLowerCase();
  const defaultBotTarget = patternMap ? void 0 : matchDefaultBotTarget(userAgentLower);
  if (typeof defaultBotTarget !== "undefined") {
    const definition = BOT_MAP[defaultBotTarget >> 8];
    const bot = definition.bots[defaultBotTarget & 255];
    return {
      isBot: true,
      data: {
        botName: bot.name,
        botCategory: definition.type,
        trusted: definition.trusted
      }
    };
  }
  let botData;
  if (patternMap) {
    for (const [pattern, candidate] of patternMap) {
      if (userAgentLower.includes(pattern)) {
        botData = candidate;
        break;
      }
    }
  }
  if (botData) {
    return {
      isBot: true,
      data: {
        botName: botData.botName,
        botCategory: botData.botCategory,
        trusted: botData.trusted
      }
    };
  }
  return { isBot: false };
}
function getBotDetection(headers, patternMap) {
  const userAgent = Array.isArray(headers["user-agent"]) ? headers["user-agent"][0] : headers["user-agent"];
  const detection = isBotFromHeaders(headers, patternMap);
  if (detection.isBot && detection.data) {
    return {
      isBot: true,
      userAgent,
      detectionMethod: "headers",
      botName: detection.data.botName,
      botCategory: detection.data.botCategory,
      trusted: detection.data.trusted
    };
  }
  return {
    isBot: false,
    userAgent
  };
}
function isBot(headers, patternMap) {
  const detection = getBotDetection(headers, patternMap);
  return detection.isBot;
}
function getBotInfo(headers, patternMap) {
  const detection = getBotDetection(headers, patternMap);
  if (!detection.isBot) {
    return null;
  }
  return {
    name: detection.botName,
    category: detection.botCategory,
    trusted: detection.trusted,
    method: detection.detectionMethod
  };
}
function robotsDirectivesFromObject(obj) {
  const directives = [];
  for (const [key, value] of Object.entries(obj)) {
    if (value === false || value === null || value === void 0)
      continue;
    if (key in ROBOT_DIRECTIVE_VALUES && typeof value === "boolean" && value) {
      directives.push(ROBOT_DIRECTIVE_VALUES[key]);
    } else if (key === "max-image-preview" && typeof value === "string") {
      directives.push(formatMaxImagePreview(value));
    } else if (key === "max-snippet" && typeof value === "number") {
      directives.push(formatMaxSnippet(value));
    } else if (key === "max-video-preview" && typeof value === "number") {
      directives.push(formatMaxVideoPreview(value));
    }
  }
  return directives;
}
function normaliseRobotsRouteRule(config) {
  if (!config)
    return void 0;
  let allow;
  if (typeof config.robots === "boolean")
    allow = config.robots;
  else if (typeof config.robots === "object" && "indexable" in config.robots && typeof config.robots.indexable !== "undefined")
    allow = config.robots.indexable;
  let rule;
  if (typeof config.robots === "object" && config.robots !== null) {
    if ("rule" in config.robots && typeof config.robots.rule !== "undefined") {
      rule = config.robots.rule;
    } else if (!("indexable" in config.robots)) {
      const directives = robotsDirectivesFromObject(config.robots);
      if (directives.length > 0) {
        rule = directives.join(", ");
      }
    }
  } else if (typeof config.robots === "string") {
    rule = config.robots;
  }
  if (rule && typeof allow === "undefined") {
    const disallowIndicators = ["none", "noindex", "noai", "noimageai"];
    allow = !disallowIndicators.some(
      (indicator) => rule === indicator || rule.split(",").some((part) => part.trim() === indicator)
    );
  }
  if (typeof allow === "undefined" && typeof rule === "undefined")
    return;
  return {
    allow,
    rule
  };
}

export { AI_BOTS, AUTOMATION_BOTS, AiBots, BOT_MAP, GENERIC_BOTS, HTTP_TOOL_BOTS, KNOWN_SEARCH_BOTS, NonHelpfulBots, ROBOT_DIRECTIVE_VALUES, SCRAPING_BOTS, SECURITY_SCANNING_BOTS, SEO_BOTS, SOCIAL_BOTS, asArray, createPatternMap, formatMaxImagePreview, formatMaxSnippet, formatMaxVideoPreview, generateRobotsTxt, getBotDetection, getBotInfo, isBot, isBotFromHeaders, isInternalRoute, mapBotKindToCategory, matchPathToRule, mergeOnKey, normaliseRobotsRouteRule, normalizeGroup, parseRobotsTxt, robotsDirectivesFromObject, validateRobots };
