import type { H3Event } from '#nuxtseo/h3';
import type { ModuleRuntimeConfig, SitemapSourceBase, SitemapSourceInput, SitemapSourceResolved } from '../../../types.js';
export declare function normalizeSourceInput(source: SitemapSourceInput): SitemapSourceBase | SitemapSourceResolved;
export declare function fetchDataSource(input: SitemapSourceBase | SitemapSourceResolved, event?: H3Event): Promise<SitemapSourceResolved>;
export declare function globalSitemapSources(): Promise<any[]>;
export declare function childSitemapSources(definition: ModuleRuntimeConfig['sitemaps'][string]): Promise<any[]>;
export declare function resolveSitemapSources(sources: SitemapSourceInput[], event?: H3Event): Promise<SitemapSourceResolved[]>;
