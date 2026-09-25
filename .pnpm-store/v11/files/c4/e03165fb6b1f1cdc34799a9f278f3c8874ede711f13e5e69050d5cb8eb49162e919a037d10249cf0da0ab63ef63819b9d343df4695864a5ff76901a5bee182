import { spawn } from 'node:child_process';
import { existsSync, readFileSync, readdirSync, mkdirSync, writeFileSync } from 'node:fs';
import { createRequire } from 'node:module';
import { join, dirname } from 'node:path';
import process from 'node:process';
import { onDevToolsInitialized, extendServerRpc, addCustomTab, startSubprocess } from '@nuxt/devtools-kit';
import { useNuxt } from '@nuxt/kit';
import { detectPackageManager } from 'nypm';
import sirv from 'sirv';
import { modules } from './const.mjs';
import { detectNuxtSeoModules } from './kit.mjs';
import 'node:url';
import 'pathe';
import 'pkg-types';
import 'std-env';

function npmForSlug(slug) {
  return modules.find((m) => m.slug === slug)?.npm;
}
const UNIFIED_CLIENT_ROUTE = "/__nuxt-seo-devtools";
const TOOLCHAIN_PACKAGE = "nuxtseo-layer-devtools";
const hashSet = (arr) => [...JSON.stringify(arr)].reduce((h, c) => h * 31 + c.charCodeAt(0) >>> 0, 7).toString(36);
function placeholderHtml() {
  return `<!doctype html><html><head><meta charset="utf-8"><title>Nuxt SEO DevTools</title>
<style>html,body{margin:0;height:100%;font-family:'Hubot Sans',system-ui,sans-serif;background:oklch(98.4% 0.005 292);color:oklch(16% 0.036 292)}@media(prefers-color-scheme:dark){html,body{background:oklch(11% 0.029 292);color:oklch(96.8% 0.009 292)}}.wrap{height:100%;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:14px;padding:24px;text-align:center}.spin{width:34px;height:34px;border-radius:50%;border:3px solid color-mix(in oklab,oklch(54% 0.225 292) 25%,transparent);border-top-color:oklch(54% 0.225 292);animation:s .8s linear infinite}@keyframes s{to{transform:rotate(360deg)}}h1{font-size:15px;font-weight:600;margin:0}p{font-size:13px;opacity:.6;margin:0;max-width:440px}.mods{display:flex;flex-wrap:wrap;gap:6px;justify-content:center;max-width:420px}.chip{font-size:11px;padding:2px 9px;border-radius:999px;background:color-mix(in oklab,oklch(54% 0.225 292) 14%,transparent);color:oklch(54% 0.225 292)}.btn{font:inherit;font-size:13px;font-weight:600;padding:7px 16px;border-radius:8px;border:0;background:oklch(54% 0.225 292);color:#fff;cursor:pointer}.btn:hover{background:oklch(49% 0.225 292)}.btn:disabled{opacity:.6;cursor:default}.hide{display:none}.step{font-size:12px;font-family:ui-monospace,SFMono-Regular,Menlo,monospace;opacity:.55;max-width:520px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;min-height:16px}.t{font-variant-numeric:tabular-nums;opacity:.85}.err .spin{border-top-color:oklch(60% 0.2 25);border-color:color-mix(in oklab,oklch(60% 0.2 25) 25%,transparent);animation:none}</style></head>
<body><div class="wrap" id="wrap"><div class="spin" id="spin"></div><h1 id="title">Nuxt SEO DevTools</h1><div class="mods" id="mods"></div><p id="desc">Starting\u2026</p><button class="btn hide" id="install">Install</button><div class="step" id="step"></div></div>
<script>
const $=id=>document.getElementById(id)
const esc=s=>(s||'').replace(/[<>&]/g,c=>({'<':'&lt;','>':'&gt;','&':'&amp;'}[c]))
let mods=false,clicked=false
$('install').addEventListener('click',async()=>{
  clicked=true
  $('install').disabled=true;$('install').classList.add('hide')
  $('spin').classList.remove('hide')
  $('title').textContent='Installing\u2026'
  $('desc').textContent='Adding the dev-only DevTools UI to your project.'
  try{await fetch('${UNIFIED_CLIENT_ROUTE}/__install')}catch{}
})
async function poll(){
  try{
    const j=await (await fetch('${UNIFIED_CLIENT_ROUTE}/__status')).json()
    if(j.ready){location.reload();return}
    if(!mods&&Array.isArray(j.modules)&&j.modules.length){mods=true;$('mods').innerHTML=j.modules.map(m=>'<span class="chip">'+esc(m)+'</span>').join('')}
    if(j.failed){$('wrap').classList.add('err');$('spin').classList.remove('hide');$('install').classList.add('hide');$('title').textContent='DevTools unavailable';$('desc').textContent='';$('step').textContent=j.step||'';return}
    if(j.needsInstall&&!clicked){
      const pkg=j.packageName||'nuxtseo-devtools'
      $('spin').classList.add('hide')
      $('install').classList.remove('hide');$('install').disabled=false;$('install').textContent='Install '+pkg
      $('title').textContent='Nuxt SEO DevTools'
      $('desc').textContent='The panel needs '+pkg+' (dev only). Installing it adds the package to your devDependencies; nothing is changed until you choose to install.'
      $('step').textContent=''
      return
    }
    $('spin').classList.remove('hide');$('install').classList.add('hide')
    $('title').textContent=j.installing?'Installing\u2026':'Building Nuxt SEO DevTools\u2026'
    $('desc').textContent=j.installing?'Adding the dev-only DevTools UI to your project.':'Assembling panels for your installed modules. This runs once.'
    const t=j.elapsed?' \xB7 <span class="t">'+Math.round(j.elapsed/1000)+'s</span>':''
    $('step').innerHTML=esc(j.step)+t
  }catch{}
}
setInterval(poll,800);poll()
<\/script></body></html>`;
}
function deriveRoutes(layerDir, slug) {
  const routes = [`/${slug}`];
  const pagesDir = join(layerDir, "pages", slug);
  if (existsSync(pagesDir)) {
    for (const f of readdirSync(pagesDir)) {
      if (f.endsWith(".vue") && f !== "index.vue")
        routes.push(`/${slug}/${f.slice(0, -4)}`);
    }
  }
  return routes;
}
function registerSharedRpcOnce(nuxt) {
  if (nuxt._seoDevtoolsRpcRegistered)
    return;
  nuxt._seoDevtoolsRpcRegistered = true;
  onDevToolsInitialized(() => {
    extendServerRpc("nuxt-seo-modules", {
      // Registered modules (those that shipped a devtools panel) carry the iframe route.
      // detectNuxtSeoModules adds every *installed* SEO module from nuxt's module list —
      // independent of whether it self-registered a panel or which shared version it ships —
      // so the picker reflects the full install (e.g. site-config, which has no panel).
      getInstalledSeoModules: () => {
        const byNpm = /* @__PURE__ */ new Map();
        for (const m of nuxt._seoDevtoolsModules || []) {
          if (m.npm)
            byNpm.set(m.npm, m);
        }
        for (const det of detectNuxtSeoModules(nuxt)) {
          if (!byNpm.has(det.name)) {
            const meta = modules.find((s) => s.npm === det.name);
            byNpm.set(det.name, { name: meta?.slug ?? det.name, npm: det.name, title: meta?.label ?? det.name, icon: meta?.icon ?? "", route: "" });
          }
        }
        return [...byNpm.values()];
      }
    }, nuxt);
  }, nuxt);
}
function resolveBaseLayer(installed) {
  for (const m of installed) {
    try {
      return dirname(createRequire(join(m.layerDir, "index.js")).resolve("nuxtseo-layer-devtools"));
    } catch {
    }
  }
  console.warn("[nuxt-seo] could not resolve nuxtseo-layer-devtools from any installed SEO module \u2014 add it to the module's dependencies. Falling back to a bare specifier, which only works when your app installs it directly.");
  return "nuxtseo-layer-devtools";
}
function resolveNuxtCli(rootDir) {
  const bases = [process.argv[1], join(rootDir, "index.js")].filter(Boolean);
  for (const base of bases) {
    let req;
    try {
      req = createRequire(base);
    } catch {
      continue;
    }
    for (const spec of ["nuxi", "nuxt", "@nuxt/cli"]) {
      try {
        const pkgPath = req.resolve(`${spec}/package.json`);
        const bin = JSON.parse(readFileSync(pkgPath, "utf8")).bin;
        const rel = typeof bin === "string" ? bin : bin?.nuxi ?? bin?.nuxt;
        if (rel)
          return join(dirname(pkgPath), rel);
      } catch {
      }
    }
  }
  return null;
}
const stripAnsi = (s) => s.replace(new RegExp(`${String.fromCharCode(27)}\\[[0-9;]*m`, "g"), "");
function toolchainInstalled(rootDir) {
  try {
    createRequire(join(rootDir, "index.js")).resolve(TOOLCHAIN_PACKAGE);
    return true;
  } catch {
    return false;
  }
}
async function devAddArgs(rootDir) {
  const pm = await detectPackageManager(rootDir).catch((error) => {
    console.warn(`[nuxt-seo] could not detect the package manager in "${rootDir}", falling back to npm:`, error);
    return null;
  });
  const name = pm?.name ?? "npm";
  if (name === "npm")
    return { command: "npm", args: ["install", "--save-dev", TOOLCHAIN_PACKAGE] };
  if (name === "yarn")
    return { command: "yarn", args: ["add", "--dev", TOOLCHAIN_PACKAGE] };
  return { command: name, args: ["add", "-D", TOOLCHAIN_PACKAGE] };
}
async function installToolchain(rootDir, nuxt, onProgress) {
  const { command, args } = await devAddArgs(rootDir);
  onProgress(`Installing ${TOOLCHAIN_PACKAGE} with ${command}\u2026`);
  return await new Promise((resolve) => {
    const { getProcess } = startSubprocess(
      { command, args, cwd: rootDir },
      { id: "nuxt-seo:install-devtools", name: `Install ${TOOLCHAIN_PACKAGE}`, icon: "carbon:download" },
      nuxt
    );
    const proc = getProcess();
    if (!proc) {
      resolve(false);
      return;
    }
    proc.on("exit", (code) => resolve(code === 0 && toolchainInstalled(rootDir)));
    proc.on("error", (err) => {
      console.error(`[nuxt-seo] could not run "${command} ${args.join(" ")}": ${err.message}`);
      resolve(false);
    });
  });
}
function generateAndBuild(cacheDir, rootDir, installed, hooks) {
  const routes = ["/", ...installed.flatMap((m) => deriveRoutes(m.layerDir, m.slug))];
  const extendsList = [resolveBaseLayer(installed), ...installed.map((m) => m.layerDir)];
  mkdirSync(join(cacheDir, "pages"), { recursive: true });
  writeFileSync(join(cacheDir, "nuxt.config.ts"), `export default defineNuxtConfig({
  extends: ${JSON.stringify(extendsList, null, 2)},
  ssr: false,
  robots: false,
  content: false,
  sitemap: false,
  nitro: { prerender: { routes: ${JSON.stringify(routes)} }, output: { publicDir: ${JSON.stringify(join(cacheDir, "dist/devtools"))} } },
  app: { baseURL: '${UNIFIED_CLIENT_ROUTE}' },
  compatibilityDate: '2026-03-13',
})
`);
  writeFileSync(join(cacheDir, "app.vue"), `<template><NuxtPage /></template>
`);
  writeFileSync(join(cacheDir, "pages/index.vue"), `<template><div class="p-4">${installed.map((m) => `<NuxtLink to="/${m.slug}" class="block underline">${m.title}</NuxtLink>`).join("")}</div></template>
`);
  console.log(`[nuxt-seo] building devtools client for: ${installed.map((m) => m.slug).join(", ")}`);
  const cliBin = resolveNuxtCli(rootDir);
  const child = cliBin ? spawn(process.execPath, [cliBin, "build"], { cwd: cacheDir, stdio: ["inherit", "pipe", "pipe"] }) : spawn("npx", ["nuxi", "build"], { cwd: cacheDir, stdio: ["inherit", "pipe", "pipe"], shell: true });
  const statusLine = /^(?:[ℹ✔✓✨⚠✖✗●➜√]|\[\w)/;
  const buffered = [];
  let drawing = false;
  const capture = (chunk) => {
    buffered.push(chunk);
    const step = stripAnsi(chunk.toString()).split("\n").map((l) => l.trim()).filter((l) => statusLine.test(l)).pop();
    if (step) {
      hooks.onProgress(step);
      process.stdout.write(`\r\x1B[2K[nuxt-seo] ${step}`);
      drawing = true;
    }
  };
  const endLine = () => {
    if (drawing) {
      process.stdout.write("\n");
      drawing = false;
    }
  };
  child.stdout?.on("data", capture);
  child.stderr?.on("data", capture);
  child.on("error", (err) => {
    endLine();
    console.error(`[nuxt-seo] could not build devtools client, the panel will stay unavailable: ${err.message}`);
    hooks.onError();
  });
  child.on("exit", (code) => {
    endLine();
    if (code === 0) {
      writeFileSync(join(cacheDir, ".installed-hash"), hashSet(installed.map((m) => m.slug).sort()));
      hooks.onReady();
      console.log("[nuxt-seo] devtools client ready");
    } else {
      process.stderr.write(Buffer.concat(buffered));
      console.error(`[nuxt-seo] devtools client build exited with code ${code}, the panel will stay unavailable`);
      hooks.onError();
    }
  });
}
function setupLayerModule(config, layerDir, nuxt) {
  const slug = config.slug ?? config.name.replace(/^nuxt-/, "");
  const clientRoute = `${UNIFIED_CLIENT_ROUTE}/${slug}`;
  const modules = nuxt._seoDevtoolsModules ??= [];
  modules.push({ name: config.name, npm: npmForSlug(slug), title: config.title, icon: config.icon, route: clientRoute });
  const layers = nuxt._seoDevtoolsLayers ??= [];
  layers.push({ slug, name: config.name, title: config.title, icon: config.icon, layerDir });
  addCustomTab({ name: `nuxt-seo-${slug}`, title: config.title, icon: config.icon, view: { type: "iframe", src: clientRoute } });
  if (nuxt._seoDevtoolsInit)
    return;
  nuxt._seoDevtoolsInit = true;
  const cacheDir = join(nuxt.options.rootDir, "node_modules/.cache/nuxt-seo-devtools");
  const dist = join(cacheDir, "dist/devtools");
  const state = { ready: false, building: false, installing: false, needsInstall: false, failed: false, startedAt: 0, step: "", modules: [] };
  const rootDir = nuxt.options.rootDir;
  function ensureBuilt() {
    if (state.ready || state.building)
      return;
    state.building = true;
    state.failed = false;
    state.startedAt = Date.now();
    state.step = "Starting build\u2026";
    const installed = nuxt._seoDevtoolsLayers;
    state.modules = installed.map((m) => m.title);
    generateAndBuild(cacheDir, rootDir, installed, {
      onProgress: (step) => {
        state.step = step;
      },
      onReady: () => {
        state.ready = true;
        state.building = false;
      },
      onError: (message) => {
        state.building = false;
        state.failed = true;
        state.step = message ?? "Build failed, see the dev server logs";
      }
    });
  }
  function startInstall() {
    if (state.installing || state.building || state.ready)
      return;
    state.installing = true;
    state.needsInstall = false;
    state.failed = false;
    state.startedAt = Date.now();
    state.step = `Installing ${TOOLCHAIN_PACKAGE}\u2026`;
    installToolchain(rootDir, nuxt, (step) => {
      state.step = step;
    }).then((ok) => {
      state.installing = false;
      if (ok) {
        ensureBuilt();
      } else {
        state.failed = true;
        state.step = `Could not install ${TOOLCHAIN_PACKAGE} \u2014 see the dev server logs`;
      }
    }).catch((err) => {
      state.installing = false;
      state.failed = true;
      state.step = `Could not install ${TOOLCHAIN_PACKAGE} \u2014 see the dev server logs`;
      console.error(`[nuxt-seo] devtools toolchain install failed: ${err.message}`);
    });
  }
  nuxt.hook("modules:done", () => {
    const installed = nuxt._seoDevtoolsLayers;
    const key = hashSet(installed.map((m) => m.slug).sort());
    state.ready = existsSync(join(cacheDir, ".installed-hash")) && readFileSync(join(cacheDir, ".installed-hash"), "utf8") === key && existsSync(dist);
  });
  nuxt.hook("vite:serverCreated", (server) => {
    const serve = sirv(dist, { dev: true, single: "200.html" });
    server.middlewares.use(UNIFIED_CLIENT_ROUTE, (req, res, next) => {
      const url = req.url || "/";
      if (url.startsWith("/__install")) {
        startInstall();
        res.setHeader("content-type", "application/json");
        return res.end(JSON.stringify({ installing: state.installing }));
      }
      if (url.startsWith("/__status")) {
        if (!state.ready && !state.building && !state.installing) {
          if (toolchainInstalled(rootDir))
            ensureBuilt();
          else
            state.needsInstall = true;
        }
        res.setHeader("content-type", "application/json");
        return res.end(JSON.stringify({
          ready: state.ready,
          failed: state.failed,
          needsInstall: state.needsInstall,
          installing: state.installing,
          packageName: TOOLCHAIN_PACKAGE,
          step: state.step,
          modules: state.modules,
          elapsed: state.startedAt ? Date.now() - state.startedAt : 0
        }));
      }
      if (!state.ready) {
        res.setHeader("content-type", "text/html");
        return res.end(placeholderHtml());
      }
      return serve(req, res, next);
    });
  });
}
function setupLegacyModule(config, clientPath, nuxt) {
  const { name, title, icon, devPort = 3030 } = config;
  const slug = config.slug ?? name.replace(/^nuxt-/, "");
  const route = config.route ?? `/__${slug}`;
  const modules = nuxt._seoDevtoolsModules ??= [];
  modules.push({ name, npm: npmForSlug(slug), title, icon, route });
  const isProductionBuild = existsSync(clientPath) && readdirSync(clientPath).length > 0;
  if (isProductionBuild) {
    nuxt.hook("vite:serverCreated", (server) => {
      server.middlewares.use(route, sirv(clientPath, { dev: true, single: true }));
    });
  } else {
    nuxt.hook("vite:extendConfig", (viteConfig) => {
      Object.assign(viteConfig, {
        server: {
          ...viteConfig.server,
          proxy: {
            ...viteConfig.server?.proxy,
            [route]: {
              target: `http://localhost:${devPort}${route}`,
              changeOrigin: true,
              followRedirects: true,
              ws: true,
              rewrite: (p) => p.replace(route, ""),
              configure: (proxy) => {
                proxy.on("error", (err, _req, res) => {
                  if (res.headersSent)
                    return;
                  res.writeHead(502, { "Content-Type": "text/plain" });
                  res.end(`Devtools client not ready: ${err.message}`);
                });
              }
            }
          }
        }
      });
    });
  }
  addCustomTab({ name, title, icon, view: { type: "iframe", src: route } });
}
function setupDevToolsUI(config, resolve, nuxt = useNuxt()) {
  if (!nuxt.options.dev)
    return;
  const layerFallback = resolve("./devtools");
  const layerCandidates = [layerFallback, resolve("../devtools")];
  const layerDir = layerCandidates.find((dir) => existsSync(join(dir, "nuxt.config.ts"))) ?? layerFallback;
  const isLayer = existsSync(join(layerDir, "nuxt.config.ts")) && !existsSync(join(layerDir, "index.html"));
  registerSharedRpcOnce(nuxt);
  if (isLayer)
    setupLayerModule(config, layerDir, nuxt);
  else
    setupLegacyModule(config, layerDir, nuxt);
}
function setupDevToolsRpc(namespace, serverFunctions, nuxt = useNuxt()) {
  return new Promise((resolve) => {
    onDevToolsInitialized(() => {
      resolve(extendServerRpc(namespace, serverFunctions, nuxt));
    }, nuxt);
  });
}

export { UNIFIED_CLIENT_ROUTE, setupDevToolsRpc, setupDevToolsUI };
