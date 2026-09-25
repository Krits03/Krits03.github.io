import { existsSync } from 'node:fs';
import { loadFile, writeFile } from 'magicast';
import { addNuxtModule } from 'magicast/helpers';
import { join } from 'pathe';
import { logger } from '../../dist/runtime/logger.js';

function parseFontString(font) {
  const parts = font.split(":");
  if (parts.length === 3) {
    return {
      name: parts[0] || font,
      style: parts[1] === "ital" ? "italic" : "normal",
      weight: Number.parseInt(parts[2] || "") || 400
    };
  }
  return {
    name: parts[0] || font,
    weight: Number.parseInt(parts[1] || "") || 400,
    style: "normal"
  };
}
function groupFontsByFamily(fonts) {
  const families = /* @__PURE__ */ new Map();
  for (const font of fonts) {
    const parsed = parseFontString(font);
    const existing = families.get(parsed.name);
    if (existing) {
      existing.weights.add(parsed.weight);
      existing.styles.add(parsed.style);
    } else {
      families.set(parsed.name, {
        weights: /* @__PURE__ */ new Set([parsed.weight]),
        styles: /* @__PURE__ */ new Set([parsed.style])
      });
    }
  }
  return Array.from(families.entries(), ([name, { weights, styles }]) => ({
    name,
    weights: [...weights].toSorted((a, b) => a - b),
    styles: [...styles]
  }));
}
async function migrateFontsConfig(rootDir) {
  const configPaths = [
    "nuxt.config.ts",
    "nuxt.config.js",
    "nuxt.config.mjs"
  ];
  let configPath;
  for (const p of configPaths) {
    const fullPath = join(rootDir, p);
    if (existsSync(fullPath)) {
      configPath = fullPath;
      break;
    }
  }
  if (!configPath) {
    return { migrated: false, message: "No nuxt.config found" };
  }
  const mod = await loadFile(configPath);
  const config = mod.exports.default;
  if (!config?.ogImage?.fonts) {
    return { migrated: false, message: "No ogImage.fonts config found" };
  }
  const oldFonts = config.ogImage.fonts;
  if (!Array.isArray(oldFonts) || oldFonts.length === 0) {
    return { migrated: false, message: "ogImage.fonts is empty or invalid" };
  }
  const groupedFonts = groupFontsByFamily(oldFonts);
  if (!config.fonts) {
    config.fonts = {};
  }
  if (!config.fonts.families) {
    config.fonts.families = [];
  }
  const existingFamilies = config.fonts.families;
  for (const font of groupedFonts) {
    const existing = existingFamilies.find((f) => f.name === font.name);
    if (existing) {
      const existingWeights = new Set(existing.weights || []);
      for (const w of font.weights) {
        existingWeights.add(w);
      }
      existing.weights = [...existingWeights].toSorted((a, b) => a - b);
      if (font.styles.includes("italic")) {
        const existingStyles = new Set(existing.styles || ["normal"]);
        existingStyles.add("italic");
        existing.styles = [...existingStyles];
      }
      existing.global = true;
    } else {
      const family = {
        name: font.name,
        weights: font.weights,
        global: true
      };
      if (font.styles.includes("italic")) {
        family.styles = font.styles;
      }
      existingFamilies.push(family);
    }
  }
  addNuxtModule(mod, "@nuxt/fonts");
  delete config.ogImage.fonts;
  if (Object.keys(config.ogImage).length === 0) {
    delete config.ogImage;
  }
  await writeFile(mod, configPath);
  const familyNames = groupedFonts.map((f) => f.name).join(", ");
  return {
    migrated: true,
    message: `Migrated fonts (${familyNames}) from ogImage.fonts to @nuxt/fonts`
  };
}
async function migrateDefaultsComponent(rootDir) {
  const configPaths = [
    "nuxt.config.ts",
    "nuxt.config.js",
    "nuxt.config.mjs"
  ];
  let configPath;
  for (const cp of configPaths) {
    const fullPath = join(rootDir, cp);
    if (existsSync(fullPath)) {
      configPath = fullPath;
      break;
    }
  }
  if (!configPath)
    return { migrated: false, componentName: null, message: "No nuxt.config found" };
  const mod = await loadFile(configPath);
  const config = mod.exports.default;
  if (!config?.ogImage?.defaults?.component)
    return { migrated: false, componentName: null, message: "No defaults.component found" };
  const componentName = String(config.ogImage.defaults.component);
  delete config.ogImage.defaults.component;
  if (config.ogImage.defaults && Object.keys(config.ogImage.defaults).length === 0)
    delete config.ogImage.defaults;
  if (config.ogImage && Object.keys(config.ogImage).length === 0)
    delete config.ogImage;
  await writeFile(mod, configPath);
  return { migrated: true, componentName, message: `Removed defaults.component: '${componentName}'` };
}
async function promptFontsMigration(rootDir) {
  logger.info("");
  logger.info("Detected deprecated ogImage.fonts configuration.");
  logger.info("");
  logger.info("Inter fonts now work out of the box without any configuration.");
  logger.info("For custom fonts, use @nuxt/fonts:");
  logger.info("");
  logger.info("Before:");
  logger.info("  ogImage: {");
  logger.info("    fonts: ['Inter:400', 'Inter:700']");
  logger.info("  }");
  logger.info("");
  logger.info("After (Inter only): Remove the config entirely \u2014 it works by default.");
  logger.info("");
  logger.info("After (custom fonts):");
  logger.info("  modules: ['@nuxt/fonts', 'nuxt-og-image'],");
  logger.info("  fonts: {");
  logger.info("    families: [");
  logger.info("      { name: 'Roboto', weights: [400, 700], global: true }");
  logger.info("    ]");
  logger.info("  }");
  logger.info("");
  const migrate = await logger.prompt("Automatically migrate nuxt.config?", {
    type: "confirm",
    initial: true
  });
  if (migrate) {
    const result = await migrateFontsConfig(rootDir).catch((err) => {
      logger.error(`Migration failed: ${err.message}`);
      return { migrated: false, message: err.message };
    });
    if (result.migrated) {
      logger.success(result.message);
      logger.info("");
      logger.info("Please install @nuxt/fonts:");
      logger.info("  npm add @nuxt/fonts");
    } else {
      logger.warn(`Could not migrate: ${result.message}`);
      logger.info("Please migrate manually.");
    }
  } else {
    logger.info("Skipping automatic migration. Please migrate manually.");
  }
}

export { migrateFontsConfig as a, migrateDefaultsComponent as m, promptFontsMigration as p };
