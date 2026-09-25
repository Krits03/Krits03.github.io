type ChecklistItemLevel = 'required' | 'recommended';
interface ChecklistItemDefinition {
    /** Unique ID within its module, e.g. 'site-url' */
    id: string;
    /** Human-readable label */
    label: string;
    /** Why this matters */
    description: string;
    level: ChecklistItemLevel;
    /** URL to relevant docs */
    docsUrl: string;
}
interface NuxtSEOModule {
    slug: 'nuxt-seo' | 'site-config' | 'robots' | 'sitemap' | 'og-image' | 'link-checker' | 'seo-utils' | 'schema-org' | 'skew-protection' | 'ai-ready' | 'ai-kit';
    label: string;
    icon: string;
    description: string;
    repo: string;
    npm: string;
    playgrounds?: Record<string, string>;
}
declare const NuxtSEO: NuxtSEOModule;
declare const SiteConfigModule: NuxtSEOModule;
declare const RobotsModule: NuxtSEOModule;
declare const SitemapModule: NuxtSEOModule;
declare const OgImageModule: NuxtSEOModule;
declare const LinkCheckerModule: NuxtSEOModule;
declare const SeoUtilsModule: NuxtSEOModule;
declare const SchemaOrgModule: NuxtSEOModule;
declare const SkewProtectionModule: NuxtSEOModule;
declare const AiReadyModule: NuxtSEOModule;
declare const modules: NuxtSEOModule[];
declare const bundledModules: NuxtSEOModule[];
declare const standaloneModules: NuxtSEOModule[];
/** @deprecated Use `bundledModules` */
declare const normalModules: NuxtSEOModule[];
/** @deprecated Use `standaloneModules` */
declare const proModules: NuxtSEOModule[];

export { AiReadyModule, LinkCheckerModule, NuxtSEO, OgImageModule, RobotsModule, SchemaOrgModule, SeoUtilsModule, SiteConfigModule, SitemapModule, SkewProtectionModule, bundledModules, modules, normalModules, proModules, standaloneModules };
export type { ChecklistItemDefinition, ChecklistItemLevel, NuxtSEOModule };
