## 3.0.0-beta.10 (2022-07-11)

* feat: expose server resolved urls (#8986) ([26bcdc3](https://github.com/vitejs/vite/commit/26bcdc3)), closes [#8986](https://github.com/vitejs/vite/issues/8986)
* feat: show ws connection error (#9007) ([da7c3ae](https://github.com/vitejs/vite/commit/da7c3ae)), closes [#9007](https://github.com/vitejs/vite/issues/9007)
* chore: fix test optimizeDeps at build time flag (#9004) ([9363872](https://github.com/vitejs/vite/commit/9363872)), closes [#9004](https://github.com/vitejs/vite/issues/9004)
* chore: ignore ts warning (#9015) ([e2a6bf4](https://github.com/vitejs/vite/commit/e2a6bf4)), closes [#9015](https://github.com/vitejs/vite/issues/9015)
* chore: scanner after server listen (#9020) ([53799e1](https://github.com/vitejs/vite/commit/53799e1)), closes [#9020](https://github.com/vitejs/vite/issues/9020)
* chore: v3.0.0-beta.9 release notes (#8996) ([2a9bc6d](https://github.com/vitejs/vite/commit/2a9bc6d)), closes [#8996](https://github.com/vitejs/vite/issues/8996)
* chore(deps): update all non-major dependencies (#9022) ([6342140](https://github.com/vitejs/vite/commit/6342140)), closes [#9022](https://github.com/vitejs/vite/issues/9022)
* fix(ssr): sourcemap content (fixes #8657) (#8997) ([aff4544](https://github.com/vitejs/vite/commit/aff4544)), closes [#8657](https://github.com/vitejs/vite/issues/8657) [#8997](https://github.com/vitejs/vite/issues/8997)
* docs: update api-javascript (#8999) ([05b17df](https://github.com/vitejs/vite/commit/05b17df)), closes [#8999](https://github.com/vitejs/vite/issues/8999)



## 3.0.0-beta.9 (2022-07-08)

### Main Changes

- New docs theme using [VitePress](https://vitepress.vuejs.org/) v1 alpha: https://main.vitejs.dev
- Vite CLI
  - The default dev server port is now 5173, with the preview server starting at 4173.
  - The default dev server host is now `localhost` instead of `127.0.0.1`.
- Compatibility
  - Vite no longer supports Node v12, which reached its EOL. Node 14.18+ is now required.
  - Vite is now published as ESM, with a CJS proxy to the ESM entry for compatibility.
  - The Modern Browser Baseline now targets browsers which support the [native ES Modules](https://caniuse.com/es6-module) and [native ESM dynamic import](https://caniuse.com/es6-module-dynamic-import) and [`import.meta`](https://caniuse.com/mdn-javascript_statements_import_meta).
  - JS file extensions in SSR and lib mode now use a valid extension (`js`, `mjs`, or `cjs`) for output JS entries and chunks based on their format and the package type.
- Architecture changes
  - Vite now avoids full reload during cold start when imports are injected by plugins in while crawling the initial statically imported modules ([#8869](https://github.com/vitejs/vite/issues/8869)).
  - Vite uses ESM for the SSR build by default, and previous [SSR externalization heuristics](https://vitejs.dev/guide/ssr.html#ssr-externals) are no longer needed.
- `import.meta.glob` has been improved, read about the new features in the [Glob Import Guide](https://main.vitejs.dev/guide/features.html#glob-import)
- The WebAssembly import API has been revised to avoid collisions with future standards. Read more in the [WebAssembly guide](https://main.vitejs.dev/guide/features.html#webassembly)
- Improved support for relative base.
- Experimental Features
  - [Build Advanced Base Options](https://main.vitejs.dev/guide/build.html#advanced-base-options)
  - [HMR Partial Accept](https://github.com/vitejs/vite/pull/7324)
  - Vite now allows the use of [esbuild to optimize dependencies during build time](https://main.vitejs.dev/guide/migration.html#using-esbuild-deps-optimization-at-build-time) avoiding the need of [`@rollupjs/plugin-commonjs`](https://github.com/rollup/plugins/tree/master/packages/commonjs), removing one of the difference id dependency handling between dev and prod.
- Bundle size reduction 
  - Terser is now an optional dependency. If you use `build.minify: 'terser'`, you'll need to install it (`npm add -D terser`)
  - node-forge moved out of the monorepo to [@vitejs/plugin-basic-ssl](https://main.vitejs.dev/guide/migration.html#automatic-https-certificate-generation)
- Options that were [already deprecated in v2](https://main.vitejs.dev/guide/migration.html#config-options-changes) have been removed. 
  
> **Note**
> Before updating, check out the [migration guide from v2](https://main.vitejs.dev/guide/migration)

### Features

* refactor: opt-in optimizeDeps during build and SSR (#8965) ([f8c8cf2](https://github.com/vitejs/vite/commit/f8c8cf2)), closes [#8965](https://github.com/vitejs/vite/issues/8965)
* refactor!: move basic ssl setup to external plugin, fix #8532 (#8961) ([5c6cf5a](https://github.com/vitejs/vite/commit/5c6cf5a)), closes [#8532](https://github.com/vitejs/vite/issues/8532) [#8961](https://github.com/vitejs/vite/issues/8961)
* feat: avoid scanner during build and only optimize CJS in SSR (#8932) ([339d9e3](https://github.com/vitejs/vite/commit/339d9e3)), closes [#8932](https://github.com/vitejs/vite/issues/8932)
* feat: improved cold start using deps scanner (#8869) ([188f188](https://github.com/vitejs/vite/commit/188f188)), closes [#8869](https://github.com/vitejs/vite/issues/8869)
* feat: ssr.optimizeDeps (#8917) ([f280dd9](https://github.com/vitejs/vite/commit/f280dd9)), closes [#8917](https://github.com/vitejs/vite/issues/8917)
* feat: support import assertions (#8937) ([2390422](https://github.com/vitejs/vite/commit/2390422)), closes [#8937](https://github.com/vitejs/vite/issues/8937)
* feat: accept AcceptedPlugin type for postcss plugin (#8830) ([6886078](https://github.com/vitejs/vite/commit/6886078)), closes [#8830](https://github.com/vitejs/vite/issues/8830)
* feat: ssrBuild flag in config env (#8863) ([b6d655a](https://github.com/vitejs/vite/commit/b6d655a)), closes [#8863](https://github.com/vitejs/vite/issues/8863)
* feat: experimental.renderBuiltUrl (revised build base options) (#8762) ([895a7d6](https://github.com/vitejs/vite/commit/895a7d6)), closes [#8762](https://github.com/vitejs/vite/issues/8762)
* feat: respect esbuild minify config for css (#8811) ([d90409e](https://github.com/vitejs/vite/commit/d90409e)), closes [#8811](https://github.com/vitejs/vite/issues/8811)
* feat: use esbuild supported feature (#8665) ([2061d41](https://github.com/vitejs/vite/commit/2061d41)), closes [#8665](https://github.com/vitejs/vite/issues/8665)
* feat: respect esbuild minify config (#8754) ([8b77695](https://github.com/vitejs/vite/commit/8b77695)), closes [#8754](https://github.com/vitejs/vite/issues/8754)
* feat: update rollup commonjs plugin to v22  (#8743) ([d4dcdd1](https://github.com/vitejs/vite/commit/d4dcdd1)), closes [#8743](https://github.com/vitejs/vite/issues/8743)
* feat: enable tree-shaking for lib es (#8737) ([5dc0f72](https://github.com/vitejs/vite/commit/5dc0f72)), closes [#8737](https://github.com/vitejs/vite/issues/8737)
* feat: supports cts and mts config (#8729) ([c2b09db](https://github.com/vitejs/vite/commit/c2b09db)), closes [#8729](https://github.com/vitejs/vite/issues/8729)
* feat: bump minimum node version to 14.18.0 (#8662) ([8a05432](https://github.com/vitejs/vite/commit/8a05432)), closes [#8662](https://github.com/vitejs/vite/issues/8662)
* feat: experimental.buildAdvancedBaseOptions (#8450) ([8ef7333](https://github.com/vitejs/vite/commit/8ef7333)), closes [#8450](https://github.com/vitejs/vite/issues/8450)
* feat: export esbuildVersion and rollupVersion (#8675) ([15ebe1e](https://github.com/vitejs/vite/commit/15ebe1e)), closes [#8675](https://github.com/vitejs/vite/issues/8675)
* feat: print resolved address for localhost (#8647) ([eb52d36](https://github.com/vitejs/vite/commit/eb52d36)), closes [#8647](https://github.com/vitejs/vite/issues/8647)
* feat(hmr): experimental.hmrPartialAccept (#7324) ([83dab7e](https://github.com/vitejs/vite/commit/83dab7e)), closes [#7324](https://github.com/vitejs/vite/issues/7324)
* refactor: type client maps (#8626) ([cf87882](https://github.com/vitejs/vite/commit/cf87882)), closes [#8626](https://github.com/vitejs/vite/issues/8626)
* feat: cleaner default dev output (#8638) ([dbd9688](https://github.com/vitejs/vite/commit/dbd9688)), closes [#8638](https://github.com/vitejs/vite/issues/8638)
* feat: legacy options to revert to v2 strategies (#8623) ([993b842](https://github.com/vitejs/vite/commit/993b842)), closes [#8623](https://github.com/vitejs/vite/issues/8623)
* feat: support async plugins (#8574) ([caa8a58](https://github.com/vitejs/vite/commit/caa8a58)), closes [#8574](https://github.com/vitejs/vite/issues/8574)
* feat: support cjs noExternal in SSR dev, fix #2579 (#8430) ([11d2191](https://github.com/vitejs/vite/commit/11d2191)), closes [#2579](https://github.com/vitejs/vite/issues/2579) [#8430](https://github.com/vitejs/vite/issues/8430)
* feat(dev): added assets to manifest (#6649) ([cdf744d](https://github.com/vitejs/vite/commit/cdf744d)), closes [#6649](https://github.com/vitejs/vite/issues/6649)
* feat!: appType (spa, mpa, custom), boolean middlewareMode (#8452) ([14db473](https://github.com/vitejs/vite/commit/14db473)), closes [#8452](https://github.com/vitejs/vite/issues/8452)
* feat: 500 response if the node proxy request fails (#7398) ([73e1775](https://github.com/vitejs/vite/commit/73e1775)), closes [#7398](https://github.com/vitejs/vite/issues/7398)
* feat: expose createFilter util (#8562) ([c5c424a](https://github.com/vitejs/vite/commit/c5c424a)), closes [#8562](https://github.com/vitejs/vite/issues/8562)
* feat: better config `__dirname` support (#8442) ([51e9195](https://github.com/vitejs/vite/commit/51e9195)), closes [#8442](https://github.com/vitejs/vite/issues/8442)
* feat: expose `version` (#8456) ([e992594](https://github.com/vitejs/vite/commit/e992594)), closes [#8456](https://github.com/vitejs/vite/issues/8456)
* feat: handle named imports of builtin modules (#8338) ([e2e44ff](https://github.com/vitejs/vite/commit/e2e44ff)), closes [#8338](https://github.com/vitejs/vite/issues/8338)
* feat: preserve process env vars in lib build (#8090) ([908c9e4](https://github.com/vitejs/vite/commit/908c9e4)), closes [#8090](https://github.com/vitejs/vite/issues/8090)
* refactor!: make terser an optional dependency (#8049) ([164f528](https://github.com/vitejs/vite/commit/164f528)), closes [#8049](https://github.com/vitejs/vite/issues/8049)
* chore: resolve ssr options (#8455) ([d97e402](https://github.com/vitejs/vite/commit/d97e402)), closes [#8455](https://github.com/vitejs/vite/issues/8455)
* perf: disable postcss sourcemap when unused (#8451) ([64fc61c](https://github.com/vitejs/vite/commit/64fc61c)), closes [#8451](https://github.com/vitejs/vite/issues/8451)
* feat: add ssr.format to force esm output for ssr (#6812) ([337b197](https://github.com/vitejs/vite/commit/337b197)), closes [#6812](https://github.com/vitejs/vite/issues/6812)
* feat: default esm SSR build, simplified externalization (#8348) ([f8c92d1](https://github.com/vitejs/vite/commit/f8c92d1)), closes [#8348](https://github.com/vitejs/vite/issues/8348)
* feat: derive proper js extension from package type (#8382) ([95cdd81](https://github.com/vitejs/vite/commit/95cdd81)), closes [#8382](https://github.com/vitejs/vite/issues/8382)
* feat: ssr build using optimized deps (#8403) ([6a5a5b5](https://github.com/vitejs/vite/commit/6a5a5b5)), closes [#8403](https://github.com/vitejs/vite/issues/8403)
* refactor: `ExportData.imports` to `ExportData.hasImports` (#8355) ([168de2d](https://github.com/vitejs/vite/commit/168de2d)), closes [#8355](https://github.com/vitejs/vite/issues/8355)
* feat: scan free dev server (#8319) ([3f742b6](https://github.com/vitejs/vite/commit/3f742b6)), closes [#8319](https://github.com/vitejs/vite/issues/8319)
* feat: non-blocking esbuild optimization at build time (#8280) ([909cf9c](https://github.com/vitejs/vite/commit/909cf9c)), closes [#8280](https://github.com/vitejs/vite/issues/8280)
* feat: non-blocking needs interop (#7568) ([531cd7b](https://github.com/vitejs/vite/commit/531cd7b)), closes [#7568](https://github.com/vitejs/vite/issues/7568)
* refactor(cli): improve output aesthetics (#6997) ([809ab47](https://github.com/vitejs/vite/commit/809ab47)), closes [#6997](https://github.com/vitejs/vite/issues/6997)
* dx: sourcemap combine debug utils (#8307) ([45dba50](https://github.com/vitejs/vite/commit/45dba50)), closes [#8307](https://github.com/vitejs/vite/issues/8307)
* feat: sourcemap for importAnalysis (#8258) ([a4e4d39](https://github.com/vitejs/vite/commit/a4e4d39)), closes [#8258](https://github.com/vitejs/vite/issues/8258)
* feat: spa option, `preview` and `dev` for MPA and SSR apps (#8217) ([d7cba46](https://github.com/vitejs/vite/commit/d7cba46)), closes [#8217](https://github.com/vitejs/vite/issues/8217)
* feat: vite connected logs changed to console.debug (#7733) ([9f00c41](https://github.com/vitejs/vite/commit/9f00c41)), closes [#7733](https://github.com/vitejs/vite/issues/7733)
* feat: worker support query url (#7914) ([95297dd](https://github.com/vitejs/vite/commit/95297dd)), closes [#7914](https://github.com/vitejs/vite/issues/7914)
* feat(wasm): new wasm plugin (`.wasm?init`) (#8219) ([75c3bf6](https://github.com/vitejs/vite/commit/75c3bf6)), closes [#8219](https://github.com/vitejs/vite/issues/8219)
* build!: bump targets (#8045) ([66efd69](https://github.com/vitejs/vite/commit/66efd69)), closes [#8045](https://github.com/vitejs/vite/issues/8045)
* feat!: migrate to ESM (#8178) ([76fdc27](https://github.com/vitejs/vite/commit/76fdc27)), closes [#8178](https://github.com/vitejs/vite/issues/8178)
* feat!: relative base (#7644) ([09648c2](https://github.com/vitejs/vite/commit/09648c2)), closes [#7644](https://github.com/vitejs/vite/issues/7644)
* feat(css): warn if url rewrite has no importer (#8183) ([0858450](https://github.com/vitejs/vite/commit/0858450)), closes [#8183](https://github.com/vitejs/vite/issues/8183)
* feat: allow any JS identifier in define, not ASCII-only (#5972) ([95eb45b](https://github.com/vitejs/vite/commit/95eb45b)), closes [#5972](https://github.com/vitejs/vite/issues/5972)
* feat: enable `generatedCode: 'es2015'` for rollup build (#5018) ([46d5e67](https://github.com/vitejs/vite/commit/46d5e67)), closes [#5018](https://github.com/vitejs/vite/issues/5018)
* feat: rework `dynamic-import-vars` (#7756) ([80d113b](https://github.com/vitejs/vite/commit/80d113b)), closes [#7756](https://github.com/vitejs/vite/issues/7756)
* feat: worker emit fileName with config (#7804) ([04c2edd](https://github.com/vitejs/vite/commit/04c2edd)), closes [#7804](https://github.com/vitejs/vite/issues/7804)
* feat(glob-import): support `{ import: '*' }` (#8071) ([0b78b2a](https://github.com/vitejs/vite/commit/0b78b2a)), closes [#8071](https://github.com/vitejs/vite/issues/8071)
* build!: remove node v12 support (#7833) ([eeac2d2](https://github.com/vitejs/vite/commit/eeac2d2)), closes [#7833](https://github.com/vitejs/vite/issues/7833)
* feat!: rework `import.meta.glob` (#7537) ([330e0a9](https://github.com/vitejs/vite/commit/330e0a9)), closes [#7537](https://github.com/vitejs/vite/issues/7537)
* feat!: vite dev default port is now 5173 (#8148) ([1cc2e2d](https://github.com/vitejs/vite/commit/1cc2e2d)), closes [#8148](https://github.com/vitejs/vite/issues/8148)
* refactor: remove deprecated api for 3.0 (#5868) ([b5c3709](https://github.com/vitejs/vite/commit/b5c3709)), closes [#5868](https://github.com/vitejs/vite/issues/5868)
* chore: stabilize experimental api (#7707) ([b902932](https://github.com/vitejs/vite/commit/b902932)), closes [#7707](https://github.com/vitejs/vite/issues/7707)
* test: migrate to vitest (#8076) ([8148f67](https://github.com/vitejs/vite/commit/8148f67)), closes [#8076](https://github.com/vitejs/vite/issues/8076)

### Bug Fixes

* fix: respect explicitily external/noExternal config (#8983) ([e369880](https://github.com/vitejs/vite/commit/e369880)), closes [#8983](https://github.com/vitejs/vite/issues/8983)
* fix: cjs interop export names local clash, fix #8950 (#8953) ([2185f72](https://github.com/vitejs/vite/commit/2185f72)), closes [#8950](https://github.com/vitejs/vite/issues/8950) [#8953](https://github.com/vitejs/vite/issues/8953)
* fix: handle context resolve options (#8966) ([57c6c15](https://github.com/vitejs/vite/commit/57c6c15)), closes [#8966](https://github.com/vitejs/vite/issues/8966)
* fix: re-encode url to prevent fs.allow bypass (fixes #8498) (#8979) ([b835699](https://github.com/vitejs/vite/commit/b835699)), closes [#8498](https://github.com/vitejs/vite/issues/8498) [#8979](https://github.com/vitejs/vite/issues/8979)
* fix(scan): detect import .ts as .js (#8969) ([752af6c](https://github.com/vitejs/vite/commit/752af6c)), closes [#8969](https://github.com/vitejs/vite/issues/8969)
* fix: ssrBuild is optional, avoid breaking VitePress (#8912) ([722f514](https://github.com/vitejs/vite/commit/722f514)), closes [#8912](https://github.com/vitejs/vite/issues/8912)
* fix(css): always use css module content (#8936) ([6e0dd3a](https://github.com/vitejs/vite/commit/6e0dd3a)), closes [#8936](https://github.com/vitejs/vite/issues/8936)
* fix: avoid optimizing non-optimizable external deps (#8860) ([cd8d63b](https://github.com/vitejs/vite/commit/cd8d63b)), closes [#8860](https://github.com/vitejs/vite/issues/8860)
* fix: ensure define overrides import.meta in build (#8892) ([7d810a9](https://github.com/vitejs/vite/commit/7d810a9)), closes [#8892](https://github.com/vitejs/vite/issues/8892)
* fix: ignore Playwright test results directory (#8778) ([314c09c](https://github.com/vitejs/vite/commit/314c09c)), closes [#8778](https://github.com/vitejs/vite/issues/8778)
* fix: node platform for ssr dev regression (#8840) ([7257fd8](https://github.com/vitejs/vite/commit/7257fd8)), closes [#8840](https://github.com/vitejs/vite/issues/8840)
* fix: optimize deps on dev SSR, builtin imports in node (#8854) ([d49856c](https://github.com/vitejs/vite/commit/d49856c)), closes [#8854](https://github.com/vitejs/vite/issues/8854)
* fix: prevent crash when the pad amount is negative (#8747) ([3af6a1b](https://github.com/vitejs/vite/commit/3af6a1b)), closes [#8747](https://github.com/vitejs/vite/issues/8747)
* fix: reverts #8278 ([a0da2f0](https://github.com/vitejs/vite/commit/a0da2f0)), closes [#8278](https://github.com/vitejs/vite/issues/8278)
* fix: server.force deprecation and force on restart API (#8842) ([c94f564](https://github.com/vitejs/vite/commit/c94f564)), closes [#8842](https://github.com/vitejs/vite/issues/8842)
* fix(deps): update all non-major dependencies (#8802) ([a4a634d](https://github.com/vitejs/vite/commit/a4a634d)), closes [#8802](https://github.com/vitejs/vite/issues/8802)
* fix(hmr): set isSelfAccepting unless it is delayed (#8898) ([ae34565](https://github.com/vitejs/vite/commit/ae34565)), closes [#8898](https://github.com/vitejs/vite/issues/8898)
* fix(worker): dont throw on `import.meta.url` in ssr (#8846) ([ef749ed](https://github.com/vitejs/vite/commit/ef749ed)), closes [#8846](https://github.com/vitejs/vite/issues/8846)
* fix: deps optimizer should wait on entries (#8822) ([2db1b5b](https://github.com/vitejs/vite/commit/2db1b5b)), closes [#8822](https://github.com/vitejs/vite/issues/8822)
* fix: incorrectly resolving `knownJsSrcRE` files from root (fixes #4161) (#8808) ([e1e426e](https://github.com/vitejs/vite/commit/e1e426e)), closes [#4161](https://github.com/vitejs/vite/issues/4161) [#8808](https://github.com/vitejs/vite/issues/8808)
* fix: /@fs/ dir traversal with escaped chars (fixes #8498) (#8804) ([6851009](https://github.com/vitejs/vite/commit/6851009)), closes [#8498](https://github.com/vitejs/vite/issues/8498) [#8804](https://github.com/vitejs/vite/issues/8804)
* fix: preserve extension of css assets in the manifest (#8768) ([9508549](https://github.com/vitejs/vite/commit/9508549)), closes [#8768](https://github.com/vitejs/vite/issues/8768)
* fix: always remove temp config (#8782) ([2c2a86b](https://github.com/vitejs/vite/commit/2c2a86b)), closes [#8782](https://github.com/vitejs/vite/issues/8782)
* fix: ensure deps optimizer first run, fixes #8750 (#8775) ([3f689a4](https://github.com/vitejs/vite/commit/3f689a4)), closes [#8750](https://github.com/vitejs/vite/issues/8750) [#8775](https://github.com/vitejs/vite/issues/8775)
* fix: remove buildTimeImportMetaUrl (#8785) ([cd32095](https://github.com/vitejs/vite/commit/cd32095)), closes [#8785](https://github.com/vitejs/vite/issues/8785)
* fix: skip inline html (#8789) ([4a6408b](https://github.com/vitejs/vite/commit/4a6408b)), closes [#8789](https://github.com/vitejs/vite/issues/8789)
* fix(optimizer): only run require-import conversion if require'd (#8795) ([7ae0d3e](https://github.com/vitejs/vite/commit/7ae0d3e)), closes [#8795](https://github.com/vitejs/vite/issues/8795)
* perf: avoid sourcemap chains during dev (#8796) ([1566f61](https://github.com/vitejs/vite/commit/1566f61)), closes [#8796](https://github.com/vitejs/vite/issues/8796)
* perf(lib): improve helper inject regex (#8741) ([19fc7e5](https://github.com/vitejs/vite/commit/19fc7e5)), closes [#8741](https://github.com/vitejs/vite/issues/8741)
* fix: avoid type mismatch with Rollup (fix #7843) (#8701) ([87e51f7](https://github.com/vitejs/vite/commit/87e51f7)), closes [#7843](https://github.com/vitejs/vite/issues/7843) [#8701](https://github.com/vitejs/vite/issues/8701)
* fix: optimizeDeps.entries transformRequest url (fix #8719) (#8748) ([9208c3b](https://github.com/vitejs/vite/commit/9208c3b)), closes [#8719](https://github.com/vitejs/vite/issues/8719) [#8748](https://github.com/vitejs/vite/issues/8748)
* fix(hmr): __HMR_PORT__ should not be `'undefined'` (#8761) ([3271266](https://github.com/vitejs/vite/commit/3271266)), closes [#8761](https://github.com/vitejs/vite/issues/8761)
* fix: respect `rollupOptions.external` for transitive dependencies (#8679) ([4f9097b](https://github.com/vitejs/vite/commit/4f9097b)), closes [#8679](https://github.com/vitejs/vite/issues/8679)
* fix: use esbuild platform browser/node instead of neutral (#8714) ([a201cd4](https://github.com/vitejs/vite/commit/a201cd4)), closes [#8714](https://github.com/vitejs/vite/issues/8714)
* fix: disable inlineDynamicImports for ssr.target = node (#8641) ([3b41a8e](https://github.com/vitejs/vite/commit/3b41a8e)), closes [#8641](https://github.com/vitejs/vite/issues/8641)
* fix: infer hmr ws target by client location (#8650) ([4061ee0](https://github.com/vitejs/vite/commit/4061ee0)), closes [#8650](https://github.com/vitejs/vite/issues/8650)
* fix: non-relative base public paths in CSS files (#8682) ([d11d6ea](https://github.com/vitejs/vite/commit/d11d6ea)), closes [#8682](https://github.com/vitejs/vite/issues/8682)
* fix: SSR with relative base (#8683) ([c1667bb](https://github.com/vitejs/vite/commit/c1667bb)), closes [#8683](https://github.com/vitejs/vite/issues/8683)
* fix: filter of BOM tags in json plugin (#8628) ([e10530b](https://github.com/vitejs/vite/commit/e10530b)), closes [#8628](https://github.com/vitejs/vite/issues/8628)
* fix: revert #5902, fix #8243 (#8654) ([1b820da](https://github.com/vitejs/vite/commit/1b820da)), closes [#8243](https://github.com/vitejs/vite/issues/8243) [#8654](https://github.com/vitejs/vite/issues/8654)
* fix(optimizer): use simple browser external shim in prod (#8630) ([a32c4ba](https://github.com/vitejs/vite/commit/a32c4ba)), closes [#8630](https://github.com/vitejs/vite/issues/8630)
* fix(server): skip localhost verbatim dns lookup (#8642) ([7632247](https://github.com/vitejs/vite/commit/7632247)), closes [#8642](https://github.com/vitejs/vite/issues/8642)
* fix(wasm): support inlined WASM in Node < v16 (fix #8620) (#8622) ([f586b14](https://github.com/vitejs/vite/commit/f586b14)), closes [#8620](https://github.com/vitejs/vite/issues/8620) [#8622](https://github.com/vitejs/vite/issues/8622)
* fix: allow cache overlap in parallel builds (#8592) ([2dd0b49](https://github.com/vitejs/vite/commit/2dd0b49)), closes [#8592](https://github.com/vitejs/vite/issues/8592)
* fix: avoid replacing defines and NODE_ENV in optimized deps (fix #8593) (#8606) ([739175b](https://github.com/vitejs/vite/commit/739175b)), closes [#8593](https://github.com/vitejs/vite/issues/8593) [#8606](https://github.com/vitejs/vite/issues/8606)
* fix: sequential injection of tags in transformIndexHtml (#5851) (#6901) ([649c7f6](https://github.com/vitejs/vite/commit/649c7f6)), closes [#5851](https://github.com/vitejs/vite/issues/5851) [#6901](https://github.com/vitejs/vite/issues/6901)
* fix(asset): respect assetFileNames if rollupOptions.output is an array (#8561) ([4e6c26f](https://github.com/vitejs/vite/commit/4e6c26f)), closes [#8561](https://github.com/vitejs/vite/issues/8561)
* fix(css): escape pattern chars from base path in postcss dir-dependency messages (#7081) ([5151e74](https://github.com/vitejs/vite/commit/5151e74)), closes [#7081](https://github.com/vitejs/vite/issues/7081)
* fix(optimizer): browser mapping for yarn pnp (#6493) ([c1c7af3](https://github.com/vitejs/vite/commit/c1c7af3)), closes [#6493](https://github.com/vitejs/vite/issues/6493)
* fix: add missed JPEG file extensions to `KNOWN_ASSET_TYPES` (#8565) ([2dfc015](https://github.com/vitejs/vite/commit/2dfc015)), closes [#8565](https://github.com/vitejs/vite/issues/8565)
* fix: default export module transformation for vitest spy (#8567) ([d357e33](https://github.com/vitejs/vite/commit/d357e33)), closes [#8567](https://github.com/vitejs/vite/issues/8567)
* fix: default host to `localhost` instead of `127.0.0.1` (#8543) ([49c0896](https://github.com/vitejs/vite/commit/49c0896)), closes [#8543](https://github.com/vitejs/vite/issues/8543)
* fix: dont handle sigterm in middleware mode (#8550) ([c6f43dd](https://github.com/vitejs/vite/commit/c6f43dd)), closes [#8550](https://github.com/vitejs/vite/issues/8550)
* fix: mime missing extensions (#8568) ([acf3024](https://github.com/vitejs/vite/commit/acf3024)), closes [#8568](https://github.com/vitejs/vite/issues/8568)
* fix: objurl for type module, and concurrent tests (#8541) ([26ecd5a](https://github.com/vitejs/vite/commit/26ecd5a)), closes [#8541](https://github.com/vitejs/vite/issues/8541)
* fix: outdated optimized dep removed from module graph (#8533) ([3f4d22d](https://github.com/vitejs/vite/commit/3f4d22d)), closes [#8533](https://github.com/vitejs/vite/issues/8533)
* fix(config): only rewrite .js loader in `loadConfigFromBundledFile` (#8556) ([2548dd3](https://github.com/vitejs/vite/commit/2548dd3)), closes [#8556](https://github.com/vitejs/vite/issues/8556)
* fix(deps): update all non-major dependencies (#8558) ([9a1fd4c](https://github.com/vitejs/vite/commit/9a1fd4c)), closes [#8558](https://github.com/vitejs/vite/issues/8558)
* fix(ssr): dont replace rollup input (#7275) ([9a88afa](https://github.com/vitejs/vite/commit/9a88afa)), closes [#7275](https://github.com/vitejs/vite/issues/7275)
* fix: deps optimizer idle logic for workers (fix #8479) (#8511) ([1e05548](https://github.com/vitejs/vite/commit/1e05548)), closes [#8479](https://github.com/vitejs/vite/issues/8479) [#8511](https://github.com/vitejs/vite/issues/8511)
* fix: not match \n when injecting esbuild helpers (#8414) ([5a57626](https://github.com/vitejs/vite/commit/5a57626)), closes [#8414](https://github.com/vitejs/vite/issues/8414)
* fix: respect optimize deps entries (#8489) ([fba82d0](https://github.com/vitejs/vite/commit/fba82d0)), closes [#8489](https://github.com/vitejs/vite/issues/8489)
* fix(optimizer): encode `_` and `.` in different way (#8508) ([9065b37](https://github.com/vitejs/vite/commit/9065b37)), closes [#8508](https://github.com/vitejs/vite/issues/8508)
* fix(optimizer): external require-import conversion (fixes #2492, #3409) (#8459) ([1061bbd](https://github.com/vitejs/vite/commit/1061bbd)), closes [#2492](https://github.com/vitejs/vite/issues/2492) [#3409](https://github.com/vitejs/vite/issues/3409) [#8459](https://github.com/vitejs/vite/issues/8459)
* fix: make array `acornInjectPlugins` work (fixes #8410) (#8415) ([08d594b](https://github.com/vitejs/vite/commit/08d594b)), closes [#8410](https://github.com/vitejs/vite/issues/8410) [#8415](https://github.com/vitejs/vite/issues/8415)
* fix: SSR deep imports externalization (fixes #8420) (#8421) ([89d6711](https://github.com/vitejs/vite/commit/89d6711)), closes [#8420](https://github.com/vitejs/vite/issues/8420) [#8421](https://github.com/vitejs/vite/issues/8421)
* fix: `import.meta.accept()` -> `import.meta.hot.accept()` (#8361) ([c5185cf](https://github.com/vitejs/vite/commit/c5185cf)), closes [#8361](https://github.com/vitejs/vite/issues/8361)
* fix: return type of `handleHMRUpdate` (#8367) ([79d5ce1](https://github.com/vitejs/vite/commit/79d5ce1)), closes [#8367](https://github.com/vitejs/vite/issues/8367)
* fix: sourcemap source point to null (#8299) ([356b896](https://github.com/vitejs/vite/commit/356b896)), closes [#8299](https://github.com/vitejs/vite/issues/8299)
* fix: ssr-manifest no base (#8371) ([37eb5b3](https://github.com/vitejs/vite/commit/37eb5b3)), closes [#8371](https://github.com/vitejs/vite/issues/8371)
* fix(deps): update all non-major dependencies (#8391) ([842f995](https://github.com/vitejs/vite/commit/842f995)), closes [#8391](https://github.com/vitejs/vite/issues/8391)
* fix: preserve annotations during build deps optimization (#8358) ([334cd9f](https://github.com/vitejs/vite/commit/334cd9f)), closes [#8358](https://github.com/vitejs/vite/issues/8358)
* fix: missing types for `es-module-lexer` (fixes #8349) (#8352) ([df2cc3d](https://github.com/vitejs/vite/commit/df2cc3d)), closes [#8349](https://github.com/vitejs/vite/issues/8349) [#8352](https://github.com/vitejs/vite/issues/8352)
* fix(optimizer): transpile before calling `transformGlobImport` (#8343) ([1dbc7cc](https://github.com/vitejs/vite/commit/1dbc7cc)), closes [#8343](https://github.com/vitejs/vite/issues/8343)
* fix(deps): update all non-major dependencies (#8281) ([c68db4d](https://github.com/vitejs/vite/commit/c68db4d)), closes [#8281](https://github.com/vitejs/vite/issues/8281)
* fix: expose client dist in `exports` (#8324) ([689adc0](https://github.com/vitejs/vite/commit/689adc0)), closes [#8324](https://github.com/vitejs/vite/issues/8324)
* fix(cjs): build cjs for `loadEnv` (#8305) ([80dd2df](https://github.com/vitejs/vite/commit/80dd2df)), closes [#8305](https://github.com/vitejs/vite/issues/8305)
* fix: correctly replace process.env.NODE_ENV (#8283) ([ec52baa](https://github.com/vitejs/vite/commit/ec52baa)), closes [#8283](https://github.com/vitejs/vite/issues/8283)
* fix: dev sourcemap (#8269) ([505f75e](https://github.com/vitejs/vite/commit/505f75e)), closes [#8269](https://github.com/vitejs/vite/issues/8269)
* fix: glob types (#8257) ([03b227e](https://github.com/vitejs/vite/commit/03b227e)), closes [#8257](https://github.com/vitejs/vite/issues/8257)
* fix: srcset handling in html (#6419) ([a0ee4ff](https://github.com/vitejs/vite/commit/a0ee4ff)), closes [#6419](https://github.com/vitejs/vite/issues/6419)
* fix: support set NODE_ENV in scripts when custom mode option (#8218) ([adcf041](https://github.com/vitejs/vite/commit/adcf041)), closes [#8218](https://github.com/vitejs/vite/issues/8218)
* fix(hmr): catch thrown errors when connecting to hmr websocket (#7111) ([4bc9284](https://github.com/vitejs/vite/commit/4bc9284)), closes [#7111](https://github.com/vitejs/vite/issues/7111)
* fix(plugin-legacy): respect `entryFileNames` for polyfill chunks (#8247) ([baa9632](https://github.com/vitejs/vite/commit/baa9632)), closes [#8247](https://github.com/vitejs/vite/issues/8247)
* fix(plugin-react): broken optimized deps dir check (#8255) ([9e2a1ea](https://github.com/vitejs/vite/commit/9e2a1ea)), closes [#8255](https://github.com/vitejs/vite/issues/8255)
* fix!: do not fixStacktrace by default (#7995) ([23f8e08](https://github.com/vitejs/vite/commit/23f8e08)), closes [#7995](https://github.com/vitejs/vite/issues/7995)
* fix(glob): properly handles tailing comma (#8181) ([462be8e](https://github.com/vitejs/vite/commit/462be8e)), closes [#8181](https://github.com/vitejs/vite/issues/8181)
* fix: add hash to lib chunk names (#7190) ([c81cedf](https://github.com/vitejs/vite/commit/c81cedf)), closes [#7190](https://github.com/vitejs/vite/issues/7190)
* fix: allow css to be written for systemjs output (#5902) ([780b4f5](https://github.com/vitejs/vite/commit/780b4f5)), closes [#5902](https://github.com/vitejs/vite/issues/5902)
* fix: client full reload (#8018) ([2f478ed](https://github.com/vitejs/vite/commit/2f478ed)), closes [#8018](https://github.com/vitejs/vite/issues/8018)
* fix: handle optimize failure (#8006) ([ba95a2a](https://github.com/vitejs/vite/commit/ba95a2a)), closes [#8006](https://github.com/vitejs/vite/issues/8006)
* fix: increase default HTTPS dev server session memory limit (#6207) ([f895f94](https://github.com/vitejs/vite/commit/f895f94)), closes [#6207](https://github.com/vitejs/vite/issues/6207)
* fix: relative path html (#8122) ([d0deac0](https://github.com/vitejs/vite/commit/d0deac0)), closes [#8122](https://github.com/vitejs/vite/issues/8122)
* fix: Remove ssrError when invalidating a module (#8124) ([a543220](https://github.com/vitejs/vite/commit/a543220)), closes [#8124](https://github.com/vitejs/vite/issues/8124)
* fix: remove useless `/__vite_ping` handler (#8133) ([d607b2b](https://github.com/vitejs/vite/commit/d607b2b)), closes [#8133](https://github.com/vitejs/vite/issues/8133)
* fix: typo in #8121 (#8143) ([c32e3ac](https://github.com/vitejs/vite/commit/c32e3ac)), closes [#8121](https://github.com/vitejs/vite/issues/8121) [#8143](https://github.com/vitejs/vite/issues/8143)
* fix: use Vitest for unit testing, clean regex bug (#8040) ([63cd53d](https://github.com/vitejs/vite/commit/63cd53d)), closes [#8040](https://github.com/vitejs/vite/issues/8040)
* fix: Vite cannot load configuration files in the link directory (#4180) (#4181) ([a3fa1a3](https://github.com/vitejs/vite/commit/a3fa1a3)), closes [#4180](https://github.com/vitejs/vite/issues/4180) [#4181](https://github.com/vitejs/vite/issues/4181)
* fix: vite client types (#7877) ([0e67fe8](https://github.com/vitejs/vite/commit/0e67fe8)), closes [#7877](https://github.com/vitejs/vite/issues/7877)
* fix: warn for unresolved css in html (#7911) ([2b58cb3](https://github.com/vitejs/vite/commit/2b58cb3)), closes [#7911](https://github.com/vitejs/vite/issues/7911)
* fix(build): use crossorigin for module preloaded ([85cab70](https://github.com/vitejs/vite/commit/85cab70))
* fix(client): wait on the socket host, not the ping host (#6819) ([ae56e47](https://github.com/vitejs/vite/commit/ae56e47)), closes [#6819](https://github.com/vitejs/vite/issues/6819)
* fix(css): hoist external @import for non-split css (#8022) ([5280908](https://github.com/vitejs/vite/commit/5280908)), closes [#8022](https://github.com/vitejs/vite/issues/8022)
* fix(css): preserve dynamic import css code (fix #5348) (#7746) ([12d0cc0](https://github.com/vitejs/vite/commit/12d0cc0)), closes [#5348](https://github.com/vitejs/vite/issues/5348) [#7746](https://github.com/vitejs/vite/issues/7746)
* fix(glob): wrap glob compile output in function invocation (#3682) ([bb603d3](https://github.com/vitejs/vite/commit/bb603d3)), closes [#3682](https://github.com/vitejs/vite/issues/3682)
* fix(lib): enable inlineDynamicImports for umd and iife (#8126) ([272a252](https://github.com/vitejs/vite/commit/272a252)), closes [#8126](https://github.com/vitejs/vite/issues/8126)
* fix(lib): use proper extension (#6827) ([34df307](https://github.com/vitejs/vite/commit/34df307)), closes [#6827](https://github.com/vitejs/vite/issues/6827)
* fix(ssr): avoid transforming json file in ssrTransform (#6597) ([a709440](https://github.com/vitejs/vite/commit/a709440)), closes [#6597](https://github.com/vitejs/vite/issues/6597)
* fix(lib)!: remove format prefixes for cjs and esm (#8107) ([ad8c3b1](https://github.com/vitejs/vite/commit/ad8c3b1)), closes [#8107](https://github.com/vitejs/vite/issues/8107)


### Previous Changelogs


#### [3.0.0-beta.8](https://github.com/vitejs/vite/compare/v3.0.0-beta.7...v3.0.0-beta.8) (2022-07-08)

See [3.0.0-beta.8 changelog](https://github.com/vitejs/vite/blob/v3.0.0-beta.8/packages/vite/CHANGELOG.md)


#### [3.0.0-beta.7](https://github.com/vitejs/vite/compare/v3.0.0-beta.6...v3.0.0-beta.7) (2022-07-06)

See [3.0.0-beta.7 changelog](https://github.com/vitejs/vite/blob/v3.0.0-beta.7/packages/vite/CHANGELOG.md)


#### [3.0.0-beta.6](https://github.com/vitejs/vite/compare/v3.0.0-beta.5...v3.0.0-beta.6) (2022-07-04)

See [3.0.0-beta.6 changelog](https://github.com/vitejs/vite/blob/v3.0.0-beta.6/packages/vite/CHANGELOG.md)


#### [3.0.0-beta.5](https://github.com/vitejs/vite/compare/v3.0.0-beta.4...v3.0.0-beta.5) (2022-06-28)

See [3.0.0-beta.5 changelog](https://github.com/vitejs/vite/blob/v3.0.0-beta.5/packages/vite/CHANGELOG.md)


#### [3.0.0-beta.4](https://github.com/vitejs/vite/compare/v3.0.0-beta.3...v3.0.0-beta.4) (2022-06-27)

See [3.0.0-beta.4 changelog](https://github.com/vitejs/vite/blob/v3.0.0-beta.4/packages/vite/CHANGELOG.md)


#### [3.0.0-beta.3](https://github.com/vitejs/vite/compare/v3.0.0-beta.2...v3.0.0-beta.3) (2022-06-26)

See [3.0.0-beta.3 changelog](https://github.com/vitejs/vite/blob/v3.0.0-beta.3/packages/vite/CHANGELOG.md)


#### [3.0.0-beta.2](https://github.com/vitejs/vite/compare/v3.0.0-beta.1...v3.0.0-beta.2) (2022-06-24)

See [3.0.0-beta.2 changelog](https://github.com/vitejs/vite/blob/v3.0.0-beta.2/packages/vite/CHANGELOG.md)


#### [3.0.0-beta.1](https://github.com/vitejs/vite/compare/v3.0.0-beta.0...v3.0.0-beta.1) (2022-06-22)

See [3.0.0-beta.1 changelog](https://github.com/vitejs/vite/blob/v3.0.0-beta.1/packages/vite/CHANGELOG.md)


#### [3.0.0-beta.0](https://github.com/vitejs/vite/compare/v3.0.0-alpha.14...v3.0.0-beta.0) (2022-06-21)

See [3.0.0-beta.0 changelog](https://github.com/vitejs/vite/blob/v3.0.0-beta.0/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.14](https://github.com/vitejs/vite/compare/v3.0.0-alpha.13...v3.0.0-alpha.14) (2022-06-20)

See [3.0.0-alpha.14 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.14/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.13](https://github.com/vitejs/vite/compare/v3.0.0-alpha.12...v3.0.0-alpha.13) (2022-06-19)

See [3.0.0-alpha.13 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.13/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.12](https://github.com/vitejs/vite/compare/v3.0.0-alpha.11...v3.0.0-alpha.12) (2022-06-16)

See [3.0.0-alpha.12 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.12/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.11](https://github.com/vitejs/vite/compare/v3.0.0-alpha.10...v3.0.0-alpha.11) (2022-06-14)

See [3.0.0-alpha.11 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.11/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.10](https://github.com/vitejs/vite/compare/v3.0.0-alpha.9...v3.0.0-alpha.10) (2022-06-10)

See [3.0.0-alpha.10 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.10/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.9](https://github.com/vitejs/vite/compare/v3.0.0-alpha.8...v3.0.0-alpha.9) (2022-06-01)

See [3.0.0-alpha.9 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.9/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.8](https://github.com/vitejs/vite/compare/v3.0.0-alpha.7...v3.0.0-alpha.8) (2022-05-31)

See [3.0.0-alpha.8 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.8/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.7](https://github.com/vitejs/vite/compare/v3.0.0-alpha.6...v3.0.0-alpha.7) (2022-05-27)

See [3.0.0-alpha.7 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.7/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.6](https://github.com/vitejs/vite/compare/v3.0.0-alpha.5...v3.0.0-alpha.6) (2022-05-27)

See [3.0.0-alpha.6 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.6/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.5](https://github.com/vitejs/vite/compare/v3.0.0-alpha.4...v3.0.0-alpha.5) (2022-05-26)

See [3.0.0-alpha.5 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.5/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.4](https://github.com/vitejs/vite/compare/v3.0.0-alpha.3...v3.0.0-alpha.4) (2022-05-25)

See [3.0.0-alpha.4 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.4/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.3](https://github.com/vitejs/vite/compare/v3.0.0-alpha.2...v3.0.0-alpha.3) (2022-05-25)

See [3.0.0-alpha.3 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.3/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.2](https://github.com/vitejs/vite/compare/v3.0.0-alpha.1...v3.0.0-alpha.2) (2022-05-23)

See [3.0.0-alpha.2 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.2/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.1](https://github.com/vitejs/vite/compare/v3.0.0-alpha.0...v3.0.0-alpha.1) (2022-05-18)

See [3.0.0-alpha.1 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.1/packages/vite/CHANGELOG.md)


#### [3.0.0-alpha.0](https://github.com/vitejs/vite/compare/v2.9.12...v3.0.0-alpha.0) (2022-05-13)

See [3.0.0-alpha.0 changelog](https://github.com/vitejs/vite/blob/v3.0.0-alpha.0/packages/vite/CHANGELOG.md)



## <small>2.9.12 (2022-06-10)</small>

* fix: outdated optimized dep removed from module graph (#8534) ([c0d6c60](https://github.com/vitejs/vite/commit/c0d6c60)), closes [#8534](https://github.com/vitejs/vite/issues/8534)



## <small>2.9.11 (2022-06-10)</small>

* fix: respect server.headers in static middlewares (#8481) ([ab7dc1c](https://github.com/vitejs/vite/commit/ab7dc1c)), closes [#8481](https://github.com/vitejs/vite/issues/8481)
* fix(dev): avoid FOUC when swapping out link tag (fix #7973) (#8495) ([01fa807](https://github.com/vitejs/vite/commit/01fa807)), closes [#7973](https://github.com/vitejs/vite/issues/7973) [#8495](https://github.com/vitejs/vite/issues/8495)



## <small>2.9.10 (2022-06-06)</small>

* feat: treat Astro file scripts as TS (#8151) ([9fdd0a3](https://github.com/vitejs/vite/commit/9fdd0a3)), closes [#8151](https://github.com/vitejs/vite/issues/8151)
* feat: new hook `configurePreviewServer` (#7658) (#8437) ([7b972bc](https://github.com/vitejs/vite/commit/7b972bc)), closes [#7658](https://github.com/vitejs/vite/issues/7658) [#8437](https://github.com/vitejs/vite/issues/8437)
* fix: remove empty chunk css imports when using esnext (#8345) ([9fbc1a9](https://github.com/vitejs/vite/commit/9fbc1a9)), closes [#8345](https://github.com/vitejs/vite/issues/8345)
* fix: EPERM error on Windows when processing dependencies (#8235) ([dfe4307](https://github.com/vitejs/vite/commit/dfe4307)), closes [#8235](https://github.com/vitejs/vite/issues/8235)
* fix(css): remove `?used` hack (fixes #6421, #8245) (#8278) (#8471) ([8d7bac4](https://github.com/vitejs/vite/commit/8d7bac4)), closes [#6421](https://github.com/vitejs/vite/issues/6421) [#8245](https://github.com/vitejs/vite/issues/8245) [#8278](https://github.com/vitejs/vite/issues/8278) [#8471](https://github.com/vitejs/vite/issues/8471)
* chore(lint): sort for imports (#8113) ([4bd1531](https://github.com/vitejs/vite/commit/4bd1531)), closes [#8113](https://github.com/vitejs/vite/issues/8113)



## <small>2.9.9 (2022-05-11)</small>

* fix: add direct query to html-proxy css (fixes #8091) (#8094) ([a24b5e3](https://github.com/vitejs/vite/commit/a24b5e3)), closes [#8091](https://github.com/vitejs/vite/issues/8091) [#8094](https://github.com/vitejs/vite/issues/8094)
* fix: graceful rename in windows (#8036) ([84496f8](https://github.com/vitejs/vite/commit/84496f8)), closes [#8036](https://github.com/vitejs/vite/issues/8036)
* fix: image-set with base64 images (fix #8028) (#8035) ([992aee2](https://github.com/vitejs/vite/commit/992aee2)), closes [#8028](https://github.com/vitejs/vite/issues/8028) [#8035](https://github.com/vitejs/vite/issues/8035)
* fix: invalidate ssrError when HMR update occurs (#8052) ([22fa882](https://github.com/vitejs/vite/commit/22fa882)), closes [#8052](https://github.com/vitejs/vite/issues/8052)
* fix: use `strip-literal` to strip string lterals (#8054) ([b6fc3cd](https://github.com/vitejs/vite/commit/b6fc3cd)), closes [#8054](https://github.com/vitejs/vite/issues/8054)
* perf(lib): reduce backtrack when injecting esbuild helpers (#8110) ([e5556ab](https://github.com/vitejs/vite/commit/e5556ab)), closes [#8110](https://github.com/vitejs/vite/issues/8110)



## <small>2.9.8 (2022-05-04)</small>

* fix: inline js and css paths for virtual html (#7993) ([d49e3fb](https://github.com/vitejs/vite/commit/d49e3fb)), closes [#7993](https://github.com/vitejs/vite/issues/7993)
* fix: only handle merge ssr.noExternal (#8003) ([642d65b](https://github.com/vitejs/vite/commit/642d65b)), closes [#8003](https://github.com/vitejs/vite/issues/8003)
* fix: optimized processing folder renaming in win (fix #7939) (#8019) ([e5fe1c6](https://github.com/vitejs/vite/commit/e5fe1c6)), closes [#7939](https://github.com/vitejs/vite/issues/7939) [#8019](https://github.com/vitejs/vite/issues/8019)
* fix(css): do not clean id when passing to postcss (fix #7822) (#7827) ([72f17f8](https://github.com/vitejs/vite/commit/72f17f8)), closes [#7822](https://github.com/vitejs/vite/issues/7822) [#7827](https://github.com/vitejs/vite/issues/7827)
* fix(css): var in image-set (#7921) ([e96b908](https://github.com/vitejs/vite/commit/e96b908)), closes [#7921](https://github.com/vitejs/vite/issues/7921)
* fix(ssr): allow ssrTransform to parse hashbang (#8005) ([6420ba0](https://github.com/vitejs/vite/commit/6420ba0)), closes [#8005](https://github.com/vitejs/vite/issues/8005)
* feat: import ts with .js in vue (#7998) ([9974094](https://github.com/vitejs/vite/commit/9974094)), closes [#7998](https://github.com/vitejs/vite/issues/7998)
* chore: remove maybeVirtualHtmlSet (#8010) ([e85164e](https://github.com/vitejs/vite/commit/e85164e)), closes [#8010](https://github.com/vitejs/vite/issues/8010)



## <small>2.9.7 (2022-05-02)</small>

* chore: update license ([d58c030](https://github.com/vitejs/vite/commit/d58c030))
* chore(css): catch postcss config error (fix #2793) (#7934) ([7f535ac](https://github.com/vitejs/vite/commit/7f535ac)), closes [#2793](https://github.com/vitejs/vite/issues/2793) [#7934](https://github.com/vitejs/vite/issues/7934)
* chore(deps): update all non-major dependencies (#7949) ([b877d30](https://github.com/vitejs/vite/commit/b877d30)), closes [#7949](https://github.com/vitejs/vite/issues/7949)
* fix: inject esbuild helpers in IIFE and UMD wrappers (#7948) ([f7d2d71](https://github.com/vitejs/vite/commit/f7d2d71)), closes [#7948](https://github.com/vitejs/vite/issues/7948)
* fix: inline css hash (#7974) ([f6ae60d](https://github.com/vitejs/vite/commit/f6ae60d)), closes [#7974](https://github.com/vitejs/vite/issues/7974)
* fix: inline style hmr, transform style code inplace (#7869) ([a30a548](https://github.com/vitejs/vite/commit/a30a548)), closes [#7869](https://github.com/vitejs/vite/issues/7869)
* fix: use NODE_ENV in optimizer (#7673) ([50672e4](https://github.com/vitejs/vite/commit/50672e4)), closes [#7673](https://github.com/vitejs/vite/issues/7673)
* fix(css): clean comments before hoist at rules (#7924) ([e48827f](https://github.com/vitejs/vite/commit/e48827f)), closes [#7924](https://github.com/vitejs/vite/issues/7924)
* fix(css): dynamic import css in package fetches removed js (fixes #7955, #6823) (#7969) ([025eebf](https://github.com/vitejs/vite/commit/025eebf)), closes [#7955](https://github.com/vitejs/vite/issues/7955) [#6823](https://github.com/vitejs/vite/issues/6823) [#7969](https://github.com/vitejs/vite/issues/7969)
* fix(css): inline css module when ssr, minify issue (fix #5471) (#7807) ([cf8a48a](https://github.com/vitejs/vite/commit/cf8a48a)), closes [#5471](https://github.com/vitejs/vite/issues/5471) [#7807](https://github.com/vitejs/vite/issues/7807)
* fix(css): sourcemap crash with postcss (#7982) ([7f9f8f1](https://github.com/vitejs/vite/commit/7f9f8f1)), closes [#7982](https://github.com/vitejs/vite/issues/7982)
* fix(css): support postcss.config.ts (#7935) ([274c10e](https://github.com/vitejs/vite/commit/274c10e)), closes [#7935](https://github.com/vitejs/vite/issues/7935)
* fix(ssr): failed ssrLoadModule call throws same error (#7177) ([891e7fc](https://github.com/vitejs/vite/commit/891e7fc)), closes [#7177](https://github.com/vitejs/vite/issues/7177)
* fix(worker): import.meta.* (#7706) ([b092697](https://github.com/vitejs/vite/commit/b092697)), closes [#7706](https://github.com/vitejs/vite/issues/7706)
* docs: `server.origin` config trailing slash (fix #6622) (#7865) ([5c1ee5a](https://github.com/vitejs/vite/commit/5c1ee5a)), closes [#6622](https://github.com/vitejs/vite/issues/6622) [#7865](https://github.com/vitejs/vite/issues/7865)



## <small>2.9.6 (2022-04-26)</small>

* fix: `apply` condition skipped for nested plugins (#7741) ([1f2ca53](https://github.com/vitejs/vite/commit/1f2ca53)), closes [#7741](https://github.com/vitejs/vite/issues/7741)
* fix: clean string regexp (#7871) ([ecc78bc](https://github.com/vitejs/vite/commit/ecc78bc)), closes [#7871](https://github.com/vitejs/vite/issues/7871)
* fix: escape character in string regexp match (#7834) ([1d468c8](https://github.com/vitejs/vite/commit/1d468c8)), closes [#7834](https://github.com/vitejs/vite/issues/7834)
* fix: HMR propagation of HTML changes (fix #7870) (#7895) ([1f7855c](https://github.com/vitejs/vite/commit/1f7855c)), closes [#7870](https://github.com/vitejs/vite/issues/7870) [#7895](https://github.com/vitejs/vite/issues/7895)
* fix: modulepreload polyfill only during build (fix #4786) (#7816) ([709776f](https://github.com/vitejs/vite/commit/709776f)), closes [#4786](https://github.com/vitejs/vite/issues/4786) [#7816](https://github.com/vitejs/vite/issues/7816)
* fix: new SharedWorker syntax (#7800) ([474d5c2](https://github.com/vitejs/vite/commit/474d5c2)), closes [#7800](https://github.com/vitejs/vite/issues/7800)
* fix: node v18 support (#7812) ([fc89057](https://github.com/vitejs/vite/commit/fc89057)), closes [#7812](https://github.com/vitejs/vite/issues/7812)
* fix: preview jsdoc params (#7903) ([e474381](https://github.com/vitejs/vite/commit/e474381)), closes [#7903](https://github.com/vitejs/vite/issues/7903)
* fix: replace import.meta.url correctly (#7792) ([12d1194](https://github.com/vitejs/vite/commit/12d1194)), closes [#7792](https://github.com/vitejs/vite/issues/7792)
* fix: set `isSelfAccepting` to `false` for any asset not processed by importAnalysis (#7898) ([0d2089c](https://github.com/vitejs/vite/commit/0d2089c)), closes [#7898](https://github.com/vitejs/vite/issues/7898)
* fix: spelling mistakes (#7883) ([54728e3](https://github.com/vitejs/vite/commit/54728e3)), closes [#7883](https://github.com/vitejs/vite/issues/7883)
* fix: ssr.noExternal with boolean values (#7813) ([0b2d307](https://github.com/vitejs/vite/commit/0b2d307)), closes [#7813](https://github.com/vitejs/vite/issues/7813)
* fix: style use string instead of js import (#7786) ([ba43c29](https://github.com/vitejs/vite/commit/ba43c29)), closes [#7786](https://github.com/vitejs/vite/issues/7786)
* fix: update sourcemap in importAnalysisBuild (#7825) ([d7540c8](https://github.com/vitejs/vite/commit/d7540c8)), closes [#7825](https://github.com/vitejs/vite/issues/7825)
* fix(ssr): rewrite dynamic class method name (fix #7751) (#7757) ([b89974a](https://github.com/vitejs/vite/commit/b89974a)), closes [#7751](https://github.com/vitejs/vite/issues/7751) [#7757](https://github.com/vitejs/vite/issues/7757)
* chore: code structure (#7790) ([5f7fe00](https://github.com/vitejs/vite/commit/5f7fe00)), closes [#7790](https://github.com/vitejs/vite/issues/7790)
* chore: fix worker sourcemap output style (#7805) ([17f3be7](https://github.com/vitejs/vite/commit/17f3be7)), closes [#7805](https://github.com/vitejs/vite/issues/7805)
* chore(deps): update all non-major dependencies (#7780) ([eba9d05](https://github.com/vitejs/vite/commit/eba9d05)), closes [#7780](https://github.com/vitejs/vite/issues/7780)
* chore(deps): update all non-major dependencies (#7847) ([e29d1d9](https://github.com/vitejs/vite/commit/e29d1d9)), closes [#7847](https://github.com/vitejs/vite/issues/7847)
* feat: enable optimizeDeps.esbuildOptions.loader (#6840) ([af8ca60](https://github.com/vitejs/vite/commit/af8ca60)), closes [#6840](https://github.com/vitejs/vite/issues/6840)



## <small>2.9.5 (2022-04-14)</small>

* fix: revert #7582, fix #7721 and #7736 (#7737) ([fa86d69](https://github.com/vitejs/vite/commit/fa86d69)), closes [#7721](https://github.com/vitejs/vite/issues/7721) [#7736](https://github.com/vitejs/vite/issues/7736) [#7737](https://github.com/vitejs/vite/issues/7737)
* chore: format css minify esbuild error (#7731) ([c445075](https://github.com/vitejs/vite/commit/c445075)), closes [#7731](https://github.com/vitejs/vite/issues/7731)



## <small>2.9.4 (2022-04-13)</small>

* fix: handle url imports with semicolon (fix #7717) (#7718) ([a5c2a78](https://github.com/vitejs/vite/commit/a5c2a78)), closes [#7717](https://github.com/vitejs/vite/issues/7717) [#7718](https://github.com/vitejs/vite/issues/7718)



## <small>2.9.3 (2022-04-13)</small>

* fix: revert #7665 (#7716) ([26862c4](https://github.com/vitejs/vite/commit/26862c4)), closes [#7665](https://github.com/vitejs/vite/issues/7665) [#7716](https://github.com/vitejs/vite/issues/7716)



## <small>2.9.2 (2022-04-13)</small>

* fix: `$ vite preview` 404 handling (#7665) ([66b6dc5](https://github.com/vitejs/vite/commit/66b6dc5)), closes [#7665](https://github.com/vitejs/vite/issues/7665)
* fix: build should also respect esbuild=false config (#7602) ([2dc0e80](https://github.com/vitejs/vite/commit/2dc0e80)), closes [#7602](https://github.com/vitejs/vite/issues/7602)
* fix: default value of assetsDir option (#7703) ([83d32d9](https://github.com/vitejs/vite/commit/83d32d9)), closes [#7703](https://github.com/vitejs/vite/issues/7703)
* fix: detect env hmr (#7595) ([212d454](https://github.com/vitejs/vite/commit/212d454)), closes [#7595](https://github.com/vitejs/vite/issues/7595)
* fix: EACCES permission denied due to resolve new paths default (#7612) ([1dd019f](https://github.com/vitejs/vite/commit/1dd019f)), closes [#7612](https://github.com/vitejs/vite/issues/7612)
* fix: fix HMR propagation when imports not analyzed (#7561) ([57e7914](https://github.com/vitejs/vite/commit/57e7914)), closes [#7561](https://github.com/vitejs/vite/issues/7561)
* fix: nested comments and strings, new regexp utils (#7650) ([93900f0](https://github.com/vitejs/vite/commit/93900f0)), closes [#7650](https://github.com/vitejs/vite/issues/7650)
* fix: revert optimizeDeps false, keep optimizedDeps.disabled (#7715) ([ba9a1ff](https://github.com/vitejs/vite/commit/ba9a1ff)), closes [#7715](https://github.com/vitejs/vite/issues/7715)
* fix: update watch mode (#7132) ([9ed1672](https://github.com/vitejs/vite/commit/9ed1672)), closes [#7132](https://github.com/vitejs/vite/issues/7132)
* fix: update ws types (#7605) ([b620587](https://github.com/vitejs/vite/commit/b620587)), closes [#7605](https://github.com/vitejs/vite/issues/7605)
* fix: use correct proxy config in preview (#7604) ([cf59005](https://github.com/vitejs/vite/commit/cf59005)), closes [#7604](https://github.com/vitejs/vite/issues/7604)
* fix(css): hoist charset (#7678) ([29e622c](https://github.com/vitejs/vite/commit/29e622c)), closes [#7678](https://github.com/vitejs/vite/issues/7678)
* fix(css): include inline css module in bundle (#7591) ([45b9273](https://github.com/vitejs/vite/commit/45b9273)), closes [#7591](https://github.com/vitejs/vite/issues/7591)
* fix(deps): update all non-major dependencies (#7668) ([485263c](https://github.com/vitejs/vite/commit/485263c)), closes [#7668](https://github.com/vitejs/vite/issues/7668)
* fix(less): handles rewriting relative paths passed Less's `data-uri` function. (#7400) ([08e39b7](https://github.com/vitejs/vite/commit/08e39b7)), closes [#7400](https://github.com/vitejs/vite/issues/7400)
* fix(resolver): skip known ESM entries when resolving a `require` call  (#7582) ([5d6ea8e](https://github.com/vitejs/vite/commit/5d6ea8e)), closes [#7582](https://github.com/vitejs/vite/issues/7582)
* fix(ssr): properly transform export default with expressions (#7705) ([d6830e3](https://github.com/vitejs/vite/commit/d6830e3)), closes [#7705](https://github.com/vitejs/vite/issues/7705)
* feat: clean string module lex string template (#7667) ([dfce283](https://github.com/vitejs/vite/commit/dfce283)), closes [#7667](https://github.com/vitejs/vite/issues/7667)
* feat: explicit the word boundary (#6876) ([7ddbf96](https://github.com/vitejs/vite/commit/7ddbf96)), closes [#6876](https://github.com/vitejs/vite/issues/6876)
* feat: optimizeDeps.disabled (#7646) ([48e038c](https://github.com/vitejs/vite/commit/48e038c)), closes [#7646](https://github.com/vitejs/vite/issues/7646)
* chore: fix term cases (#7553) ([c296130](https://github.com/vitejs/vite/commit/c296130)), closes [#7553](https://github.com/vitejs/vite/issues/7553)
* chore: revert removed line in #7698 ([7e6a2c8](https://github.com/vitejs/vite/commit/7e6a2c8)), closes [#7698](https://github.com/vitejs/vite/issues/7698)
* chore: type unknown env as any (#7702) ([23fdef1](https://github.com/vitejs/vite/commit/23fdef1)), closes [#7702](https://github.com/vitejs/vite/issues/7702)
* chore(deps): update all non-major dependencies (#7603) ([fc51a15](https://github.com/vitejs/vite/commit/fc51a15)), closes [#7603](https://github.com/vitejs/vite/issues/7603)
* perf(css): hoist at rules with regex (#7691) ([8858180](https://github.com/vitejs/vite/commit/8858180)), closes [#7691](https://github.com/vitejs/vite/issues/7691)
* refactor: esbuild handles `target` and `useDefineForClassFields` (#7698) ([0c928aa](https://github.com/vitejs/vite/commit/0c928aa)), closes [#7698](https://github.com/vitejs/vite/issues/7698)
* docs: update release notes (#7563) ([a74bd7b](https://github.com/vitejs/vite/commit/a74bd7b)), closes [#7563](https://github.com/vitejs/vite/issues/7563)



## <small>2.9.1 (2022-03-31)</small>

* fix: allow port 0 to be provided to server (#7530) ([173e4c9](https://github.com/vitejs/vite/commit/173e4c9)), closes [#7530](https://github.com/vitejs/vite/issues/7530)
* fix: brotli let for reassignment (#7544) ([d0253d7](https://github.com/vitejs/vite/commit/d0253d7)), closes [#7544](https://github.com/vitejs/vite/issues/7544)
* fix: dynamic import warning with @vite-ignore (#7533) ([29c1ec0](https://github.com/vitejs/vite/commit/29c1ec0)), closes [#7533](https://github.com/vitejs/vite/issues/7533)
* fix: remove unneeded skipping optimization log (#7531) ([41fa2f5](https://github.com/vitejs/vite/commit/41fa2f5)), closes [#7531](https://github.com/vitejs/vite/issues/7531)
* docs(changelog): fix raw glob imports syntax (#7540) ([87fbe13](https://github.com/vitejs/vite/commit/87fbe13)), closes [#7540](https://github.com/vitejs/vite/issues/7540)
* chore: 2.9 release notes (#7525) ([4324f48](https://github.com/vitejs/vite/commit/4324f48)), closes [#7525](https://github.com/vitejs/vite/issues/7525)



# [2.9.0](https://github.com/vitejs/vite/compare/v2.8.6...v2.9.0) (2022-03-30)

### Faster Cold Start

Before 2.9, the first time dev was run on a project Vite needed to perform a scan phase to discover dependencies and then pre-bundle them before starting the server. In 2.9 both scanning [#7379](https://github.com/vitejs/vite/issues/7379) and pre-bundling [#6758](https://github.com/vitejs/vite/issues/6758) of dependencies are now non-blocking, so the server starts right away during cold start. We also now allow requests to flow through the pipeline improving initial cold start load speed and increasing the chances of discovering new missing dependencies when re-processing and letting Vite populate the module graph and the browser to process files. In many cases, there is also no need to full-reload the page when new dependencies are discovered.

### CSS Sourcemap support during dev (experimental)

Vite now supports CSS sourcemaps [#7173](https://github.com/vitejs/vite/issues/7173). This feature is still experimental, and it is disabled by default to avoid incurring a performance penalty for users that don't need it. To enable it, set [css.devSourcemap](https://vitejs.dev/config/#css-devsourcemap) to `true`.

### Avoid splitting vendor chunks by default

Vite's default chunking strategy was a good fit for most SPAs, but it wasn't ideal in some other use cases. Vite doesn't have enough context to make the best decision here, so in Vite 2.9 the previous chunking strategy is now [opt-in](https://vitejs.dev/guide/build.html#chunking-strategy) [#6534](https://github.com/vitejs/vite/issues/6534) and Vite will no longer split vendor libs in a separate chunk.

### Web Workers enhancements

Web Workers now supports source map generation (see [#5417](https://github.com/vitejs/vite/issues/5417)). The implementation is also now more robust, fixing several issues encountered in previous versions ([#6599](https://github.com/vitejs/vite/issues/6599)).

### Raw Glob Imports

Glob imports support for the `raw` modifier syntax has changed to using `{ as: 'raw' }`, which works in the same way as the `?raw` suffix in regular imports:

```js
const examples = import.meta.globEager('./examples/*.html', { as: 'raw' })
```

The `{ assert: { type: 'raw' }}` syntax introduced in v2.8 has been deprecated. See [#7017](https://github.com/vitejs/vite/issues/7017) for more information.

### `envDir` changes

The `envDir` now correctly loads `.env` files in the specified directory only (defaults to `root`). Previously, it would load files above the directory, which imposed security issues. If you had relied on the previous behaviour, make sure you move your `.env` files to the correct directory, or configure the `envDir` option.

### New tools for Plugin and Framework Authors

#### Client Server Communication API

Vite now provides utilities for plugins to help handle the communication with clients connected to Vite's server [#7437](https://github.com/vitejs/vite/issues/7437). Reusing the open WebSocket connection between the server and clients several use cases can be simplified ([vite-plugin-inspect](https://github.com/antfu/vite-plugin-inspect), [SliDev](https://sli.dev), and many others). Check out the [Client Server Communication docs](https://vitejs.dev/guide/api-plugin.html#client-server-communication) for more information.

```js
// Send a message from the client to the server
if (import.meta.hot) {
  import.meta.hot.send('my:from-client', { msg: 'Hey!' })
}
```

```js
// And listen to client messages in a plugin
  configureServer(server) {
    server.ws.on('my:from-client', (data, client) => {
      console.log('Message from client:', data.msg) // Hey!
      // ...
    })
  }
```

#### `importedCss` and `importedAssets` to RenderedChunk type

Replace the internal `chunkToEmittedCssFileMap` and `chunkToEmittedAssetsMap` variables with public properties added by Vite to `RenderedChunk` objects in the `renderChunk` phase. These is useful for Vite-based frameworks that generate their own HTML. See [#6629](https://github.com/vitejs/vite/issues/6629).

#### Optimize Custom Extensions (experimental)

A new `optimizeDeps.extensions: string[]` option is available to enable pre-bundling of custom extensions. A respective esbuild plugin is required to handle that extension. e.g. `['.svelte', '.svelte.md']`. See [#6801](https://github.com/vitejs/vite/issues/6801) for more information.


### Bug Fixes

* fix: build path error on Windows (#7383) ([e3c7c7a](https://github.com/vitejs/vite/commit/e3c7c7a)), closes [#7383](https://github.com/vitejs/vite/issues/7383)
* fix: import url worker two times (#7468) ([f05a813](https://github.com/vitejs/vite/commit/f05a813)), closes [#7468](https://github.com/vitejs/vite/issues/7468)
* fix: import with query with exports/browser field (#7098) ([9ce6732](https://github.com/vitejs/vite/commit/9ce6732)), closes [#7098](https://github.com/vitejs/vite/issues/7098)
* fix: make @fs URLs work with special characters (#7510) ([2b7dad1](https://github.com/vitejs/vite/commit/2b7dad1)), closes [#7510](https://github.com/vitejs/vite/issues/7510)
* fix: tailwind css sourcemap warning (#7480) ([90df0bb](https://github.com/vitejs/vite/commit/90df0bb)), closes [#7480](https://github.com/vitejs/vite/issues/7480)
* fix: worker match only run in js (#7500) ([9481c7d](https://github.com/vitejs/vite/commit/9481c7d)), closes [#7500](https://github.com/vitejs/vite/issues/7500)
* fix: Correctly process urls when they are rewritten to contain space (#7452) ([9ee2cf6](https://github.com/vitejs/vite/commit/9ee2cf6)), closes [#7452](https://github.com/vitejs/vite/issues/7452)
* fix: custom event payload type (#7498) ([28b0660](https://github.com/vitejs/vite/commit/28b0660)), closes [#7498](https://github.com/vitejs/vite/issues/7498)
* fix: handle relative path glob raw import, fix #7307 (#7371) ([7f8dc58](https://github.com/vitejs/vite/commit/7f8dc58)), closes [#7307](https://github.com/vitejs/vite/issues/7307) [#7371](https://github.com/vitejs/vite/issues/7371)
* fix: import.meta.url in worker (#7464) ([8ac4b12](https://github.com/vitejs/vite/commit/8ac4b12)), closes [#7464](https://github.com/vitejs/vite/issues/7464)
* fix: optimizeDeps.entries default ignore paths (#7469) ([4c95e99](https://github.com/vitejs/vite/commit/4c95e99)), closes [#7469](https://github.com/vitejs/vite/issues/7469)
* fix: errors in worker handling (#7236) ([77dc1a1](https://github.com/vitejs/vite/commit/77dc1a1)), closes [#7236](https://github.com/vitejs/vite/issues/7236)
* fix: consider undefined port when checking port (#7318) ([c7fc7c3](https://github.com/vitejs/vite/commit/c7fc7c3)), closes [#7318](https://github.com/vitejs/vite/issues/7318)
* fix: inline style css sourcemap (#7434) ([47668b5](https://github.com/vitejs/vite/commit/47668b5)), closes [#7434](https://github.com/vitejs/vite/issues/7434)
* fix: sourcemap missing source files warning with cached vue (#7442) ([a2ce20d](https://github.com/vitejs/vite/commit/a2ce20d)), closes [#7442](https://github.com/vitejs/vite/issues/7442)
* fix: update tsconfck to 1.2.1 (#7424) ([a90b03b](https://github.com/vitejs/vite/commit/a90b03b)), closes [#7424](https://github.com/vitejs/vite/issues/7424)
* fix: virtual html sourcemap warning (#7440) ([476786b](https://github.com/vitejs/vite/commit/476786b)), closes [#7440](https://github.com/vitejs/vite/issues/7440)
* fix(less): empty less file error (#7412) ([0535c70](https://github.com/vitejs/vite/commit/0535c70)), closes [#7412](https://github.com/vitejs/vite/issues/7412)
* fix(resolve): skip `module` field when the importer is a `require` call (#7438) ([fe4c1ed](https://github.com/vitejs/vite/commit/fe4c1ed)), closes [#7438](https://github.com/vitejs/vite/issues/7438)
* fix: avoid mangling code from incorrect magic-string usage (#7397) ([68d76c9](https://github.com/vitejs/vite/commit/68d76c9)), closes [#7397](https://github.com/vitejs/vite/issues/7397)
* fix(config): server restart on config dependencies changed on windows (#7366) ([c43467a](https://github.com/vitejs/vite/commit/c43467a)), closes [#7366](https://github.com/vitejs/vite/issues/7366)
* fix(deps): update all non-major dependencies (#7392) ([b63fc3b](https://github.com/vitejs/vite/commit/b63fc3b)), closes [#7392](https://github.com/vitejs/vite/issues/7392)
* fix: add version to optimized chunks, fix #7323 (#7350) ([1be1db6](https://github.com/vitejs/vite/commit/1be1db6)), closes [#7323](https://github.com/vitejs/vite/issues/7323) [#7350](https://github.com/vitejs/vite/issues/7350)
* fix: browser cache of newly discovered deps (#7378) ([392a0de](https://github.com/vitejs/vite/commit/392a0de)), closes [#7378](https://github.com/vitejs/vite/issues/7378)
* fix: do not warn (about not being able to bundle non module scripts) when src is an external url (#7 ([0646fe8](https://github.com/vitejs/vite/commit/0646fe8)), closes [#7380](https://github.com/vitejs/vite/issues/7380)
* fix: overwrite deps info browserHash only on commit (#7359) ([1e9615d](https://github.com/vitejs/vite/commit/1e9615d)), closes [#7359](https://github.com/vitejs/vite/issues/7359)
* fix: delayed full page reload (#7347) ([fa0820a](https://github.com/vitejs/vite/commit/fa0820a)), closes [#7347](https://github.com/vitejs/vite/issues/7347)
* fix: early discovery of missing deps, fix #7333 (#7346) ([7d2f37c](https://github.com/vitejs/vite/commit/7d2f37c)), closes [#7333](https://github.com/vitejs/vite/issues/7333) [#7346](https://github.com/vitejs/vite/issues/7346)
* fix: unhandled exception on eager transformRequest (#7345) ([c3260a4](https://github.com/vitejs/vite/commit/c3260a4)), closes [#7345](https://github.com/vitejs/vite/issues/7345)
* fix: update to esbuild 0.14.27, fix #6994 (#7320) ([65aaeee](https://github.com/vitejs/vite/commit/65aaeee)), closes [#6994](https://github.com/vitejs/vite/issues/6994) [#7320](https://github.com/vitejs/vite/issues/7320)
* fix: `ssrExternal` should not skip nested dependencies (#7154) ([f8f934a](https://github.com/vitejs/vite/commit/f8f934a)), closes [#7154](https://github.com/vitejs/vite/issues/7154)
* fix: dep with dynamic import wrong error log (#7313) ([769f535](https://github.com/vitejs/vite/commit/769f535)), closes [#7313](https://github.com/vitejs/vite/issues/7313)
* fix: avoid caching transform result of invalidated module (#7254) ([2d7ba72](https://github.com/vitejs/vite/commit/2d7ba72)), closes [#7254](https://github.com/vitejs/vite/issues/7254)
* fix: dont replace define in json (#7294) ([fc5c937](https://github.com/vitejs/vite/commit/fc5c937)), closes [#7294](https://github.com/vitejs/vite/issues/7294)
* fix: main browserHash after stable optimization rerun (#7284) ([98eefa8](https://github.com/vitejs/vite/commit/98eefa8)), closes [#7284](https://github.com/vitejs/vite/issues/7284)
* fix: needs es interop check for newly discovered deps (#7243) ([ba3047d](https://github.com/vitejs/vite/commit/ba3047d)), closes [#7243](https://github.com/vitejs/vite/issues/7243)
* fix: pending requests after module invalidation (#7283) ([a1044d7](https://github.com/vitejs/vite/commit/a1044d7)), closes [#7283](https://github.com/vitejs/vite/issues/7283)
* fix: use browserHash for imports from node_modules (#7278) ([161f8ea](https://github.com/vitejs/vite/commit/161f8ea)), closes [#7278](https://github.com/vitejs/vite/issues/7278)
* fix: use hmr port if specified (#7282) ([3ee04c0](https://github.com/vitejs/vite/commit/3ee04c0)), closes [#7282](https://github.com/vitejs/vite/issues/7282)
* fix: use relative paths in _metadata.json (#7299) ([8b945f5](https://github.com/vitejs/vite/commit/8b945f5)), closes [#7299](https://github.com/vitejs/vite/issues/7299)
* fix(asset): allow non-existent url (#7306) ([6bc45a2](https://github.com/vitejs/vite/commit/6bc45a2)), closes [#7306](https://github.com/vitejs/vite/issues/7306)
* fix(hmr): hmr style tag no support in html (#7262) ([fae120a](https://github.com/vitejs/vite/commit/fae120a)), closes [#7262](https://github.com/vitejs/vite/issues/7262)
* fix: `import.meta.url` should not throw (#7219) ([5de3a98](https://github.com/vitejs/vite/commit/5de3a98)), closes [#7219](https://github.com/vitejs/vite/issues/7219)
* fix: allow `localhost` as a valid hostname (#7092) ([4194cce](https://github.com/vitejs/vite/commit/4194cce)), closes [#7092](https://github.com/vitejs/vite/issues/7092)
* fix: build optimize deps metada location (#7214) ([dc46adf](https://github.com/vitejs/vite/commit/dc46adf)), closes [#7214](https://github.com/vitejs/vite/issues/7214)
* fix: define plugin not ignore file names (#6340) ([7215a03](https://github.com/vitejs/vite/commit/7215a03)), closes [#6340](https://github.com/vitejs/vite/issues/6340)
* fix: deprecate `{ assert: { type: raw }}` in favor of `{ as: raw }` (fix #7017) (#7215) ([87ecce5](https://github.com/vitejs/vite/commit/87ecce5)), closes [#7017](https://github.com/vitejs/vite/issues/7017) [#7215](https://github.com/vitejs/vite/issues/7215)
* fix: execute classic worker in dev mode (#7099) ([3c0a609](https://github.com/vitejs/vite/commit/3c0a609)), closes [#7099](https://github.com/vitejs/vite/issues/7099)
* fix: handle files with multiple comments (#7202) ([3f5b645](https://github.com/vitejs/vite/commit/3f5b645)), closes [#7202](https://github.com/vitejs/vite/issues/7202)
* fix: honor the host param when creating a websocket server (#5617) ([882c8a8](https://github.com/vitejs/vite/commit/882c8a8)), closes [#5617](https://github.com/vitejs/vite/issues/5617)
* fix: import css in less/scss (fix 3293) (#7147) ([9b51a3a](https://github.com/vitejs/vite/commit/9b51a3a)), closes [#7147](https://github.com/vitejs/vite/issues/7147)
* fix: optimizeDeps.include missing in known imports fallback (#7218) ([6c08c86](https://github.com/vitejs/vite/commit/6c08c86)), closes [#7218](https://github.com/vitejs/vite/issues/7218)
* fix: prevent loading env outside of root (#6995) ([e0a4d81](https://github.com/vitejs/vite/commit/e0a4d81)), closes [#6995](https://github.com/vitejs/vite/issues/6995)
* fix: reoptimize deps on esbuild options change (#6855) ([4517c2b](https://github.com/vitejs/vite/commit/4517c2b)), closes [#6855](https://github.com/vitejs/vite/issues/6855)
* fix: replacing compression with modern version (#6557) ([5648d09](https://github.com/vitejs/vite/commit/5648d09)), closes [#6557](https://github.com/vitejs/vite/issues/6557)
* fix: restart optimize (#7004) ([47fbe29](https://github.com/vitejs/vite/commit/47fbe29)), closes [#7004](https://github.com/vitejs/vite/issues/7004)
* fix: reusing variable names in html module scripts (fix #6851) (#6818) ([c46b56d](https://github.com/vitejs/vite/commit/c46b56d)), closes [#6851](https://github.com/vitejs/vite/issues/6851) [#6818](https://github.com/vitejs/vite/issues/6818)
* fix: revert #6340, definePlugin tests, warning box (#7174) ([6cb0647](https://github.com/vitejs/vite/commit/6cb0647)), closes [#6340](https://github.com/vitejs/vite/issues/6340) [#7174](https://github.com/vitejs/vite/issues/7174)
* fix: update postcss-load-config to load PostCSS plugins based on their config file path (#6856) ([f02f961](https://github.com/vitejs/vite/commit/f02f961)), closes [#6856](https://github.com/vitejs/vite/issues/6856)
* fix(hmr): client pinging behind a proxy on websocket disconnect (fix #4501) (#5466) ([96573db](https://github.com/vitejs/vite/commit/96573db)), closes [#4501](https://github.com/vitejs/vite/issues/4501) [#5466](https://github.com/vitejs/vite/issues/5466)
* fix(html): build mode ignore html define transform (#6663) ([79dd003](https://github.com/vitejs/vite/commit/79dd003)), closes [#6663](https://github.com/vitejs/vite/issues/6663)
* fix(json): load json module error (#6352) ([c8a7ea8](https://github.com/vitejs/vite/commit/c8a7ea8)), closes [#6352](https://github.com/vitejs/vite/issues/6352)
* fix(optimizer): add missing keys to hash (#7189) ([b0c0efe](https://github.com/vitejs/vite/commit/b0c0efe)), closes [#7189](https://github.com/vitejs/vite/issues/7189)
* fix(resolve): try .tsx extension for .js import from typescript module (#7005) ([72b8cb6](https://github.com/vitejs/vite/commit/72b8cb6)), closes [#7005](https://github.com/vitejs/vite/issues/7005)
* fix(server): base middleware redirect with search and hash (#6574) ([a516e85](https://github.com/vitejs/vite/commit/a516e85)), closes [#6574](https://github.com/vitejs/vite/issues/6574)
* fix(server): ensure consistency for url to file mapping in importAnalysis and static middleware (#65 ([b214115](https://github.com/vitejs/vite/commit/b214115)), closes [#6518](https://github.com/vitejs/vite/issues/6518)
* fix(ssr): bypass missing resolve error in SSR (#7164) ([a4927c5](https://github.com/vitejs/vite/commit/a4927c5)), closes [#7164](https://github.com/vitejs/vite/issues/7164)


### Features

* feat(worker): Add sourcemap support for worker bundles (#5417) ([465b6b9](https://github.com/vitejs/vite/commit/465b6b9)), closes [#5417](https://github.com/vitejs/vite/issues/5417)
* feat(type): support typing for custom events (#7476) ([50a8765](https://github.com/vitejs/vite/commit/50a8765)), closes [#7476](https://github.com/vitejs/vite/issues/7476)
* refactor(types): share hot context type (#7475) ([64ddff0](https://github.com/vitejs/vite/commit/64ddff0)), closes [#7475](https://github.com/vitejs/vite/issues/7475)
* feat: support importing css with ?raw (#5796) ([fedb106](https://github.com/vitejs/vite/commit/fedb106)), closes [#5796](https://github.com/vitejs/vite/issues/5796)
* feat(css): css.devSourcemap option (#7471) ([57f14cb](https://github.com/vitejs/vite/commit/57f14cb)), closes [#7471](https://github.com/vitejs/vite/issues/7471)
* feat(dev): expose APIs for client-server communication (#7437) ([e29ea8e](https://github.com/vitejs/vite/commit/e29ea8e)), closes [#7437](https://github.com/vitejs/vite/issues/7437)
* feat: hide optimized deps found during scan phase logs (#7419) ([f4934e8](https://github.com/vitejs/vite/commit/f4934e8)), closes [#7419](https://github.com/vitejs/vite/issues/7419)
* feat: non-blocking scanning of dependencies (#7379) ([676f545](https://github.com/vitejs/vite/commit/676f545)), closes [#7379](https://github.com/vitejs/vite/issues/7379)
* feat: css sourcemap support during dev (#7173) ([38a655f](https://github.com/vitejs/vite/commit/38a655f)), closes [#7173](https://github.com/vitejs/vite/issues/7173)
* feat: expose ssrRewriteStacktrace (#7091) ([d4ae45d](https://github.com/vitejs/vite/commit/d4ae45d)), closes [#7091](https://github.com/vitejs/vite/issues/7091)
* feat: add `importedCss` and `importedAssets` to RenderedChunk type (#6629) ([8d0fc90](https://github.com/vitejs/vite/commit/8d0fc90)), closes [#6629](https://github.com/vitejs/vite/issues/6629)
* feat: non-blocking pre bundling of dependencies (#6758) ([24bb3e4](https://github.com/vitejs/vite/commit/24bb3e4)), closes [#6758](https://github.com/vitejs/vite/issues/6758)
* feat: optimize custom extensions (#6801) ([c11af23](https://github.com/vitejs/vite/commit/c11af23)), closes [#6801](https://github.com/vitejs/vite/issues/6801)
* feat: show all prebundle deps when debug (#6726) ([e626055](https://github.com/vitejs/vite/commit/e626055)), closes [#6726](https://github.com/vitejs/vite/issues/6726)
* feat(glob): import.meta.glob support alias path (#6526) ([86882ad](https://github.com/vitejs/vite/commit/86882ad)), closes [#6526](https://github.com/vitejs/vite/issues/6526)
* feat(perf): tsconfck perf improvement (#7055) ([993ea39](https://github.com/vitejs/vite/commit/993ea39)), closes [#7055](https://github.com/vitejs/vite/issues/7055)
* feat(worker): bundle worker emit asset file (#6599) ([0ade335](https://github.com/vitejs/vite/commit/0ade335)), closes [#6599](https://github.com/vitejs/vite/issues/6599)
* refactor: avoid splitting vendor chunk by default (#6534) ([849e845](https://github.com/vitejs/vite/commit/849e845)), closes [#6534](https://github.com/vitejs/vite/issues/6534)


### Beta Changelogs


#### [2.9.0-beta.11](https://github.com/vitejs/vite/compare/v2.9.0-beta.10...v2.9.0-beta.11) (2022-03-29)

See [2.9.0-beta.11 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.11/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.10](https://github.com/vitejs/vite/compare/v2.9.0-beta.9...v2.9.0-beta.10) (2022-03-28)

See [2.9.0-beta.10 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.10/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.9](https://github.com/vitejs/vite/compare/v2.9.0-beta.8...v2.9.0-beta.9) (2022-03-26)

See [2.9.0-beta.9 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.9/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.8](https://github.com/vitejs/vite/compare/v2.9.0-beta.7...v2.9.0-beta.8) (2022-03-24)

See [2.9.0-beta.8 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.8/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.7](https://github.com/vitejs/vite/compare/v2.9.0-beta.6...v2.9.0-beta.7) (2022-03-23)

See [2.9.0-beta.7 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.7/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.6](https://github.com/vitejs/vite/compare/v2.9.0-beta.5...v2.9.0-beta.6) (2022-03-22)

See [2.9.0-beta.6 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.6/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.5](https://github.com/vitejs/vite/compare/v2.9.0-beta.4...v2.9.0-beta.5) (2022-03-22)

See [2.9.0-beta.5 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.5/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.4](https://github.com/vitejs/vite/compare/v2.9.0-beta.3...v2.9.0-beta.4) (2022-03-19)

See [2.9.0-beta.4 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.4/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.3](https://github.com/vitejs/vite/compare/v2.9.0-beta.2...v2.9.0-beta.3) (2022-03-16)

See [2.9.0-beta.3 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.3/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.2](https://github.com/vitejs/vite/compare/v2.9.0-beta.1...v2.9.0-beta.2) (2022-03-14)

See [2.9.0-beta.2 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.2/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.1](https://github.com/vitejs/vite/compare/v2.9.0-beta.0...v2.9.0-beta.1) (2022-03-14)

See [2.9.0-beta.1 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.1/packages/vite/CHANGELOG.md)


#### [2.9.0-beta.0](https://github.com/vitejs/vite/compare/v2.8.6...v2.9.0-beta.0) (2022-03-09)

See [2.9.0-beta.0 changelog](https://github.com/vitejs/vite/blob/v2.9.0-beta.0/packages/vite/CHANGELOG.md)



## [2.8.6](https://github.com/vitejs/vite/compare/v2.8.5...v2.8.6) (2022-03-01)


### Bug Fixes

* revert [#7052](https://github.com/vitejs/vite/issues/7052), hmr style tag no support in html ([#7136](https://github.com/vitejs/vite/issues/7136)) ([5c116ec](https://github.com/vitejs/vite/commit/5c116ecde0ad43409334853457d68481a22e19d4))
* throw Error when can't preload CSS ([#7108](https://github.com/vitejs/vite/issues/7108)) ([d9f8edb](https://github.com/vitejs/vite/commit/d9f8edbd5b243f60212cc4bb9271c01b7e3fdd76))



## [2.8.5](https://github.com/vitejs/vite/compare/v2.8.4...v2.8.5) (2022-02-28)


### Bug Fixes

* ?html-proxy with trailing = added by some servers ([#7093](https://github.com/vitejs/vite/issues/7093)) ([5818ac9](https://github.com/vitejs/vite/commit/5818ac927861783ea2b05450761fed30f40e7399))
* allow optional trailing comma in asset `import.meta.url` ([#6983](https://github.com/vitejs/vite/issues/6983)) ([2debb9f](https://github.com/vitejs/vite/commit/2debb9f4cbb6003e7d24444cf049b45582d82ff1))
* cannot reassign process.env.NODE_ENV in ssr ([#6989](https://github.com/vitejs/vite/issues/6989)) ([983feb2](https://github.com/vitejs/vite/commit/983feb2cdc5180dc46c3f5fc5b99baaa8d6b7078))
* **config:** Warn about terserOptions in more cases ([#7101](https://github.com/vitejs/vite/issues/7101)) ([79428ad](https://github.com/vitejs/vite/commit/79428ad5b849455e14f95d1b439ae296ba231221))
* don't override user config ([#7034](https://github.com/vitejs/vite/issues/7034)) ([8fd8f6e](https://github.com/vitejs/vite/commit/8fd8f6e0e501c9e46bc3e179c900d31fa5cafce1))
* fileToBuiltUrl got undefined when file type is `.ico` ([#7106](https://github.com/vitejs/vite/issues/7106)) ([7a1a552](https://github.com/vitejs/vite/commit/7a1a552ba710bad5714ef0fbb16fdd29ac58ae0b))
* **glob:** css imports injecting a ?used query to export the css string ([#6949](https://github.com/vitejs/vite/issues/6949)) ([0b3f4ef](https://github.com/vitejs/vite/commit/0b3f4ef231004e072bf1b037f63bc4ef169d938e))
* **hmr:** hmr style tag no support in html ([#7052](https://github.com/vitejs/vite/issues/7052)) ([a9dfce3](https://github.com/vitejs/vite/commit/a9dfce38108e796e0de0e3b43ced34d60883cef3))
* image -> image/x-icon ([#7120](https://github.com/vitejs/vite/issues/7120)) ([065ceca](https://github.com/vitejs/vite/commit/065ceca5c7b8f1843e220fbdbe8a0da4cbb78935))
* import with query with exports field ([#7073](https://github.com/vitejs/vite/issues/7073)) ([88ded7f](https://github.com/vitejs/vite/commit/88ded7f16382d83603511de043785e01ee1e4a3a))
* prebundle dep with colon ([#7006](https://github.com/vitejs/vite/issues/7006)) ([2136f2b](https://github.com/vitejs/vite/commit/2136f2bb960d1a81ac3b3ca04d9ebd89dba44661))
* recycle serve to avoid preventing Node self-exit ([#6895](https://github.com/vitejs/vite/issues/6895)) ([d6b2c53](https://github.com/vitejs/vite/commit/d6b2c53c6f0bcc4ffa9cdf48375f9bbcc98f79f7))
* resolve [@import](https://github.com/import) of the proxied <style> ([#7031](https://github.com/vitejs/vite/issues/7031)) ([c7aad02](https://github.com/vitejs/vite/commit/c7aad0287ce24f299f538828c090819ce0ca1468))
* **ssrTransform:** use appendLeft instead of appendRight ([#6407](https://github.com/vitejs/vite/issues/6407)) ([3012541](https://github.com/vitejs/vite/commit/30125418b4c7ebda56555090b177ac34b29ffdc7))
* typo ([#7064](https://github.com/vitejs/vite/issues/7064)) ([f38654f](https://github.com/vitejs/vite/commit/f38654fd331316f496008f3a118d2628c65b071b))


### Features

* add fixStacktrace option to ssrLoadModule ([#7048](https://github.com/vitejs/vite/issues/7048)) ([c703a33](https://github.com/vitejs/vite/commit/c703a3348adeaad9dc92d805a381866917f2a03b))
* **cli:** add command descriptions ([#6991](https://github.com/vitejs/vite/issues/6991)) ([ffda8f0](https://github.com/vitejs/vite/commit/ffda8f046026980b363ff164677f52bb076fde26))



## [2.8.4](https://github.com/vitejs/vite/compare/v2.8.3...v2.8.4) (2022-02-18)


### Bug Fixes

* don't replace NODE_ENV in vite:client-inject ([#6935](https://github.com/vitejs/vite/issues/6935)) ([2b70003](https://github.com/vitejs/vite/commit/2b70003f4758114c50269a260aac3516a32b16b5))
* normalize postcss dependency messages ([#6959](https://github.com/vitejs/vite/issues/6959)) ([3f3f473](https://github.com/vitejs/vite/commit/3f3f4737d5242547fb83f8d2522ba91cc1d96fb0))
* revert [#6935](https://github.com/vitejs/vite/issues/6935), bypass replacing process.env.NODE_ENV in ssr ([#6970](https://github.com/vitejs/vite/issues/6970)) ([b8218b0](https://github.com/vitejs/vite/commit/b8218b068caf0231502f0d0d0f8933330643f417))



## [2.8.3](https://github.com/vitejs/vite/compare/v2.8.2...v2.8.3) (2022-02-15)


### Bug Fixes

* revert update dotenv-expand [#6703](https://github.com/vitejs/vite/issues/6703), fix [#6858](https://github.com/vitejs/vite/issues/6858) ([#6934](https://github.com/vitejs/vite/issues/6934)) ([a9a1ae2](https://github.com/vitejs/vite/commit/a9a1ae2db6a81a2fd31db370b58686e442047d9e))



## [2.8.2](https://github.com/vitejs/vite/compare/v2.8.1...v2.8.2) (2022-02-14)


### Features

* custom manifest file name ([#6667](https://github.com/vitejs/vite/issues/6667)) ([e385346](https://github.com/vitejs/vite/commit/e385346c53b3bb54f2e1abcb7348e33d7e075fd4))
* make `import.meta.glob` and `import.meta.globEager` generic ([#5073](https://github.com/vitejs/vite/issues/5073)) ([78e84c8](https://github.com/vitejs/vite/commit/78e84c80c0f49d6f7c8a0e10c4257a477a221280))


### Performance Improvements

* improve isFileReadable performance ([#6868](https://github.com/vitejs/vite/issues/6868)) ([62cbe68](https://github.com/vitejs/vite/commit/62cbe68ab713d5aba626a1e3a4da46e8c2320bf3))
* lazy import preview function ([#6898](https://github.com/vitejs/vite/issues/6898)) ([2eabcb9](https://github.com/vitejs/vite/commit/2eabcb9a30a413ff540cbdd60a919a0d1f72fb35))



## [2.8.1](https://github.com/vitejs/vite/compare/v2.8.0...v2.8.1) (2022-02-11)


### Bug Fixes

* **deps:** update all non-major dependencies ([#6782](https://github.com/vitejs/vite/issues/6782)) ([e38be3e](https://github.com/vitejs/vite/commit/e38be3e6ca7bf79319d5d7188e1d347b1d6091ef))
* **scan:** escape for virtual modules ([#6863](https://github.com/vitejs/vite/issues/6863)) ([de20c73](https://github.com/vitejs/vite/commit/de20c73ef37b179c1791c0f96da04d29cfd48840))



# [2.8.0](https://github.com/vitejs/vite/compare/v2.8.0-beta.7...v2.8.0) (2022-02-09)

### Reduced Footprint

[Vite 2.8.0](https://packagephobia.com/result?p=vite%402.8.0) is almost 1/4 of the [2.7.0](https://packagephobia.com/result?p=vite%402.7.0) publish size, and the install size has been reduced by 35%. See [this thread](https://twitter.com/IAmTrySound/status/1475600522572877829) about each change that reduced Vite's footprint.

| Version                                                  | Publish Size | Install Size |
| -------------------------------------------------------- | ------------ | ------------ |
| [2.7.0](https://packagephobia.com/result?p=vite%402.7.0) | 12.7MB       | 25.2MB       |
| [2.8.0](https://packagephobia.com/result?p=vite%402.8.0) | 4.6MB        | 17.4MB       |

### Default preview port

New default port for `vite preview` is 4173 (avoid conflicts in macOS that took over the 5000 port)

### Workers using standard syntax

Workers are detected and bundled when using `new URL('path', import.meta.url)`, replacing the need for the `?worker` suffix and aligning Vite with standard patterns. See [#6356](https://github.com/vitejs/vite/issues/6356). Instead of

```js
import MyWorker from './worker.js?worker'
const worker = new MyWorker()
```

it is now recommended to use

```js
const worker = new Worker(
  new URL('./worker.js', import.meta.url), { type: 'module' }
)
```

### Configuring Workers Bundling

New `worker` config field adding support for Worker `format`, `plugins` and, `rollupOptions`. See [#6351](https://github.com/vitejs/vite/issues/6351)
  * `worker.format: 'es' | 'iife'`<br>
     Output format for worker bundle (default: `iife`).
  * `worker.plugins: (Plugin | Plugin[])[]`<br>
     Vite plugins that apply to worker bundle.
  * `worker.rollupOptions: `[`RollupOptions`](https://rollupjs.org/guide/en/#big-list-of-options)<br>
     Rollup options to build worker bundle.

The worker plugins pipeline isn't shared with the main Vite pipeline, there may be plugins that shouldn't be applied to Workers. If a plugin must be applied to both the main build and the worker build, you need to add a plugin in the main `plugins` array and another one in the `worker.plugins` config.

```js
import PluginX from 'vite-plugin-x'
export default {
  plugins: [ PluginX() ]
  worker: {
    format: 'es',
    plugins: [ PluginX() ]
  }
}
```

### Raw Glob Imports

Glob imports now support the `raw` modifier (that works in the same way as [the `?raw` suffix]() in regular imports). Vite is going to gradually migrate to the new standard `assert` syntax instead of using custom URL suffixes where possible.

```js
const examples = import.meta.globEager('./examples/*.html', { assert: { type: 'raw' }})
```

* New `server.headers` config option allowing configuration of response headers in dev mode.

```js
export default {
 server: {
    port: '8080',
    headers: {
      'Cache-Control': 'no-store'
    }
  },
}
```

### Bug Fixes

* revert [#6233](https://github.com/vitejs/vite/issues/6233), strip query when resolving entry (fix [#6797](https://github.com/vitejs/vite/issues/6797)) ([a012644](https://github.com/vitejs/vite/commit/a0126441a556b4991ac14cf037820194ab9e17b9))
* **ssr:** skip vite resolve for windows absolute path ([#6764](https://github.com/vitejs/vite/issues/6764)) ([489a7f1](https://github.com/vitejs/vite/commit/489a7f11e9d89932310025299c1eeb75c5cb4ce6))
* revert [#5342](https://github.com/vitejs/vite/issues/5342), only run build-html plugin on bundler inputs ([#6715](https://github.com/vitejs/vite/issues/6715)) ([59f8a63](https://github.com/vitejs/vite/commit/59f8a639bc6abd9e6c99bc77e155990c43e07ad9))
* **build:** NODE_ENV override by .env ([#6303](https://github.com/vitejs/vite/issues/6303)) ([7329b24](https://github.com/vitejs/vite/commit/7329b24e03952b8fb25b025b61955e40ef777e2a))
* debug `dotenv` when specifically scoped ([#6682](https://github.com/vitejs/vite/issues/6682)) ([c2f0021](https://github.com/vitejs/vite/commit/c2f00214e41b62196fab9108da76609aa8edbaa4))
* **dev:** prevent stripping query params from CSS in HMR ([#6589](https://github.com/vitejs/vite/issues/6589)) ([3ab96c6](https://github.com/vitejs/vite/commit/3ab96c6171dbd3a6155e3496f901d2718edae558))
* **legacy:** fix conflict with the modern build on css emitting ([#6584](https://github.com/vitejs/vite/issues/6584)) ([f48255e](https://github.com/vitejs/vite/commit/f48255e6e0058e973b949fb4a2372974f0480e11)), closes [#3296](https://github.com/vitejs/vite/issues/3296) [#3317](https://github.com/vitejs/vite/issues/3317) [/github.com/vitejs/vite/commit/6bce1081991501f3779bff1a81e5dd1e63e5d38e#diff-2cfbd4f4d8c32727cd8e1a561cffbde0b384a3ce0789340440e144f9d64c10f6R262-R263](https://github.com//github.com/vitejs/vite/commit/6bce1081991501f3779bff1a81e5dd1e63e5d38e/issues/diff-2cfbd4f4d8c32727cd8e1a561cffbde0b384a3ce0789340440e144f9d64c10f6R262-R263)
* revert [#5601](https://github.com/vitejs/vite/issues/5601) [#6025](https://github.com/vitejs/vite/issues/6025), don't resolve rollupOptions.input ([#6680](https://github.com/vitejs/vite/issues/6680)) ([2a9da2e](https://github.com/vitejs/vite/commit/2a9da2e3b10e3637f7ed7daa3b45cb173f40d7a3))
* update SSR externals only when SSR is enabled (fix [#6478](https://github.com/vitejs/vite/issues/6478)) ([#6492](https://github.com/vitejs/vite/issues/6492)) ([28d1e7e](https://github.com/vitejs/vite/commit/28d1e7eed2213f0b22936ff6900354b29e320bc9))
* avoid referencing importGlob from importMeta.d.ts ([#6531](https://github.com/vitejs/vite/issues/6531)) ([962d285](https://github.com/vitejs/vite/commit/962d28508dce63b395e79b79f3b0e2cf0e381a71))
* **config:** merge array correctly ([#6499](https://github.com/vitejs/vite/issues/6499)) ([b2d972e](https://github.com/vitejs/vite/commit/b2d972e53b59329695f74e01893b21ec5c136ffd))
* improve alias merging ([#6497](https://github.com/vitejs/vite/issues/6497)) ([e57d8c6](https://github.com/vitejs/vite/commit/e57d8c63042c2701e797c797b25af65d9dab9eea))
* improve array config merging ([#6344](https://github.com/vitejs/vite/issues/6344)) ([028cbeb](https://github.com/vitejs/vite/commit/028cbeb34adef217f274be7c4a7dd5c9f9b12b29))
* merge debug params instead of overwrite ([#6504](https://github.com/vitejs/vite/issues/6504)) ([#6505](https://github.com/vitejs/vite/issues/6505)) ([1ac7fb1](https://github.com/vitejs/vite/commit/1ac7fb19befe4c18a08786038dc1b63325e96835))
* only run build-html plugin on bundler inputs (fix [#4067](https://github.com/vitejs/vite/issues/4067)) ([#5342](https://github.com/vitejs/vite/issues/5342)) ([7541a8d](https://github.com/vitejs/vite/commit/7541a8d570d9bbf0ab0cd4264cae985dddaf3189))
* **ssr:** avoid using `tryNodeResolve` on absolute paths ([#6488](https://github.com/vitejs/vite/issues/6488)) ([f346d89](https://github.com/vitejs/vite/commit/f346d89741b3c3a5287ce8b03637e520777d3674))
* **ssr:** fix resolution for nested ssr externals ([#6080](https://github.com/vitejs/vite/issues/6080)) ([#6470](https://github.com/vitejs/vite/issues/6470)) ([4a764f5](https://github.com/vitejs/vite/commit/4a764f52e4964b02c02f1ce6863ae3454daad55c))
* **ssr:** handle nameless descture in function args ([#6489](https://github.com/vitejs/vite/issues/6489)) ([debc08d](https://github.com/vitejs/vite/commit/debc08de75434bb63f50e0e5669995de0878ce37))
* **ssr:** should correctly transfrom identifier in ssr ([#6548](https://github.com/vitejs/vite/issues/6548)) ([15cd975](https://github.com/vitejs/vite/commit/15cd975933f6213d25d004634b3d49eb1630e360))
* **types:** add missing options parameter to importMeta ([#6433](https://github.com/vitejs/vite/issues/6433)) ([ccf7d79](https://github.com/vitejs/vite/commit/ccf7d791497139951fde58168999d44e18f706ee))
* **types:** dynamic import in import.meta ([#6456](https://github.com/vitejs/vite/issues/6456)) ([5d7b4c3](https://github.com/vitejs/vite/commit/5d7b4c31b8e44add7c192ae8af4b90b9378ae1fe)), closes [#6433](https://github.com/vitejs/vite/issues/6433)
* update preview port to 4173 ([#6330](https://github.com/vitejs/vite/issues/6330)) ([870e1c0](https://github.com/vitejs/vite/commit/870e1c076272960a5f390b2cfdd3ae275b3891a5))
* use cacheDir for resolveHttpsConfig ([#6416](https://github.com/vitejs/vite/issues/6416)) ([647168b](https://github.com/vitejs/vite/commit/647168b2b44b82b1a1cbd8e639f74ddf52a5d5cd))
* improve array config merging ([#6344](https://github.com/vitejs/vite/issues/6344)) ([028cbeb](https://github.com/vitejs/vite/commit/028cbeb34adef217f274be7c4a7dd5c9f9b12b29))
* only run build-html plugin on bundler inputs (fix [#4067](https://github.com/vitejs/vite/issues/4067)) ([#5342](https://github.com/vitejs/vite/issues/5342)) ([7541a8d](https://github.com/vitejs/vite/commit/7541a8d570d9bbf0ab0cd4264cae985dddaf3189))
* **ssr:** handle nameless descture in function args ([#6489](https://github.com/vitejs/vite/issues/6489)) ([debc08d](https://github.com/vitejs/vite/commit/debc08de75434bb63f50e0e5669995de0878ce37))
* **types:** add missing options parameter to importMeta ([#6433](https://github.com/vitejs/vite/issues/6433)) ([ccf7d79](https://github.com/vitejs/vite/commit/ccf7d791497139951fde58168999d44e18f706ee))
* **types:** dynamic import in import.meta ([#6456](https://github.com/vitejs/vite/issues/6456)) ([5d7b4c3](https://github.com/vitejs/vite/commit/5d7b4c31b8e44add7c192ae8af4b90b9378ae1fe)), closes [#6433](https://github.com/vitejs/vite/issues/6433)
* use cacheDir for resolveHttpsConfig ([#6416](https://github.com/vitejs/vite/issues/6416)) ([647168b](https://github.com/vitejs/vite/commit/647168b2b44b82b1a1cbd8e639f74ddf52a5d5cd))
* **build:** fix chokidar.ignore override ([#6317](https://github.com/vitejs/vite/issues/6317)) ([aa47549](https://github.com/vitejs/vite/commit/aa475494c61898638a592387ac907a939f1dd938))
* **build:** fix watch crash with inline module ([#6373](https://github.com/vitejs/vite/issues/6373)) ([49d2f6d](https://github.com/vitejs/vite/commit/49d2f6dbd9445518b022f6c75ca397460a02d9d8))
* check if e.stack exists in the first place ([#6362](https://github.com/vitejs/vite/issues/6362)) ([f144aa9](https://github.com/vitejs/vite/commit/f144aa9f1df2134dc6695db6e8eff25cac2b5263))
* correct ssr flag in resolve calls (fix [#6213](https://github.com/vitejs/vite/issues/6213)) ([#6216](https://github.com/vitejs/vite/issues/6216)) ([6dd7d1a](https://github.com/vitejs/vite/commit/6dd7d1a7cb99737dd48e070607d0fe9ece35adab))
* **css:** no emit assets in html style tag (fix [#5968](https://github.com/vitejs/vite/issues/5968)) ([#6321](https://github.com/vitejs/vite/issues/6321)) ([dc9fce1](https://github.com/vitejs/vite/commit/dc9fce144a957a5e7b3612b27bc657121a882edc))
* don't force terser on non-legacy (fix [#6266](https://github.com/vitejs/vite/issues/6266)) ([#6272](https://github.com/vitejs/vite/issues/6272)) ([1da104e](https://github.com/vitejs/vite/commit/1da104e8597e2965313e8cd582d032bca551e4ee))
* prevent dev server crashing on malformed URI (fix [#6300](https://github.com/vitejs/vite/issues/6300)) ([#6308](https://github.com/vitejs/vite/issues/6308)) ([a49d723](https://github.com/vitejs/vite/commit/a49d72358f2d028f62b0e9fcdb096a0e5ddf24c3))
* replace chalk with picocolors ([#6277](https://github.com/vitejs/vite/issues/6277)) ([5a111ce](https://github.com/vitejs/vite/commit/5a111cedf31f579e3b8c8af5c4442d2e0cd5aa12))
* replace execa with cross-spawn ([#6299](https://github.com/vitejs/vite/issues/6299)) ([f68ed8b](https://github.com/vitejs/vite/commit/f68ed8b4ebbec01491d069164b28a5948537f0d7))
* **ssr:** move `vite:ssr-require-hook` after user plugins ([#6306](https://github.com/vitejs/vite/issues/6306)) ([d856c4b](https://github.com/vitejs/vite/commit/d856c4bd6798707e0cbdfc127a2e8b6c00c65dae))
* strip NULL_BYTE_PLACEHOLDER before transform ([#6390](https://github.com/vitejs/vite/issues/6390)) ([5964949](https://github.com/vitejs/vite/commit/596494948a6e2f697232371b200c2d7a51d386bc))
* strip query when resolving entry ([#6233](https://github.com/vitejs/vite/issues/6233)) ([000ba2e](https://github.com/vitejs/vite/commit/000ba2e00b14e6c595febfa6dcae862e2d341823))
* upgrade postcss-modules ([#6248](https://github.com/vitejs/vite/issues/6248)) ([ac3f434](https://github.com/vitejs/vite/commit/ac3f434b8b7bc827fd76a28989f8c3ebaa999ee9))
* use `hires: true` for SSR require hook source map ([#6310](https://github.com/vitejs/vite/issues/6310)) ([0ebeb98](https://github.com/vitejs/vite/commit/0ebeb981789e6c29889db03fc11fd9b80c63883f))

### Features

* add lerna workspace support to `searchForWorkspaceRoot` ([#6270](https://github.com/vitejs/vite/issues/6270)) ([0e164f8](https://github.com/vitejs/vite/commit/0e164f80ee36f99ef5277320b3b69448459ef7ba))
* add .txt file format to assets ([#6265](https://github.com/vitejs/vite/issues/6265)) ([e87ae41](https://github.com/vitejs/vite/commit/e87ae41ae57857f387a67b5140bf7d5689a3e14b))
* allow globs in node_modules when pattern is explicit ([#6056](https://github.com/vitejs/vite/issues/6056)) ([669d7e0](https://github.com/vitejs/vite/commit/669d7e0f4b6ea4a73d3598ab1473b58c72bf093b))
* **html:** html simple script tag support import-expression ([#6525](https://github.com/vitejs/vite/issues/6525)) ([3546d4f](https://github.com/vitejs/vite/commit/3546d4ffcfbc011d78f9ba26e0dc689853575a1e))
* add customResolver option to resolve.alias ([#5876](https://github.com/vitejs/vite/issues/5876)) ([6408a3a](https://github.com/vitejs/vite/commit/6408a3ab9bd97f1542982755b5044871a78b59d4))
* new Worker can bundle URL('path', import.meta.url) script (fix [#5979](https://github.com/vitejs/vite/issues/5979)) ([#6356](https://github.com/vitejs/vite/issues/6356)) ([a345614](https://github.com/vitejs/vite/commit/a34561490b4b866d8d4f98c697435dcb68a5c3ed))
* catch postcss error messages ([#6293](https://github.com/vitejs/vite/issues/6293)) ([4d75b2e](https://github.com/vitejs/vite/commit/4d75b2e39d4decd1294f62333bdae4ba577bf1cb))
* **define:** prevent assignment ([#5515](https://github.com/vitejs/vite/issues/5515)) ([6d4ee18](https://github.com/vitejs/vite/commit/6d4ee18e0c45e7c1fedd36c24b631a8f97f40c0f))
* import.meta.glob support ?raw ([#5545](https://github.com/vitejs/vite/issues/5545)) ([5279de6](https://github.com/vitejs/vite/commit/5279de6859df61b6191a4c3bfc76da582309a5ec))
* option to disable pre-transform ([#6309](https://github.com/vitejs/vite/issues/6309)) ([2c14525](https://github.com/vitejs/vite/commit/2c145252b7870e8173886339b69f189878533839))
* **server:** support headers configurable ([#5580](https://github.com/vitejs/vite/issues/5580)) ([db36e81](https://github.com/vitejs/vite/commit/db36e8158e06ff6a383d03b9680aafc7f62d5033))
* **server:** trace `error.loc` back to original source ([#5467](https://github.com/vitejs/vite/issues/5467)) ([65cd44d](https://github.com/vitejs/vite/commit/65cd44dcabbf213b24d68cf02d787e7b9e138c21))
* **ssr:** support preload dynamic css file in html head ([#5705](https://github.com/vitejs/vite/issues/5705)) ([07fca95](https://github.com/vitejs/vite/commit/07fca955519a98e19d4e138a17e19a000eef3f46))
* support .cjs config file ([#5602](https://github.com/vitejs/vite/issues/5602)) ([cddd986](https://github.com/vitejs/vite/commit/cddd986b2a3c61afd53d6fde88f9f28d3c3a6b00))
* **vite:** pass mode to preview command ([#6392](https://github.com/vitejs/vite/issues/6392)) ([1ff1103](https://github.com/vitejs/vite/commit/1ff1103ade691b0a3f564609fdc4e76d5122227b))
* **worker:** support worker format, plugins and rollupOptions (fix [#6191](https://github.com/vitejs/vite/issues/6191)) ([#6351](https://github.com/vitejs/vite/issues/6351)) ([133fcea](https://github.com/vitejs/vite/commit/133fcea5223263b0ae08ac9a0422b55183ebd266))

### Beta Changelogs

#### [2.8.0-beta.7](https://github.com/vitejs/vite/compare/v2.8.0-beta.6...v2.8.0-beta.7) (2022-02-08)

See [2.8.0-beta.7 changelog](https://github.com/vitejs/vite/blob/v2.8.0-beta.7/packages/vite/CHANGELOG.md)


#### [2.8.0-beta.6](https://github.com/vitejs/vite/compare/v2.8.0-beta.5...v2.8.0-beta.6) (2022-02-07)

See [2.8.0-beta.6 changelog](https://github.com/vitejs/vite/blob/v2.8.0-beta.6/packages/vite/CHANGELOG.md)


#### [2.8.0-beta.5](https://github.com/vitejs/vite/compare/v2.8.0-beta.4...v2.8.0-beta.5) (2022-02-02)

See [2.8.0-beta.5 changelog](https://github.com/vitejs/vite/blob/v2.8.0-beta.5/packages/vite/CHANGELOG.md)


#### [2.8.0-beta.4](https://github.com/vitejs/vite/compare/v2.8.0-beta.3...v2.8.0-beta.4) (2022-01-31)

See [2.8.0-beta.4 changelog](https://github.com/vitejs/vite/blob/v2.8.0-beta.4/packages/vite/CHANGELOG.md)


#### [2.8.0-beta.3](https://github.com/vitejs/vite/compare/v2.8.0-beta.1...v2.8.0-beta.3) (2022-01-18)

See [2.8.0-beta.3 changelog](https://github.com/vitejs/vite/blob/v2.8.0-beta.3/packages/vite/CHANGELOG.md)


#### [2.8.0-beta.2](https://github.com/vitejs/vite/compare/v2.8.0-beta.1...v2.8.0-beta.2) (2022-01-13)

[2.8.0-beta.2 changelog](https://github.com/vitejs/vite/blob/v2.8.0-beta.2/packages/vite/CHANGELOG.md)


#### [2.8.0-beta.1](https://github.com/vitejs/vite/compare/v2.8.0-beta.0...v2.8.0-beta.1) (2022-01-06)

See [2.8.0-beta.1 changelog](https://github.com/vitejs/vite/blob/v2.8.0-beta.1/packages/vite/CHANGELOG.md)


#### [2.8.0-beta.0](https://github.com/vitejs/vite/compare/v2.7.9...v2.8.0-beta.0) (2022-01-05)

See [2.8.0-beta.0 changelog](https://github.com/vitejs/vite/blob/v2.8.0-beta.0/packages/vite/CHANGELOG.md)


## [2.7.9](https://github.com/vitejs/vite/compare/v2.7.8...v2.7.9) (2021-12-28)



## [2.7.8](https://github.com/vitejs/vite/compare/v2.7.7...v2.7.8) (2021-12-28)


### Bug Fixes

* **html:** show error overlay when parsing invalid file ([#6184](https://github.com/vitejs/vite/issues/6184)) ([1f945f6](https://github.com/vitejs/vite/commit/1f945f62bf4a722c95a7b8f9c14c32a6f2be5c3f))
* seperate source and dep for dymamic import after build ([#6251](https://github.com/vitejs/vite/issues/6251)) ([49da986](https://github.com/vitejs/vite/commit/49da98619692779df58673b9cc6004dd824a6f15))
* **ssr:** capture scope declaration correctly ([#6281](https://github.com/vitejs/vite/issues/6281)) ([60ce7f9](https://github.com/vitejs/vite/commit/60ce7f9a1d1c730a244bc621675240d74f58af3e))
* upgrade to launch-editor with picocolors ([#6209](https://github.com/vitejs/vite/issues/6209)) ([394539c](https://github.com/vitejs/vite/commit/394539c613b1fdee444079dae4275027705e85ae))



## [2.7.7](https://github.com/vitejs/vite/compare/v2.7.6...v2.7.7) (2021-12-26)


### Bug Fixes

* **ssr:** nested destucture ([#6249](https://github.com/vitejs/vite/issues/6249)) ([485e298](https://github.com/vitejs/vite/commit/485e298e72599679e97f0ed1f4315ac5da55da2c))
* **ssr:** transform class props ([#6261](https://github.com/vitejs/vite/issues/6261)) ([2e3fe59](https://github.com/vitejs/vite/commit/2e3fe5932c962d447a4faa4b0ce996ead70c7d34))



## [2.7.6](https://github.com/vitejs/vite/compare/v2.7.5...v2.7.6) (2021-12-22)


### Bug Fixes

* remove virtual module prefix while generating manifest ([#6225](https://github.com/vitejs/vite/issues/6225)) ([d51259b](https://github.com/vitejs/vite/commit/d51259b73c484dea67d4c4afb6b76fbbb866631c))



## [2.7.5](https://github.com/vitejs/vite/compare/v2.7.4...v2.7.5) (2021-12-21)


### Bug Fixes

* **asset:** import assets from encodeURI([#6195](https://github.com/vitejs/vite/issues/6195)) ([#6199](https://github.com/vitejs/vite/issues/6199)) ([4114f84](https://github.com/vitejs/vite/commit/4114f844f876fabfa9beaa6ec65e4002d7c36fbb))
* hmr full-reload encodeURI path ([#6212](https://github.com/vitejs/vite/issues/6212)) ([46b862a](https://github.com/vitejs/vite/commit/46b862a6880a6e83d1e0e451376177c0e5cab0ba))
* remove top-level imports in importMeta.d.ts, fixes augmentation ([#6214](https://github.com/vitejs/vite/issues/6214)) ([6b8d94d](https://github.com/vitejs/vite/commit/6b8d94dca2a1a8b4952e3e3fcd0aed1aedb94215)), closes [#6194](https://github.com/vitejs/vite/issues/6194) [#6211](https://github.com/vitejs/vite/issues/6211) [#6206](https://github.com/vitejs/vite/issues/6206) [#6205](https://github.com/vitejs/vite/issues/6205)
* **ssr:** handle object destructure alias, close [#6222](https://github.com/vitejs/vite/issues/6222) ([#6224](https://github.com/vitejs/vite/issues/6224)) ([1d97ec3](https://github.com/vitejs/vite/commit/1d97ec336a6ee2915faae42d5f82110226929347))



## [2.7.4](https://github.com/vitejs/vite/compare/v2.7.3...v2.7.4) (2021-12-20)


### Bug Fixes

* duplicate variable declaration caused by css modules ([#5873](https://github.com/vitejs/vite/issues/5873)) ([8e16a78](https://github.com/vitejs/vite/commit/8e16a78a2d556b9480e8b2e19ec41fa522621256))
* improve error message for HTML compilation error (fix [#5769](https://github.com/vitejs/vite/issues/5769)) ([#5777](https://github.com/vitejs/vite/issues/5777)) ([79d1397](https://github.com/vitejs/vite/commit/79d139783868bfe2a2741f6e8cffcb72cee65351))
* **ssr:** `ssrTransform` function argument destructure ([#6171](https://github.com/vitejs/vite/issues/6171)) ([2762a0e](https://github.com/vitejs/vite/commit/2762a0e7f0a599ced2c25c9d2baf06ec99ad8cfb))



## [2.7.3](https://github.com/vitejs/vite/compare/v2.7.2...v2.7.3) (2021-12-16)


### Bug Fixes

* do not overwrite rollupOptions.input in dev ([#6025](https://github.com/vitejs/vite/issues/6025)) ([6cdf13a](https://github.com/vitejs/vite/commit/6cdf13ae808a99b7aca6d278bee2ebe6e51d0846))
* Improve post-build asset update check ([#6113](https://github.com/vitejs/vite/issues/6113)) ([611fa03](https://github.com/vitejs/vite/commit/611fa037a72a1179c27794353ffad6ed27e10d1a))
* improve warning message for malformed packages ([#6086](https://github.com/vitejs/vite/issues/6086)) ([717cb08](https://github.com/vitejs/vite/commit/717cb08f8611fd1a15cfd614d346185ffe8a61fd))
* pending reload never timeout ([#6120](https://github.com/vitejs/vite/issues/6120)) ([e002f4f](https://github.com/vitejs/vite/commit/e002f4f4a578ae63156e756abac0487f42b4cdcd))
* respect new port when change the config file ([#6075](https://github.com/vitejs/vite/issues/6075)) ([3ceffcc](https://github.com/vitejs/vite/commit/3ceffcca66311f9a7d71612a596b84888c3f843b))
* **ssr:** robust regexp to check cjs content ([#6053](https://github.com/vitejs/vite/issues/6053)) ([0373441](https://github.com/vitejs/vite/commit/03734417cde10807ab2dd0d71b08c26081aac0b7))
* terminate WebSocket connections before closing WebSocket server ([#6115](https://github.com/vitejs/vite/issues/6115)) ([b9871bb](https://github.com/vitejs/vite/commit/b9871bbed57c5964b3393e798b0ef2526471d692))



## [2.7.2](https://github.com/vitejs/vite/compare/v2.7.1...v2.7.2) (2021-12-13)


### Bug Fixes

* **html:** empty script ([#6057](https://github.com/vitejs/vite/issues/6057)) ([1487223](https://github.com/vitejs/vite/commit/1487223f39b7555b1050b660d847eabf4d20249f))
* **lexGlobPattern:** edge case of glob import ([#6022](https://github.com/vitejs/vite/issues/6022)) ([d4c5cff](https://github.com/vitejs/vite/commit/d4c5cff551ad9fb721243f8abdbf0c78f5b5a7ec))
* ws types ([#6083](https://github.com/vitejs/vite/issues/6083)) ([1ded1a8](https://github.com/vitejs/vite/commit/1ded1a835bfb64f2c70c8c153e979b7911c9a8c1))



## [2.7.1](https://github.com/vitejs/vite/compare/v2.7.0...v2.7.1) (2021-12-07)


### Bug Fixes

* **ssr:** `ssrTransform` handling for empty ArrayPattern ([#5988](https://github.com/vitejs/vite/issues/5988)) ([79aa687](https://github.com/vitejs/vite/commit/79aa68744cf17553448bce5c175a25f785e4a743))



# [2.7.0](https://github.com/vitejs/vite/compare/v2.7.0-beta.11...v2.7.0) (2021-12-07)

- 🎉 Revamped SSR dependency handling
- 🧩 API consolidation
- 🛑 server.fs.strict by default

### BREAKING CHANGES

- `server.fs.strict` is `true` by default ([#5341](https://github.com/vitejs/vite/pull/5341))
  See [server filesystem restriction docs](https://vitejs.dev/config/#server-fs-strict) for more details.
- Plugin hooks `ssr` param to object in `resolveId`, `load`, and `transform` ([#5253](https://github.com/vitejs/vite/pull/5253))
  Previous to this release, the `ssr` param was passed as a `boolean` in the last parameter of each hook. The new interface for these hooks is now:
  ```ts
  export interface Plugin extends RollupPlugin {
    // ... other hooks
    resolveId?(this: PluginContext, source: string, importer: string | undefined, options: {
        custom?: CustomPluginOptions;
        ssr?: boolean;
    }): Promise<ResolveIdResult> | ResolveIdResult;
    load?(this: PluginContext, id: string, options?: {
        ssr?: boolean;
    }): Promise<LoadResult> | LoadResult;
    transform?(this: TransformPluginContext, code: string, id: string, options?: {
        ssr?: boolean;
    }): Promise<TransformResult> | TransformResult;
  }
  ```
  In your plugins, you can check if the last param is a boolean or an object to be backward compatible with 2.6 and give some time to users to migrate to Vite 2.7.
- `server.pluginContainer` options object for `resolveId`, `load`, and `transform` ([#5294](https://github.com/vitejs/vite/pull/5294))
- Normalize scripts and commands naming ([#5207](https://github.com/vitejs/vite/pull/5207))
  Adds a new `vite dev` command alias for `vite serve`, preparing for the new release of create-vite where package scripts are renamed to `dev`, `build`, and `preview`.
- Align experimental `preview` api ([#5407](https://github.com/vitejs/vite/pull/5407))
  This API was first introduced in 2.6 and it is still in flux.
- resolve `rollupOptions.input` paths ([#5601](https://github.com/vitejs/vite/pull/5601))

### Features

* expose `ssrTransform` to server ([#5983](https://github.com/vitejs/vite/issues/5983)) ([8184feb](https://github.com/vitejs/vite/commit/8184feba29c6a89d58bc4437977d22658e946e0c))



# [2.7.0-beta.11](https://github.com/vitejs/vite/compare/v2.7.0-beta.10...v2.7.0-beta.11) (2021-12-06)


### Bug Fixes

* **ssr:** allow primitive default exports and forwarded exports ([#5973](https://github.com/vitejs/vite/issues/5973)) ([a47b663](https://github.com/vitejs/vite/commit/a47b663ad06af8c5bf87128035f6b112de0ecd16))



# [2.7.0-beta.10](https://github.com/vitejs/vite/compare/v2.7.0-beta.9...v2.7.0-beta.10) (2021-12-02)


### Bug Fixes

* invalidate inlined proxy scripts on change ([#5891](https://github.com/vitejs/vite/issues/5891)) ([5b8c58b](https://github.com/vitejs/vite/commit/5b8c58bf9d2fe141cea9bde9492ccbedf9b76213))
* read the correct package.json in ssrExternal ([#5927](https://github.com/vitejs/vite/issues/5927)) ([7edabb4](https://github.com/vitejs/vite/commit/7edabb46de3ce63e078e0cda7cd3ed9e5cdd0f2a)), closes [#5890](https://github.com/vitejs/vite/issues/5890)
* **resolve:** dont overwrite `isRequire` from `baseOptions` ([#5872](https://github.com/vitejs/vite/issues/5872)) ([2b91e5a](https://github.com/vitejs/vite/commit/2b91e5aadaee0947eb9864367ae85762573a8dc4))
* **scan:** handle local scripts with lang=ts ([#5850](https://github.com/vitejs/vite/issues/5850)) ([7ed8702](https://github.com/vitejs/vite/commit/7ed870273206b5e9dcedda6f0149b7b3324dea45))
* SSR import in dev can't resolve default import (fix [#5706](https://github.com/vitejs/vite/issues/5706)) ([#5923](https://github.com/vitejs/vite/issues/5923)) ([21d79d7](https://github.com/vitejs/vite/commit/21d79d753af145f2c7ebb7dd5b0b1a4a298f96c5))
* **ssr:** skip dedupe require if noExternal true ([#5928](https://github.com/vitejs/vite/issues/5928)) ([f6aa7fe](https://github.com/vitejs/vite/commit/f6aa7fe401737ef584ccf34b6042a32b8e5e8c5d))



# [2.7.0-beta.9](https://github.com/vitejs/vite/compare/v2.7.0-beta.8...v2.7.0-beta.9) (2021-11-27)


### Bug Fixes

* `isBuiltin` using patched native `builtinModules` ([#5827](https://github.com/vitejs/vite/issues/5827)) ([4a05a6e](https://github.com/vitejs/vite/commit/4a05a6e2f69c3a799fee651d182beeb176abfaac))
* always bundle config file, fix config hmr ([#5779](https://github.com/vitejs/vite/issues/5779)) ([19d2b6a](https://github.com/vitejs/vite/commit/19d2b6ab9cf2c5ba40f52c345f71d67f321c0776))
* build pluginContext types error ([#5846](https://github.com/vitejs/vite/issues/5846)) ([c278439](https://github.com/vitejs/vite/commit/c2784390ae4cfc1150b63c86a70a240f0f319967))
* circular dependency hmr causes refresh crash ([#4589](https://github.com/vitejs/vite/issues/4589)) ([00d8c9b](https://github.com/vitejs/vite/commit/00d8c9b7ffcfa2a3f888ef5752f57682cdea91b2))
* replace asset references in CSS returned to JS ([#5729](https://github.com/vitejs/vite/issues/5729)) ([880026e](https://github.com/vitejs/vite/commit/880026e414d5745233ff2b67799cd386001bddd8))
* resolve addons using nodeResolve() ([#5809](https://github.com/vitejs/vite/issues/5809)) ([d288772](https://github.com/vitejs/vite/commit/d2887729911d52e3117a7649e85460b346f04b54))
* throw full error causing preprocessor to not load ([#5816](https://github.com/vitejs/vite/issues/5816)) ([f6fcd21](https://github.com/vitejs/vite/commit/f6fcd2190e18f2ad20766a164411351b2220cf52))
* Unicode path html entry point ([#5821](https://github.com/vitejs/vite/issues/5821)) ([#5823](https://github.com/vitejs/vite/issues/5823)) ([2048195](https://github.com/vitejs/vite/commit/20481950dce58e21d06d0d7da0325a3788e683c5))
* unminified build breaks __vitePreload ([#5785](https://github.com/vitejs/vite/issues/5785)) ([757a74a](https://github.com/vitejs/vite/commit/757a74aa41f3b12505557637daec2058423cfd23))


### Features

* lint for missing type="module" attribute ([#5837](https://github.com/vitejs/vite/issues/5837)) ([#5838](https://github.com/vitejs/vite/issues/5838)) ([494e358](https://github.com/vitejs/vite/commit/494e3586fef5865ddc99f3cff48856495c4373f1))



# [2.7.0-beta.8](https://github.com/vitejs/vite/compare/v2.7.0-beta.7...v2.7.0-beta.8) (2021-11-19)


### Bug Fixes

* **hmr:** prevent SSR from setting `isSelfAccepting` to false ([#5377](https://github.com/vitejs/vite/issues/5377)) ([37e5617](https://github.com/vitejs/vite/commit/37e561755030e87383897af3ea28b9a08e8c2773))
* move package.json cache into ResolvedConfig ([#5388](https://github.com/vitejs/vite/issues/5388)) ([650b56e](https://github.com/vitejs/vite/commit/650b56e0414d772294817bc2dc399e70563ed699))
* scoped variable with array destructuring & nested arguments ([#5730](https://github.com/vitejs/vite/issues/5730)) ([b86a2f3](https://github.com/vitejs/vite/commit/b86a2f35ee538d531db3ee0e2094e671b4e0c405))
* **transformCjsImport:** make dev and build get the same result ([#5745](https://github.com/vitejs/vite/issues/5745)) ([9d3e4e6](https://github.com/vitejs/vite/commit/9d3e4e6ca53ba0e9e5c6efbdd84cd347123f93ed))


### Features

* **dev:** expose restart function on ViteDevServer ([#5723](https://github.com/vitejs/vite/issues/5723)) ([1425a16](https://github.com/vitejs/vite/commit/1425a162e768f569e5d9a3929e31ed5f421a5ca2))



# [2.7.0-beta.7](https://github.com/vitejs/vite/compare/v2.7.0-beta.6...v2.7.0-beta.7) (2021-11-17)


### Bug Fixes

* **build:** keep IIFE name after minifying (fix [#5490](https://github.com/vitejs/vite/issues/5490)) ([#5715](https://github.com/vitejs/vite/issues/5715)) ([1544211](https://github.com/vitejs/vite/commit/1544211767695982597c18d028a2edf15372931f))
* **scan:** correctly resolve virtual modules ([#5711](https://github.com/vitejs/vite/issues/5711)) ([01f9b16](https://github.com/vitejs/vite/commit/01f9b16a8bdfa182890924ac00207fe54496b99f))
* **ssr:** skip dedupe require in esm ([#5714](https://github.com/vitejs/vite/issues/5714)) ([9666446](https://github.com/vitejs/vite/commit/96664469e49d44f8c628bf0310bdd03d1c4556de))



# [2.7.0-beta.6](https://github.com/vitejs/vite/compare/v2.7.0-beta.5...v2.7.0-beta.6) (2021-11-16)


### Bug Fixes

* **dev:** Fix infinite recursion on query imports ([#5671](https://github.com/vitejs/vite/issues/5671)) ([#5674](https://github.com/vitejs/vite/issues/5674)) ([bce4e56](https://github.com/vitejs/vite/commit/bce4e56cb12b3c76f48bf2ddc37423025e79a0d2))
* **ssr:** avoid resolving ESM for CJS dependencies ([#5693](https://github.com/vitejs/vite/issues/5693)) ([b937ea4](https://github.com/vitejs/vite/commit/b937ea4cb1642a76d7a650802c0db2fede338474))



# [2.7.0-beta.5](https://github.com/vitejs/vite/compare/v2.7.0-beta.4...v2.7.0-beta.5) (2021-11-13)


### Bug Fixes

* correctly resolve virtual modules during import scan ([#5659](https://github.com/vitejs/vite/issues/5659)) ([40d503c](https://github.com/vitejs/vite/commit/40d503cce08324b6bd6341b45ad8a73876f6f4a0))
* **resolve:** check nested directories for package.json ([#5665](https://github.com/vitejs/vite/issues/5665)) ([022db52](https://github.com/vitejs/vite/commit/022db52f6de19e98e6412e7c11bf719b1fd8960c))
* **ssr:** prefer CJS but still allow ESM entries ([#5662](https://github.com/vitejs/vite/issues/5662)) ([72d8925](https://github.com/vitejs/vite/commit/72d8925f79a8983ae131df06a627ee020aab71f8))
* tolerate undefined parent in `hookNodeResolve` callback ([#5664](https://github.com/vitejs/vite/issues/5664)) ([d788682](https://github.com/vitejs/vite/commit/d788682492465a9365b262dcd93a618e4415637c))



# [2.7.0-beta.4](https://github.com/vitejs/vite/compare/v2.7.0-beta.3...v2.7.0-beta.4) (2021-11-12)


### Bug Fixes

* **build:** resolve `rollupOptions.input` paths ([#5601](https://github.com/vitejs/vite/issues/5601)) ([5b6b016](https://github.com/vitejs/vite/commit/5b6b01693720290e8998b2613f0dcb2d699ee84f))
* check exactly in proxyESM ([#5512](https://github.com/vitejs/vite/issues/5512)) ([a17da55](https://github.com/vitejs/vite/commit/a17da55c5dd7ec6206fea8a255f9383b75384351))
* handle local and module scripts separately ([#5464](https://github.com/vitejs/vite/issues/5464)) ([0713446](https://github.com/vitejs/vite/commit/0713446fa4df678422c84bd141b189a930c100e7))
* **logger:** no sameCount if clearScreen is false ([#5648](https://github.com/vitejs/vite/issues/5648)) ([afd6b6d](https://github.com/vitejs/vite/commit/afd6b6d5408745b6f376318a15762ca6f34e8c68))
* **server:** watch correct env files ([#5520](https://github.com/vitejs/vite/issues/5520)) ([03b77bd](https://github.com/vitejs/vite/commit/03b77bd01677cfa2ac76d1a8438af0ce1c7c5678))
* **sourcemap:** tolerate virtual modules in `sources` array ([#5587](https://github.com/vitejs/vite/issues/5587)) ([cfd2c5e](https://github.com/vitejs/vite/commit/cfd2c5e8deb9fe1e80ec611deff7834a89dcdecc))
* **ssr:** use `tryNodeResolve` instead of `resolveFrom` ([#3951](https://github.com/vitejs/vite/issues/3951)) ([87c0050](https://github.com/vitejs/vite/commit/87c0050dea008120aad79cf23acca7dfd41cd72e))
* use micromatch for consistent glob matching ([#5610](https://github.com/vitejs/vite/issues/5610)) ([9d50df8](https://github.com/vitejs/vite/commit/9d50df8198d7cf339e95095580775a5bf8e93948))
* vitepress/theme in ssrExternals ([#5651](https://github.com/vitejs/vite/issues/5651)) ([1f91cdb](https://github.com/vitejs/vite/commit/1f91cdb6c5c573fd9efd147e38cabc0e5f22028f))


### Features

* support `moduleInfo.meta` in dev server ([#5465](https://github.com/vitejs/vite/issues/5465)) ([f6d08c7](https://github.com/vitejs/vite/commit/f6d08c7430906d6262ee1df729d2ea193a80fa6c))



# [2.7.0-beta.3](https://github.com/vitejs/vite/compare/v2.7.0-beta.2...v2.7.0-beta.3) (2021-11-08)



# [2.7.0-beta.2](https://github.com/vitejs/vite/compare/v2.7.0-beta.1...v2.7.0-beta.2) (2021-11-08)


### Bug Fixes

* **commonjs:** expose ignoreTryCatch config option ([#5555](https://github.com/vitejs/vite/issues/5555)) ([d383c2a](https://github.com/vitejs/vite/commit/d383c2a04159a2e5d2f2618ac4e590bdb3172f77))
* **esbuild:** respect esbuild config on build ([#5538](https://github.com/vitejs/vite/issues/5538)) ([ff05fe9](https://github.com/vitejs/vite/commit/ff05fe99ad1f2fe7524eadd455a4a0b831cd75f2))
* **hmr:** revert early break from handleHotUpdate loop ([#5536](https://github.com/vitejs/vite/issues/5536)) ([4abade6](https://github.com/vitejs/vite/commit/4abade62f101049b941fa8f6b98187c5587e238f))
* replace server.origin in css plugin (fix [#5408](https://github.com/vitejs/vite/issues/5408)) ([#5571](https://github.com/vitejs/vite/issues/5571)) ([bd8b66d](https://github.com/vitejs/vite/commit/bd8b66d8ef4ceb81168a3a7deeff7d9040d778f2))
* **server:** use `options` argument in caching of `transformRequest` calls ([#5391](https://github.com/vitejs/vite/issues/5391)) ([27b7f90](https://github.com/vitejs/vite/commit/27b7f90ce2aa9de4290a8422b899d2d718a8c7d7))
* Windows path error on script proxying ([#5556](https://github.com/vitejs/vite/issues/5556)) ([f8dc1ee](https://github.com/vitejs/vite/commit/f8dc1eee23ec26333af78dd592c35c0306c880a8))


### Features

* importing ts files using their corresponding js extesions ([#5510](https://github.com/vitejs/vite/issues/5510)) ([7977e92](https://github.com/vitejs/vite/commit/7977e92e0610cfcb814b45af8432bab1054863d2))
* preview config ([#5514](https://github.com/vitejs/vite/issues/5514)) ([ff755eb](https://github.com/vitejs/vite/commit/ff755eb7ec2346d2d6c2b74850f0c95063d51a6a))



# [2.7.0-beta.1](https://github.com/vitejs/vite/compare/v2.7.0-beta.0...v2.7.0-beta.1) (2021-11-01)


### Bug Fixes

* **ssr:** dont transform process.env. in ssr ([#5404](https://github.com/vitejs/vite/issues/5404)) ([1140981](https://github.com/vitejs/vite/commit/11409818d934f2b13ba7d5972647d31273fd3293))
* Vite module graph race condition ([#5470](https://github.com/vitejs/vite/issues/5470)) ([70fd32c](https://github.com/vitejs/vite/commit/70fd32c1569c3d93a231577b573dbd2b34da4de2))



# [2.7.0-beta.0](https://github.com/vitejs/vite/compare/v2.6.13...v2.7.0-beta.0) (2021-10-28)

### Bug Fixes

* add `import` support to `ssrModuleLoader` ([#5197](https://github.com/vitejs/vite/issues/5197)) ([baba1f9](https://github.com/vitejs/vite/commit/baba1f9e8fb22254b3858bcc1ffe89b334736068))
* consider # as a valid dir symbol (fix [#4701](https://github.com/vitejs/vite/issues/4701)) ([#4703](https://github.com/vitejs/vite/issues/4703)) ([52689c8](https://github.com/vitejs/vite/commit/52689c88497438a1df5d1b5208e81c74ede7a35f))
* do not overwrite pendingReload promise (fix [#5448](https://github.com/vitejs/vite/issues/5448)) ([#5452](https://github.com/vitejs/vite/issues/5452)) ([cc9c2da](https://github.com/vitejs/vite/commit/cc9c2da7b816a41987000dd662f04dbc2033a600))
* exclude dependency of optimized dependency (fix: 5410) ([#5411](https://github.com/vitejs/vite/issues/5411)) ([ebd4027](https://github.com/vitejs/vite/commit/ebd4027292cc5f0b47d17eb53176924dfab10915))
* missing tags inject fallback ([#5339](https://github.com/vitejs/vite/issues/5339)) ([3c44ac8](https://github.com/vitejs/vite/commit/3c44ac80bbe652c4f0a9cd0561322d223f966435))


### Features

* `server.fs.deny` support ([#5378](https://github.com/vitejs/vite/issues/5378)) ([1a15460](https://github.com/vitejs/vite/commit/1a15460bf35325ab9a7c22aacdb1e0afd1703c52))



## [2.6.13](https://github.com/vitejs/vite/compare/v2.6.12...v2.6.13) (2021-10-27)


### Bug Fixes

* **css:** ?inline cannot self-accept ([#5433](https://github.com/vitejs/vite/issues/5433)) ([d283d9b](https://github.com/vitejs/vite/commit/d283d9b7d6231d296cad36ebb0bcce338769c975))



## [2.6.12](https://github.com/vitejs/vite/compare/v2.6.11...v2.6.12) (2021-10-26)


### Bug Fixes

* allowed files logic (fix [#5416](https://github.com/vitejs/vite/issues/5416)) ([#5420](https://github.com/vitejs/vite/issues/5420)) ([414bc45](https://github.com/vitejs/vite/commit/414bc45693762c330efbe1f3c8c97829cc05695a))



## [2.6.11](https://github.com/vitejs/vite/compare/v2.6.9...v2.6.11) (2021-10-25)


### Bug Fixes

* **build:** let top-level `this` refer to `globalThis` ([#5312](https://github.com/vitejs/vite/issues/5312)) ([7e25429](https://github.com/vitejs/vite/commit/7e254291e7870bdc621b71c3817f001efe9d648c))
* bundle ws types ([#5340](https://github.com/vitejs/vite/issues/5340)) ([bc4a96c](https://github.com/vitejs/vite/commit/bc4a96c883e849cf4dbd74356d4240763e713aef))
* **client:** fix typo in overlay config hint ([#5343](https://github.com/vitejs/vite/issues/5343)) ([96591bf](https://github.com/vitejs/vite/commit/96591bf9989529de839ba89958755eafe4c445ae))
* consider deep imports in isBuiltIn ([#5248](https://github.com/vitejs/vite/issues/5248)) ([269a1b6](https://github.com/vitejs/vite/commit/269a1b672bf954ed68d19d4541b9bdb471fc1937))
* ensure server.host is passed in preview-mode (fix [#5387](https://github.com/vitejs/vite/issues/5387)) ([#5389](https://github.com/vitejs/vite/issues/5389)) ([61b4b39](https://github.com/vitejs/vite/commit/61b4b39acd4c122b26a6c91c45bb0727728da7a3))
* load-fallback catch ([#5412](https://github.com/vitejs/vite/issues/5412)) ([e73281c](https://github.com/vitejs/vite/commit/e73281c806276740c337aea69a233e39235f5a0b))
* restrict static middleware fs access ([#5361](https://github.com/vitejs/vite/issues/5361)) ([1f4723b](https://github.com/vitejs/vite/commit/1f4723bbd82e234e779ee4cbc3a51b85c24463e0))
* **ssr:** ssrTransfrom with function declaration in scope, fix [#4306](https://github.com/vitejs/vite/issues/4306) ([#5376](https://github.com/vitejs/vite/issues/5376)) ([5306632](https://github.com/vitejs/vite/commit/5306632603fb5bb6d93f06e2412416394166e371))


### Performance Improvements

* minify css only when needed ([#5178](https://github.com/vitejs/vite/issues/5178)) ([7970239](https://github.com/vitejs/vite/commit/79702392874d81819e090a4a235313df83a7515c))



## [2.6.10](https://github.com/vitejs/vite/compare/v2.6.9...v2.6.10) (2021-10-18)


### Bug Fixes

* bundle ws types ([#5340](https://github.com/vitejs/vite/issues/5340)) ([bc4a96c](https://github.com/vitejs/vite/commit/bc4a96c883e849cf4dbd74356d4240763e713aef))



## [2.6.9](https://github.com/vitejs/vite/compare/v2.6.8...v2.6.9) (2021-10-18)



## [2.6.8](https://github.com/vitejs/vite/compare/v2.6.7...v2.6.8) (2021-10-18)


### Bug Fixes

* avoid scan failures in .svelte and .astro files ([#5193](https://github.com/vitejs/vite/issues/5193)) ([386ca79](https://github.com/vitejs/vite/commit/386ca79da5c54c35cdff978d0f48481bbbaacd44))
* **deps:** bump postcss-load-config to 3.1.0 ([#5277](https://github.com/vitejs/vite/issues/5277)) ([b7e8a5c](https://github.com/vitejs/vite/commit/b7e8a5c0423570789f8c5476ac42e39ce8c2a009))
* **html:** tags prepend doctype regex ([#5315](https://github.com/vitejs/vite/issues/5315)) ([256b2bb](https://github.com/vitejs/vite/commit/256b2bbd20a31b4a363cb1cf3b6c7e797b0ee5f2))
* improve HTML script proxying ([#5279](https://github.com/vitejs/vite/issues/5279)) ([1d6e7bb](https://github.com/vitejs/vite/commit/1d6e7bb38570a65f54f813a2dc2165f719a1391b))
* regEx for <head> tag, fix [#5285](https://github.com/vitejs/vite/issues/5285) ([#5311](https://github.com/vitejs/vite/issues/5311)) ([3ac08cc](https://github.com/vitejs/vite/commit/3ac08cc78432e3640e3d2925ca854247493b4903))
* **ssr:** make import.meta.url be the filesystem URL ([#5268](https://github.com/vitejs/vite/issues/5268)) ([7674cf2](https://github.com/vitejs/vite/commit/7674cf2e558c6209f667a112a7862058fe7290c8))


### Features

* **ws:** expose `on` / `off` for `server.ws` ([#5273](https://github.com/vitejs/vite/issues/5273)) ([6f696be](https://github.com/vitejs/vite/commit/6f696be112d5d0c3db433ae9cf0c73af078f2825))



## [2.6.7](https://github.com/vitejs/vite/compare/v2.6.6...v2.6.7) (2021-10-11)



## [2.6.6](https://github.com/vitejs/vite/compare/v2.6.5...v2.6.6) (2021-10-11)


### Bug Fixes

* avoid unnecessary  pre-bundling warning ([b586098](https://github.com/vitejs/vite/commit/b58609829262255d73363229584a2341bc4f568d))
* **server:** skipped for ended response ([#5230](https://github.com/vitejs/vite/issues/5230)) ([7255fd5](https://github.com/vitejs/vite/commit/7255fd5f04e71e81d80a0a28fad3ac72bffe186e))


### Features

* add `build.cssTarget` option ([#5132](https://github.com/vitejs/vite/issues/5132)) ([b17444f](https://github.com/vitejs/vite/commit/b17444fd97b02bc54410c8575e7d3cb25e4058c2)), closes [#4746](https://github.com/vitejs/vite/issues/4746) [#5070](https://github.com/vitejs/vite/issues/5070) [#4930](https://github.com/vitejs/vite/issues/4930)



## [2.6.5](https://github.com/vitejs/vite/compare/v2.6.4...v2.6.5) (2021-10-07)


### Features

* **internal:** expose printHttpServerUrls ([f94a720](https://github.com/vitejs/vite/commit/f94a720478c4905463ddf36f4c666431b2a438a9))
* **server:** expose server.printUrls() ([96a9ee4](https://github.com/vitejs/vite/commit/96a9ee4f3566e273db53ef9023222699520e4f8f))



## [2.6.4](https://github.com/vitejs/vite/compare/v2.6.3...v2.6.4) (2021-10-07)


### Bug Fixes

* better error message for parse failures ([#5192](https://github.com/vitejs/vite/issues/5192)) ([8fe8df3](https://github.com/vitejs/vite/commit/8fe8df37d4b68705bfb2f768b47ca99a8678f4e9))
* use Function instead of eval to dynamically import config files ([#5213](https://github.com/vitejs/vite/issues/5213)) ([10694dd](https://github.com/vitejs/vite/commit/10694dd6ad98933b7d857919c09c0f5f8c22da21))



## [2.6.3](https://github.com/vitejs/vite/compare/v2.6.2...v2.6.3) (2021-10-05)


### Bug Fixes

* **dev:** read property of undefined ([#5177](https://github.com/vitejs/vite/issues/5177)) ([70e882f](https://github.com/vitejs/vite/commit/70e882f06a80bcfb6f5189902984751d9c06cf8f))
* **type:** update ExportsData type ([b582581](https://github.com/vitejs/vite/commit/b582581761519a14424e707131a8818de35fd2c4))
* upgrade to @rollup/plugin-commonjs 21.x ([#5173](https://github.com/vitejs/vite/issues/5173)) ([c5bfc5e](https://github.com/vitejs/vite/commit/c5bfc5ec2f52877cd4c57c6731a927ac79b8d322))



## [2.6.2](https://github.com/vitejs/vite/compare/v2.6.1...v2.6.2) (2021-09-30)


### Bug Fixes

* **cli:** log correct hostname ([#5156](https://github.com/vitejs/vite/issues/5156)) ([6f977a5](https://github.com/vitejs/vite/commit/6f977a5f01604d406d2e0c74c4d01a79d3416f06))
* properly handle postfix for getRealPath ([#5149](https://github.com/vitejs/vite/issues/5149)) ([7d257c3](https://github.com/vitejs/vite/commit/7d257c38356f8195ca44b39b55f9d791c6b8c33e))



## [2.6.1](https://github.com/vitejs/vite/compare/v2.6.0...v2.6.1) (2021-09-29)


### Bug Fixes

* **cli:** reorder dev server message ([#5141](https://github.com/vitejs/vite/issues/5141)) ([5fb3e0f](https://github.com/vitejs/vite/commit/5fb3e0f996bcca073420122ca4de3b4300e1c5f5))



# [2.6.0](https://github.com/vitejs/vite/compare/v2.6.0-beta.4...v2.6.0) (2021-09-29)



# [2.6.0-beta.4](https://github.com/vitejs/vite/compare/v2.6.0-beta.3...v2.6.0-beta.4) (2021-09-28)


### Bug Fixes

* don't overwrite default options unless given new value ([#5111](https://github.com/vitejs/vite/issues/5111)) ([4d72b40](https://github.com/vitejs/vite/commit/4d72b403e474ce468d95cc1ef95fdfbec625eb6d))
* use global location for import.meta.url rewrite (fix [#5087](https://github.com/vitejs/vite/issues/5087)) ([#5113](https://github.com/vitejs/vite/issues/5113)) ([0b54853](https://github.com/vitejs/vite/commit/0b54853ad8f62edef7815808bb8d5f8638bee0cb))



# [2.6.0-beta.3](https://github.com/vitejs/vite/compare/v2.6.0-beta.2...v2.6.0-beta.3) (2021-09-27)


### Bug Fixes

* Allow custom asset URL origin in development ([#5104](https://github.com/vitejs/vite/issues/5104)) ([e4ef6dd](https://github.com/vitejs/vite/commit/e4ef6ddbbf6cef689537fe35d8f8378150e87f6e))
* avoid module preload polyfill for zero js html ([#4999](https://github.com/vitejs/vite/issues/4999)) ([ac55755](https://github.com/vitejs/vite/commit/ac55755f12e1f497e00a6ba1781cc80a065d770b))
* injected tags indentation ([#5000](https://github.com/vitejs/vite/issues/5000)) ([4b84c0d](https://github.com/vitejs/vite/commit/4b84c0d66beff9fa6fd6f304df95a70fa2f23144))
* **lib-mode:** do not minify lib mode es output ([06d86e4](https://github.com/vitejs/vite/commit/06d86e4a2e90ca916a43d450bca1e6c28bc4bfe2)), closes [/github.com/vuejs/core/issues/2860#issuecomment-926882793](https://github.com//github.com/vuejs/core/issues/2860/issues/issuecomment-926882793)
* normalize away `base` in imported URLs ([#5065](https://github.com/vitejs/vite/issues/5065)) ([9164da0](https://github.com/vitejs/vite/commit/9164da0fe62cb85e77752849ea6d7a68287fb576))
* server.address before listen, chdir in test, basic cli test ([#5059](https://github.com/vitejs/vite/issues/5059)) ([fb37a63](https://github.com/vitejs/vite/commit/fb37a6315711eb6bae3030e98acdad1b819f0893))
* should load `--config foo.mjs` as an ES module ([#5091](https://github.com/vitejs/vite/issues/5091)) ([5d2c50a](https://github.com/vitejs/vite/commit/5d2c50ad229fc8a9e20171ab17053ea525018e71))
* **types:** missing return type on `logError` ([#5067](https://github.com/vitejs/vite/issues/5067)) ([3c9f1a1](https://github.com/vitejs/vite/commit/3c9f1a16c618858e73cc5be2971b1c9a3bf44420))
* use the same `target` for optimized dependencies and source files ([#5095](https://github.com/vitejs/vite/issues/5095)) ([8456a6f](https://github.com/vitejs/vite/commit/8456a6f2e9d48bea315457f2301bd1585756e6e4)), closes [#4897](https://github.com/vitejs/vite/issues/4897)


### Features

* expose `preview` method ([#5014](https://github.com/vitejs/vite/issues/5014)) ([9885656](https://github.com/vitejs/vite/commit/9885656c33306c3b9992000e0a8c89ae7aade8e5))
* expose `searchForWorkspaceRoot` util ([#4958](https://github.com/vitejs/vite/issues/4958)) ([d0f7bf1](https://github.com/vitejs/vite/commit/d0f7bf16b4949a3c0766ab1119ec166501fd5a63))
* server.open supports absolute path ([#5068](https://github.com/vitejs/vite/issues/5068)) ([2d6f682](https://github.com/vitejs/vite/commit/2d6f682ce32246f2faf7f1a19155770596a75785))



# [2.6.0-beta.2](https://github.com/vitejs/vite/compare/v2.6.0-beta.1...v2.6.0-beta.2) (2021-09-23)


### Bug Fixes

* performance is not defined ([#5048](https://github.com/vitejs/vite/issues/5048)) ([20b20e4](https://github.com/vitejs/vite/commit/20b20e4b814bd08ea85518109b5053bbca24d992))



# [2.6.0-beta.1](https://github.com/vitejs/vite/compare/v2.6.0-beta.0...v2.6.0-beta.1) (2021-09-23)


### Bug Fixes

* bump js parser ecmaVersion option to 'latest', fix [#5013](https://github.com/vitejs/vite/issues/5013) ([#5021](https://github.com/vitejs/vite/issues/5021)) ([3541ebc](https://github.com/vitejs/vite/commit/3541ebc7a0033ae2297b8618a57b56958de6dbb5))
* dedupe import analysis public name ([#5032](https://github.com/vitejs/vite/issues/5032)) ([545b1f1](https://github.com/vitejs/vite/commit/545b1f13cec069bbae5f37c7540171128f439e7b))
* exclude ?commonjs-external when building in JSON plugin ([#4867](https://github.com/vitejs/vite/issues/4867)) ([fe25567](https://github.com/vitejs/vite/commit/fe25567828e7a5cadc6c009ae674a59670e14a49))
* exclude missing dependencies from optimization during SSR ([#5017](https://github.com/vitejs/vite/issues/5017)) ([2204afa](https://github.com/vitejs/vite/commit/2204afa34482384460507aa0149730ab05f99e31))
* move peerDeps from [#2042](https://github.com/vitejs/vite/issues/2042) to the right package.json ([3161d75](https://github.com/vitejs/vite/commit/3161d7560c44ecfe45ac2259c3d702634e6611d0))
* sourcemaps windows drive letter inconsistency, fix 4964 ([#4985](https://github.com/vitejs/vite/issues/4985)) ([723cd63](https://github.com/vitejs/vite/commit/723cd633d85d6476cb2ae92d0fe08cf74f3dec93))
* **ssr:** handle default arguments properly in `ssrTransform` ([#5040](https://github.com/vitejs/vite/issues/5040)) ([6a60080](https://github.com/vitejs/vite/commit/6a600805f0c2803e843a0af279d5f8cc1a2c4d89))
* use lax range for peer deps ([35bd963](https://github.com/vitejs/vite/commit/35bd963cb4bcab9d1bfb9757c5baec69d734b875))


### Features

* default build.minify to esbuild ([#5041](https://github.com/vitejs/vite/issues/5041)) ([e4892be](https://github.com/vitejs/vite/commit/e4892be418e1294f2ec8462f0bf8bd14a6be0fb4))
* pre transform direct imports before requests hit the server ([#5037](https://github.com/vitejs/vite/issues/5037)) ([57b9a37](https://github.com/vitejs/vite/commit/57b9a37ea677e7d63f2e5085a4d018787c025e98))
* support .astro files ([#5038](https://github.com/vitejs/vite/issues/5038)) ([79ff0ec](https://github.com/vitejs/vite/commit/79ff0ecc7fddb34c0a0498169e15c31f857cfecb))



# [2.6.0-beta.0](https://github.com/vitejs/vite/compare/v2.5.7...v2.6.0-beta.0) (2021-09-20)


### Bug Fixes

* avoid wrong warning of explicit public paths ([#4927](https://github.com/vitejs/vite/issues/4927)) ([9e06b81](https://github.com/vitejs/vite/commit/9e06b81973cf298aeb0a1f48c67a496bf984c663))
* **css:** revert return sourcemap in vite:css transform ([#4880](https://github.com/vitejs/vite/issues/4880)) ([#4951](https://github.com/vitejs/vite/issues/4951)) ([72cb33e](https://github.com/vitejs/vite/commit/72cb33e947e7aa72d27ed0c5eacb2457d523dfbf))
* **deps:** update all non-major dependencies ([#4545](https://github.com/vitejs/vite/issues/4545)) ([a44fd5d](https://github.com/vitejs/vite/commit/a44fd5d38679da0be2536103e83af730cda73a95))
* do not include css string in bundle if not needed ([3e3c203](https://github.com/vitejs/vite/commit/3e3c20364d6c065026f7362bbcb7094099705cc9))
* docs for ssr manifest plugin and dedupe name ([#4974](https://github.com/vitejs/vite/issues/4974)) ([1bd6d56](https://github.com/vitejs/vite/commit/1bd6d56bfd0a1133914fe23b384fafc9e232dc32))
* force overlay LTR ([#4943](https://github.com/vitejs/vite/issues/4943)) ([f8d8b73](https://github.com/vitejs/vite/commit/f8d8b73ae34e34813a51aed6ec34f69f0c77339f))
* handle sourcemap: false in transformWithEsbuild ([864d41d](https://github.com/vitejs/vite/commit/864d41d4eef745a68121c9192cda245630936431))
* normalize internal plugin names ([#4976](https://github.com/vitejs/vite/issues/4976)) ([37f0b2f](https://github.com/vitejs/vite/commit/37f0b2fff74109d381513ed052a32b43655ee11d))
* **ssr:** add normalizePath to require.resolve, fix [#2393](https://github.com/vitejs/vite/issues/2393) ([#4980](https://github.com/vitejs/vite/issues/4980)) ([417208c](https://github.com/vitejs/vite/commit/417208cf28cecc4cdfa04ca8f456d2b7c6b343d2))
* update *.wasm type (fix [#4835](https://github.com/vitejs/vite/issues/4835)) ([#4881](https://github.com/vitejs/vite/issues/4881)) ([5e1b8d4](https://github.com/vitejs/vite/commit/5e1b8d41f0540e4cad93aa539a19b5c599ff690c))
* use pkgId to get relative path ([#4957](https://github.com/vitejs/vite/issues/4957)) ([#4961](https://github.com/vitejs/vite/issues/4961)) ([b9e837a](https://github.com/vitejs/vite/commit/b9e837a2aa2c1a7a8f93d4b19df9f72fd3c6fb09))
* websocket proxies not the same as http ([#4893](https://github.com/vitejs/vite/issues/4893)) ([9260848](https://github.com/vitejs/vite/commit/9260848ee7ca15ac5c1a91fce8755beb62269e0d))


### Features

* add resolve.preserveSymlinks option ([#4708](https://github.com/vitejs/vite/issues/4708)) ([b61b044](https://github.com/vitejs/vite/commit/b61b044d8fc957c0511ca7d33380ab60bad5754f))
* async script module support, close [#3163](https://github.com/vitejs/vite/issues/3163) ([#4864](https://github.com/vitejs/vite/issues/4864)) ([3984569](https://github.com/vitejs/vite/commit/398456966df54fa8f74c3cfa42cadeb7540792ff))
* export transformWithEsbuild ([#4882](https://github.com/vitejs/vite/issues/4882)) ([c8c0f74](https://github.com/vitejs/vite/commit/c8c0f74ceda612bf2780dd764e941514547cb63b))
* **html:** Inline entry chunk when possible ([#4555](https://github.com/vitejs/vite/issues/4555)) ([e687d98](https://github.com/vitejs/vite/commit/e687d9886fd351d9941fc0a1a4c754440a94335f))


### Performance Improvements

* report compressed size using gzip instead of brotli due to drastic ([deb84c0](https://github.com/vitejs/vite/commit/deb84c0b053b5c1e6a4162a224108d1d853dbb04))



## [2.5.7](https://github.com/vitejs/vite/compare/v2.5.6...v2.5.7) (2021-09-13)


### Bug Fixes

* compute getPkgName only when used ([#4729](https://github.com/vitejs/vite/issues/4729)) ([ce29273](https://github.com/vitejs/vite/commit/ce292735f538556996540d764e4024fcb9dc9ac7))
* **css:** return sourcemap in vite:css transform ([#4880](https://github.com/vitejs/vite/issues/4880)) ([015290a](https://github.com/vitejs/vite/commit/015290a169d5ca3806aa0b2eb417426d61df9b7d))
* **esbuildDepPlugin:** externalize built-in module during SSR ([#4904](https://github.com/vitejs/vite/issues/4904)) ([5cc4587](https://github.com/vitejs/vite/commit/5cc458753171e88bb56fa49dbbf5c87a19d0294f))
* the base is duplicated in `importAnalysisBuild.ts` ([#4740](https://github.com/vitejs/vite/issues/4740)) ([7e929ae](https://github.com/vitejs/vite/commit/7e929ae4932ef89e56b92acdd46856ae41171302))


### Features

* allow `apply` condition to be a function ([#4857](https://github.com/vitejs/vite/issues/4857)) ([f19282f](https://github.com/vitejs/vite/commit/f19282f003f64093518290a61446403b1f022d18))
* **ssr:** exports `dynamicDeps` for ssrTransform, close [#4898](https://github.com/vitejs/vite/issues/4898) ([#4909](https://github.com/vitejs/vite/issues/4909)) ([9e51a76](https://github.com/vitejs/vite/commit/9e51a76b3fce27cb0a4a4ae558c4499e9dd540cd))



## [2.5.6](https://github.com/vitejs/vite/compare/v2.5.5...v2.5.6) (2021-09-08)


### Bug Fixes

* **importAnalysis:** properly inherit dependency version query for self imports ([c7c39b1](https://github.com/vitejs/vite/commit/c7c39b133bc06627932741a4622fb8ab5c904d97))
* use debugger for package resolution warnings ([#4873](https://github.com/vitejs/vite/issues/4873)) ([38de2c9](https://github.com/vitejs/vite/commit/38de2c9fe530f4c0074f0b3473ce2ced97dda31b))



## [2.5.5](https://github.com/vitejs/vite/compare/v2.5.4...v2.5.5) (2021-09-08)


### Bug Fixes

* **hmr:** should break on first matched plugin that performs custom hmr handling ([b3b8c61](https://github.com/vitejs/vite/commit/b3b8c61b37f36713605d61baeb98cfc0deb0b020))



## [2.5.4](https://github.com/vitejs/vite/compare/v2.5.3...v2.5.4) (2021-09-07)


### Bug Fixes

* check for Blob before creating worker URL, close [#4462](https://github.com/vitejs/vite/issues/4462) ([#4674](https://github.com/vitejs/vite/issues/4674)) ([311026f](https://github.com/vitejs/vite/commit/311026f0eb327874ca43e3ecccb9a9916f0850fb))
* **css:** loadPreprocessor tolerate `require.resolve.paths` not exists ([#4853](https://github.com/vitejs/vite/issues/4853)) ([c588b8f](https://github.com/vitejs/vite/commit/c588b8fd4cbef6a29a8b62985f7cfb53fb1f6fb7))
* handle error in numberToPos and formatError ([#4782](https://github.com/vitejs/vite/issues/4782)) ([c87763c](https://github.com/vitejs/vite/commit/c87763c1418d1ba876eae13d139eba83ac6f28b2))
* **overlay:** handle missing customElements ([#4856](https://github.com/vitejs/vite/issues/4856)) ([e5b472d](https://github.com/vitejs/vite/commit/e5b472d12e4bdaf7c0a2bd4015e73b40a716dac8))
* sometimes THIS_IS_UNDEFINED warnings were still shown ([#4844](https://github.com/vitejs/vite/issues/4844)) ([8d956f6](https://github.com/vitejs/vite/commit/8d956f6e585bed9ce4f02b7c9fed6631144f638d))



## [2.5.3](https://github.com/vitejs/vite/compare/v2.5.2...v2.5.3) (2021-09-01)


### Bug Fixes

* apply SSR externalization heuristic to devDependencies ([#4699](https://github.com/vitejs/vite/issues/4699)) ([0f1d6be](https://github.com/vitejs/vite/commit/0f1d6be100e3d6fda391b024ec14d2b4091993cb))
* **resolve:** normalize optimized resolved path ([#4813](https://github.com/vitejs/vite/issues/4813)) ([fa6475f](https://github.com/vitejs/vite/commit/fa6475fd4230fb2ab200485bc35b136b2474abfd))



## [2.5.2](https://github.com/vitejs/vite/compare/v2.5.1...v2.5.2) (2021-08-31)


### Bug Fixes

* decode url for middleware ([#4728](https://github.com/vitejs/vite/issues/4728)) ([824d042](https://github.com/vitejs/vite/commit/824d042535033a5c3d7006978c0d05c201cd1c25))
* don't transform new URL(url, import.meta.url) in comments ([#4732](https://github.com/vitejs/vite/issues/4732)) ([bf0b631](https://github.com/vitejs/vite/commit/bf0b631e7479ed70d02b98b780cf7e4b02d0344b))
* prevent pre-bundling @vite/client and @vite/env ([#4716](https://github.com/vitejs/vite/issues/4716)) ([e8c1906](https://github.com/vitejs/vite/commit/e8c19069984835114084dbc650f2a01335d6365f))
* special handling for ssr.noExternal in mergeConfig ([#4766](https://github.com/vitejs/vite/issues/4766)) ([689a2c8](https://github.com/vitejs/vite/commit/689a2c8cbab0887dba0994dd0e9dc5515ab9d461))
* **ssr:** resolve .cjs file extensions ([#4772](https://github.com/vitejs/vite/issues/4772)) ([96712ad](https://github.com/vitejs/vite/commit/96712adf5a404dbafa9b6ca4abd83ac98d5ce356))
* unexpected file request with custom publicDir, fix [#4629](https://github.com/vitejs/vite/issues/4629) ([#4631](https://github.com/vitejs/vite/issues/4631)) ([7be6c0c](https://github.com/vitejs/vite/commit/7be6c0c90a6224d3525af9c44b29ba48ef63ebf2))


### Features

* add `.pdf` to list of known asset types ([#4752](https://github.com/vitejs/vite/issues/4752)) ([d891641](https://github.com/vitejs/vite/commit/d891641ab2be85e151d86dfd1720c05a63dec51d))
* allow custom vite env prefix ([#4676](https://github.com/vitejs/vite/issues/4676)) ([dfdb9cc](https://github.com/vitejs/vite/commit/dfdb9cc41197a750850b60c36a9f6855c4481168))
* allow use of clientPort without middlewareMode ([#4332](https://github.com/vitejs/vite/issues/4332)) ([da0abc5](https://github.com/vitejs/vite/commit/da0abc59935febdd7522941100d235c84c08d5b4))
* **optimizer:** nested optimization ([#4634](https://github.com/vitejs/vite/issues/4634)) ([f61ec46](https://github.com/vitejs/vite/commit/f61ec46a077b92f5b1ce99bdac472a4c32052a13))



## [2.5.1](https://github.com/vitejs/vite/compare/v2.5.0...v2.5.1) (2021-08-24)


### Bug Fixes

* __DEFINES__ is not defined is env ([#4694](https://github.com/vitejs/vite/issues/4694)) ([ff50c22](https://github.com/vitejs/vite/commit/ff50c22f9c71ac968f0fc4503e892452ccdf5ef5))
* `Matcher` for chokidar WatchOptions#ignored ([#4616](https://github.com/vitejs/vite/issues/4616)) ([89e7a41](https://github.com/vitejs/vite/commit/89e7a419d7108dc3344d0bc5690798f695a46fd1))
* enable failing dependencies to be optimised by pre-processing them with esbuild ([#4275](https://github.com/vitejs/vite/issues/4275)) ([ea98a1a](https://github.com/vitejs/vite/commit/ea98a1a1d257d235d3f12948d049c66e6a941362))
* **css:** minify css will transform rgba to #rrggbbaa ([#4658](https://github.com/vitejs/vite/issues/4658)) ([632a50a](https://github.com/vitejs/vite/commit/632a50acd693f4ba79af7d22f1df14cf20e66538))
* CSS dependencies are tracked incorrectly when base is set ([#4592](https://github.com/vitejs/vite/issues/4592)) ([633c03a](https://github.com/vitejs/vite/commit/633c03aa05755da47c2f2e00aa52f3f6460ac382))
* **css:** dynamic import css abnormal after build ([#3333](https://github.com/vitejs/vite/issues/3333)) ([b572f57](https://github.com/vitejs/vite/commit/b572f57ec067abfaa1355cab3efdadf306592202))
* **scan:** do not match 'export default' in comments ([#4602](https://github.com/vitejs/vite/issues/4602)) ([8b85f5f](https://github.com/vitejs/vite/commit/8b85f5f5cc72b8d50416ab0ab5ae045119e944be))
* **vite:** unexptected overwriting for default export fix([#4553](https://github.com/vitejs/vite/issues/4553)) ([#4596](https://github.com/vitejs/vite/issues/4596)) ([c7929ad](https://github.com/vitejs/vite/commit/c7929ad1f96f1dd4f59e55626cedd6254add8538))
* surface exception when failing to resolve package entry ([#4426](https://github.com/vitejs/vite/issues/4426)) ([f75e508](https://github.com/vitejs/vite/commit/f75e5080c0e479c4b8d66f48da06417e0a180016))


### Features

* Add `ssr.noExternal = true` option ([#4490](https://github.com/vitejs/vite/issues/4490)) ([963387a](https://github.com/vitejs/vite/commit/963387adbbceaf0336f8b4c9661f76511c0094ac))
* make redirect easier when visit a non-based page ([#4618](https://github.com/vitejs/vite/issues/4618)) ([b97afa7](https://github.com/vitejs/vite/commit/b97afa76ec0b6ccd6e7dd99a254e109f67692bf7))



# [2.5.0](https://github.com/vitejs/vite/compare/v2.5.0-beta.3...v2.5.0) (2021-08-16)



# [2.5.0-beta.3](https://github.com/vitejs/vite/compare/v2.5.0-beta.2...v2.5.0-beta.3) (2021-08-14)


### Bug Fixes

* add ?inline css query typings ([#4570](https://github.com/vitejs/vite/issues/4570)) ([c8a17a2](https://github.com/vitejs/vite/commit/c8a17a23de4cde5d8d523ebc1b437e5b191446dd))
* skip optimizer run on non-JS script tags ([#4565](https://github.com/vitejs/vite/issues/4565)) ([270bd3a](https://github.com/vitejs/vite/commit/270bd3a72dbf8dfb839909545659dde1d14e1e38))
* support dangling comma and throw on circular dependency in tsconfig ([#4590](https://github.com/vitejs/vite/issues/4590)) ([f318416](https://github.com/vitejs/vite/commit/f3184161fde7df614b584520ddef5d7f049a5ff0))



# [2.5.0-beta.2](https://github.com/vitejs/vite/compare/v2.5.0-beta.1...v2.5.0-beta.2) (2021-08-09)


### Bug Fixes

* **client:** vite-error-overlay customElement is registered twice ([#4475](https://github.com/vitejs/vite/issues/4475)) ([28a9612](https://github.com/vitejs/vite/commit/28a9612d65f9004d6a3c698f86f7b22796347768))
* add missing assets to `packages/vite/client.d.ts` ([#4516](https://github.com/vitejs/vite/issues/4516)) ([420d82d](https://github.com/vitejs/vite/commit/420d82dc31c930fd82c28612e3dd864f35278503))
* avoid crash when a file imported in SCSS does not exist ([#4505](https://github.com/vitejs/vite/issues/4505)) ([a03e944](https://github.com/vitejs/vite/commit/a03e94419ef4da3b842f0211536afb1501bc0919))


### Features

* add asset name ([#3028](https://github.com/vitejs/vite/issues/3028)) ([#3050](https://github.com/vitejs/vite/issues/3050)) ([a055938](https://github.com/vitejs/vite/commit/a05593894bb76ac46897c6833dffed04de71b960))
* import `.webmanifest` assets as URL ([#4515](https://github.com/vitejs/vite/issues/4515)) ([8c5ac3f](https://github.com/vitejs/vite/commit/8c5ac3f89c69717b3bddedc229b77fabb9239085))
* log a warning if dependency pre-bundling cannot be run ([#4546](https://github.com/vitejs/vite/issues/4546)) ([120f3b9](https://github.com/vitejs/vite/commit/120f3b97456597998b29413e8eec5e7ad41f2e7a))



# [2.5.0-beta.1](https://github.com/vitejs/vite/compare/v2.5.0-beta.0...v2.5.0-beta.1) (2021-08-04)


### Bug Fixes

* change the preview default mode from `development` to `production` ([#4483](https://github.com/vitejs/vite/issues/4483)) ([77933ba](https://github.com/vitejs/vite/commit/77933ba86e7b15cb32ba80c27ae707db2a598cec))
* close vite dev server before creating new one ([#4374](https://github.com/vitejs/vite/issues/4374)) ([9e4572e](https://github.com/vitejs/vite/commit/9e4572edf5a21db9ed2d5ffa9c1a54dbea3687b3))
* register files added by addWatchFile() as current module's dependency ([db4ba56](https://github.com/vitejs/vite/commit/db4ba56e38a2ce7fa4a4ecf52d9eb0f375073560)), closes [#3216](https://github.com/vitejs/vite/issues/3216)


### Features

* add `logger.hasErrorLogged(error)` method ([#3957](https://github.com/vitejs/vite/issues/3957)) ([fb406ce](https://github.com/vitejs/vite/commit/fb406ce4c0fe6da3333c9d1c00477b2880d46352))



# [2.5.0-beta.0](https://github.com/vitejs/vite/compare/v2.4.4...v2.5.0-beta.0) (2021-08-03)


### Bug Fixes

* mixed match result of importMetaUrl ([#4482](https://github.com/vitejs/vite/issues/4482)) ([86f673a](https://github.com/vitejs/vite/commit/86f673abf4af38ab7a1e408f96e3447fdfcc5396))
* **build:** respect rollup output.assetFileNames, fix [#2944](https://github.com/vitejs/vite/issues/2944) ([#4352](https://github.com/vitejs/vite/issues/4352)) ([cbd0458](https://github.com/vitejs/vite/commit/cbd04588a2fe62e689fc5f7bb0b71610b88f2a3e))
* **deps:** update all non-major dependencies ([#4468](https://github.com/vitejs/vite/issues/4468)) ([cd54a22](https://github.com/vitejs/vite/commit/cd54a22b8d5048f5d25a9954697f49b6d65dcc1f))
* **html:** cover more cases in bodyPrependInjectRE ([#4474](https://github.com/vitejs/vite/issues/4474)) ([40c51e1](https://github.com/vitejs/vite/commit/40c51e16802d39fef03d145bfc3a5089867dd8cb))
* **server:** keep port when modifying the config file ([#4460](https://github.com/vitejs/vite/issues/4460)) ([056b17e](https://github.com/vitejs/vite/commit/056b17eb82becd08217346dddb47f8ecbf55fe3f))
* config port timing, fix [#4094](https://github.com/vitejs/vite/issues/4094) ([#4104](https://github.com/vitejs/vite/issues/4104)) ([6b98fdd](https://github.com/vitejs/vite/commit/6b98fddd84545a8500ac7767c514c6ce3bf3bf96))
* overwrite configEnv.mode if the user explicitly set mode option (fix [#4441](https://github.com/vitejs/vite/issues/4441)) ([#4437](https://github.com/vitejs/vite/issues/4437)) ([7d340a6](https://github.com/vitejs/vite/commit/7d340a6339cb5497ef54d3684697c4660ab97302))
* update dependency @rollup/plugin-commonjs to v20, fix [#2623](https://github.com/vitejs/vite/issues/2623) ([#4469](https://github.com/vitejs/vite/issues/4469)) ([f9e5d63](https://github.com/vitejs/vite/commit/f9e5d638431dc27619d0cafdd7ea0dd8543133d3))
* **scan:** improve import regex and allow multiline comments ([#4088](https://github.com/vitejs/vite/issues/4088)) ([76dbef6](https://github.com/vitejs/vite/commit/76dbef62741d4a53be1e6e8a0e04d3727759cc93))
* @vite/client http request is 404 not found ([#4187](https://github.com/vitejs/vite/issues/4187)) ([21ecdac](https://github.com/vitejs/vite/commit/21ecdacb40ba4fd1b8d248e1a1c99c21257f238d))
* import sass file even if not listed in package.json ([#3627](https://github.com/vitejs/vite/issues/3627)) ([a5b2b4f](https://github.com/vitejs/vite/commit/a5b2b4f11c5335828fd8179721aee73191df46e9))
* the return value of resolve by adding a namespace when processing a '@' in filter ([#3534](https://github.com/vitejs/vite/issues/3534)) ([d4e979f](https://github.com/vitejs/vite/commit/d4e979fbe70e2e7ab03407bd601b813e1671c144))
* **build:** fix define plugin spread operations ([#4397](https://github.com/vitejs/vite/issues/4397)) ([bd7c148](https://github.com/vitejs/vite/commit/bd7c1481cecf5eecc87a69ff8e8f54fa4bf4bfed))
* preserve base in HMR for CSS referenced in link tags ([#4407](https://github.com/vitejs/vite/issues/4407)) ([a06b26b](https://github.com/vitejs/vite/commit/a06b26b461dd05451c6c1ca20fce3b0e392c086e))


### Features

* **ssr:** tolerate circular imports ([#3950](https://github.com/vitejs/vite/issues/3950)) ([69f91a1](https://github.com/vitejs/vite/commit/69f91a1c03a129ab324c20fddfd2a07e729add96))
* implement custom logger ([#2521](https://github.com/vitejs/vite/issues/2521)) ([59841f0](https://github.com/vitejs/vite/commit/59841f0b65a2e554db964e530b18dcdc9b3b9586))
* **css:** support css module compose/from path resolution ([#4378](https://github.com/vitejs/vite/issues/4378)) ([690b35e](https://github.com/vitejs/vite/commit/690b35e857cea833ed4f1782e5c87b2b7064d072))
* minify css with esbuild, deprecate build.cleanCssOptions ([#4371](https://github.com/vitejs/vite/issues/4371)) ([4454688](https://github.com/vitejs/vite/commit/4454688bd8eda0217ec3c7397038bf3ece39b5b0))
* modulepreload polyfill ([#4058](https://github.com/vitejs/vite/issues/4058)) ([cb75dbd](https://github.com/vitejs/vite/commit/cb75dbd4a2b1c56e2a7aeaf1625818a4d1865f00))
* respect tsconfig options that affects compilation results ([#4279](https://github.com/vitejs/vite/issues/4279)) ([2986f6e](https://github.com/vitejs/vite/commit/2986f6ec78818910675b7d4f81b3dbd6ca51143a))



## [2.4.4](https://github.com/vitejs/vite/compare/v2.4.3...v2.4.4) (2021-07-27)


### Bug Fixes

* **deps:** update all non-major dependencies ([#4387](https://github.com/vitejs/vite/issues/4387)) ([2f900ba](https://github.com/vitejs/vite/commit/2f900ba4d4ad8061e0046898e8d1de3129e7f784))
* --https get ignored in preview ([#4318](https://github.com/vitejs/vite/issues/4318)) ([a870584](https://github.com/vitejs/vite/commit/a8705846f7f604263a64aece67deb7593c498dcd))
* don't interact with res if refresh has happened ([#4370](https://github.com/vitejs/vite/issues/4370)) ([c90b7d9](https://github.com/vitejs/vite/commit/c90b7d9d89a803b51d56f2885e5e61bbcf1c1c43))
* fix pre-bundling executes multiple times ([#3640](https://github.com/vitejs/vite/issues/3640)) ([41a00df](https://github.com/vitejs/vite/commit/41a00dff62ee2ae60099953b1d3cc91f7bad0d7d))
* handle imports from dot directories ([#3739](https://github.com/vitejs/vite/issues/3739)) ([f4f0100](https://github.com/vitejs/vite/commit/f4f0100649220453d961b6c66531c58026885680))
* ignore ENOENT in `injectSourcesContent` ([#2904](https://github.com/vitejs/vite/issues/2904)) ([0693d03](https://github.com/vitejs/vite/commit/0693d038e096dd4db3140507269c6aaeefd2186e))
* provide build load fallback for arbitrary request with queries ([f097aa1](https://github.com/vitejs/vite/commit/f097aa10c17faf0b73b239a34ca72934d38188d7))
* **css:** cachedPostcssConfig reused for multiple builds ([#3906](https://github.com/vitejs/vite/issues/3906)) ([3a97644](https://github.com/vitejs/vite/commit/3a9764403722a32b8d51222025e6516ef557e178))


### Features

* support ?inline css query to avoid css insertion ([e1de8a8](https://github.com/vitejs/vite/commit/e1de8a888ea9adb9dc415cf74aec43dfa83aa526))



## [2.4.3](https://github.com/vitejs/vite/compare/v2.4.2...v2.4.3) (2021-07-20)


### Bug Fixes

* call createFileOnlyEntry() only for CSS deps, fix [#4150](https://github.com/vitejs/vite/issues/4150) ([#4267](https://github.com/vitejs/vite/issues/4267)) ([89e3160](https://github.com/vitejs/vite/commit/89e3160d86bc8c27d6d33b82adec7c44016c3fc3))
* **dev:** only rewrite SSR stacktrace when possible ([#4248](https://github.com/vitejs/vite/issues/4248)) ([887c247](https://github.com/vitejs/vite/commit/887c247984abc0f80d8b19a1d681855944f6d01a))
* **util:** copyDir may cause an infinite loop ([#4310](https://github.com/vitejs/vite/issues/4310)) ([da64197](https://github.com/vitejs/vite/commit/da64197bc8bcd8f848aef3ae7a87a2d0d56ebd55))
* correctly ignore optional deps when bundling vite deps ([#4223](https://github.com/vitejs/vite/issues/4223)) ([b5ab77d](https://github.com/vitejs/vite/commit/b5ab77d878d7bdc5c68dbbf144395f2a590f7d99)), closes [#3977](https://github.com/vitejs/vite/issues/3977) [#3850](https://github.com/vitejs/vite/issues/3850)
* do not end process in middleware mode, fix [#4196](https://github.com/vitejs/vite/issues/4196) ([#4232](https://github.com/vitejs/vite/issues/4232)) ([1c994f8](https://github.com/vitejs/vite/commit/1c994f840e707e1085ee1e1aed0986bb92e39422))
* improve indent of built html file ([#4227](https://github.com/vitejs/vite/issues/4227)) ([0316f14](https://github.com/vitejs/vite/commit/0316f14eddb6854321ed0c1bbeb29c2668c6f08c))
* nested dependencies from sub node_modules, fix [#3254](https://github.com/vitejs/vite/issues/3254) ([#4091](https://github.com/vitejs/vite/issues/4091)) ([b465d3e](https://github.com/vitejs/vite/commit/b465d3eb87d415b2f484dae77daab57adc3415bf))


### Features

* `vite preview` port is used automatically `+1` ([#4219](https://github.com/vitejs/vite/issues/4219)) ([179a057](https://github.com/vitejs/vite/commit/179a0576b2b8da4fc0c32a574b8ae487b8b5265a))
* enable usage of function as library fileName, close [#3585](https://github.com/vitejs/vite/issues/3585) ([#3625](https://github.com/vitejs/vite/issues/3625)) ([772b2f7](https://github.com/vitejs/vite/commit/772b2f73b0da08181a7cc29e0eb50073ff3cc464))
* extract `config.base` in `importAnalysisBuild.ts` ([#4096](https://github.com/vitejs/vite/issues/4096)) ([ab59598](https://github.com/vitejs/vite/commit/ab59598f4e07a466d8319e6d81047f75517085db))
* library mode does not include preload ([#4097](https://github.com/vitejs/vite/issues/4097)) ([decc7d8](https://github.com/vitejs/vite/commit/decc7d885d108a3e96ffc82abcb4057f54aa6db5))



## [2.4.2](https://github.com/vitejs/vite/compare/v2.4.1...v2.4.2) (2021-07-12)


### Bug Fixes

* __VITE_PRELOAD__ replacement error ([#4163](https://github.com/vitejs/vite/issues/4163)) ([d377aae](https://github.com/vitejs/vite/commit/d377aae05f73779869ba84c91e050fe0a9f50dce)), closes [#3051](https://github.com/vitejs/vite/issues/3051)
* shutdown process after closing server ([#4082](https://github.com/vitejs/vite/issues/4082)) ([eac779c](https://github.com/vitejs/vite/commit/eac779c3d7c306288b01a35239e9eaaa2273c1a5))
* **build:** resolve license files correctly ([#4149](https://github.com/vitejs/vite/issues/4149)) ([bf32b41](https://github.com/vitejs/vite/commit/bf32b41bc4ac89e1fd39c27fb22c3bfa0a150152))
* **utils:** add dot-all flag to match all characters, fix [#3761](https://github.com/vitejs/vite/issues/3761) ([#3780](https://github.com/vitejs/vite/issues/3780)) ([b9cdfbe](https://github.com/vitejs/vite/commit/b9cdfbeedcd74d33c30cab9d38b1a9ca6d1cd8c2))


### Features

* cache certificate ([#3642](https://github.com/vitejs/vite/issues/3642)) ([5dd670f](https://github.com/vitejs/vite/commit/5dd670f06dc2b0928771d571ce6ca5164b0db8e9))



## [2.4.1](https://github.com/vitejs/vite/compare/v2.4.0...v2.4.1) (2021-07-06)


### Bug Fixes

* **hmr:** html registered as a PostCSS dependency, fix [#3716](https://github.com/vitejs/vite/issues/3716) ([#4127](https://github.com/vitejs/vite/issues/4127)) ([09c6c94](https://github.com/vitejs/vite/commit/09c6c94690ea3fc8b66bb6781995b3e15faedf8f))
* specify full filepath to importMeta.d.ts, fix [#4125](https://github.com/vitejs/vite/issues/4125) ([#4138](https://github.com/vitejs/vite/issues/4138)) ([3bc1d78](https://github.com/vitejs/vite/commit/3bc1d78843d970d367e235f6c30fd7996cf7335a))



# [2.4.0](https://github.com/vitejs/vite/compare/v2.4.0-beta.3...v2.4.0) (2021-07-05)



# [2.4.0-beta.3](https://github.com/vitejs/vite/compare/v2.4.0-beta.2...v2.4.0-beta.3) (2021-07-02)


### Bug Fixes

* **ssr:** Transform named default exports without altering scope ([#4053](https://github.com/vitejs/vite/issues/4053)) ([5211aaf](https://github.com/vitejs/vite/commit/5211aaf9b71022a1153dd3ccdef540fd51be72c0))
* add `type: "module"` hint to cache directory ([#4063](https://github.com/vitejs/vite/issues/4063)) ([58a29b2](https://github.com/vitejs/vite/commit/58a29b241662f77dbf971967b913f4e75f91fe26))
* allow preprocessor to be installed outside of the root directory ([#3988](https://github.com/vitejs/vite/issues/3988)) ([a0a80f8](https://github.com/vitejs/vite/commit/a0a80f8e992393f01b4b7377e7dc53059ddf1fe1))
* Avoid importing in source that __vitePreload has declared (close [#4016](https://github.com/vitejs/vite/issues/4016)) ([#4041](https://github.com/vitejs/vite/issues/4041)) ([bd34203](https://github.com/vitejs/vite/commit/bd34203bc40d6a406dfac3ab6cb41f5dfed63a77))
* ensure that esbuild uses the same working directory as Vite ([#4001](https://github.com/vitejs/vite/issues/4001)) ([19abafe](https://github.com/vitejs/vite/commit/19abafeedda8008f4cc9eeda4cf8cb46e57de8b9))
* fix esbuild break when importRe matches multiline import ([#4054](https://github.com/vitejs/vite/issues/4054)) ([eb2e41b](https://github.com/vitejs/vite/commit/eb2e41b098fb3d5f367c1f4fdfcad12f7538ac16))
* skip redirect and error fallback on middleware mode ([#4057](https://github.com/vitejs/vite/issues/4057)) ([d156a9f](https://github.com/vitejs/vite/commit/d156a9f364dddcfc41338f83e39db38a00a2ceb0))
* the current main branch code build the vite project error ([#4059](https://github.com/vitejs/vite/issues/4059)) ([4adc970](https://github.com/vitejs/vite/commit/4adc9706874581d2d5048fb48c135154591360cf))
* use `.mjs` extension for injected client modules ([#4061](https://github.com/vitejs/vite/issues/4061)) ([cca92c4](https://github.com/vitejs/vite/commit/cca92c47d54e0f96b56964f13fbe0b2d050c5ed9))
* use path type import, fix [#4028](https://github.com/vitejs/vite/issues/4028) ([#4031](https://github.com/vitejs/vite/issues/4031)) ([e092e89](https://github.com/vitejs/vite/commit/e092e899dad28f50aaa004419e9da50cf31db72d))



# [2.4.0-beta.2](https://github.com/vitejs/vite/compare/v2.4.0-beta.1...v2.4.0-beta.2) (2021-06-29)


### Bug Fixes

* revert resolve nested dependencies [#3753](https://github.com/vitejs/vite/issues/3753) ([#4019](https://github.com/vitejs/vite/issues/4019)) ([b6f4293](https://github.com/vitejs/vite/commit/b6f4293435bf90c9a64476d8bfbb022f4f2af9a9)), closes [#4005](https://github.com/vitejs/vite/issues/4005)
* **commonjs:** `ignoreDynamicRequires` should default to `false` ([#4015](https://github.com/vitejs/vite/issues/4015)) ([c08069c](https://github.com/vitejs/vite/commit/c08069cb3bdf7e7aa16d9cfaef4c1aea3a29cfa2)), closes [/github.com/vitejs/vite/pull/3353#issuecomment-851520683](https://github.com//github.com/vitejs/vite/pull/3353/issues/issuecomment-851520683) [#3426](https://github.com/vitejs/vite/issues/3426) [#3997](https://github.com/vitejs/vite/issues/3997)
* **css:** skip comma when matching css url ([#4004](https://github.com/vitejs/vite/issues/4004)) ([7d0bc26](https://github.com/vitejs/vite/commit/7d0bc2691f0291c3a9b0df992554f18bf85c8892))



# [2.4.0-beta.1](https://github.com/vitejs/vite/compare/v2.4.0-beta.0...v2.4.0-beta.1) (2021-06-29)


### Bug Fixes

* **hmr:** entry mod's importers contains css mod invalidate hmr ([#3929](https://github.com/vitejs/vite/issues/3929)) ([d97b33a](https://github.com/vitejs/vite/commit/d97b33a8cb9a72ed64244f239900a9a862b6ba68))
* **types:** correct import of types ([#4003](https://github.com/vitejs/vite/issues/4003)) ([4954636](https://github.com/vitejs/vite/commit/4954636c859fbfce76d02aea7881e59435fa3211))


### Features

* allow passing options to rollupjs dynamic import vars plugin ([#3047](https://github.com/vitejs/vite/issues/3047)) ([5507b4c](https://github.com/vitejs/vite/commit/5507b4c912d2e0e36e63488f5db8e9d1bb0a80f6))



# [2.4.0-beta.0](https://github.com/vitejs/vite/compare/v2.3.8...v2.4.0-beta.0) (2021-06-27)

### BREAKING CHANGES

- **server:** `server.fsServe` renamed to `server.fs` ([#3965](https://github.com/vitejs/vite/pull/3965))
- **server:** `server.fs.root` deprecated in favor of `server.fs.allow` ([#3968](https://github.com/vitejs/vite/pull/3968))

### Security

We have improved the file serving boundaries detection with ([#3784](https://github.com/vitejs/vite/issues/3784)). While it's still experimental and **disabled by default**, you can opt-in it by

```js
// vite.config.js
export default {
  server: {
    fs: {
      strict: true
    }
  }
}
```

It should smartly serve the files related to your project (directly imported, linked deps, etc.) while denying the rest. If you find any false-negative, please [open an issue](https://github.com/vitejs/vite/issues/new?assignees=&labels=pending+triage&template=bug_report.yml) with reproduction to report.

### Bug Fixes

* **build:** bundle non-inlined workers with rollup ([#2494](https://github.com/vitejs/vite/issues/2494)) ([18a2208](https://github.com/vitejs/vite/commit/18a22089df34c32daddf3b280c58f25cae73f722))
* resolve nested dependencies ([#3254](https://github.com/vitejs/vite/issues/3254)) ([#3753](https://github.com/vitejs/vite/issues/3753)) ([8467f64](https://github.com/vitejs/vite/commit/8467f64aee218dcb3135bb832ccaed36d647052f))
* **css:** file or contents missing error in build watch ([#3742](https://github.com/vitejs/vite/issues/3742)) ([#3747](https://github.com/vitejs/vite/issues/3747)) ([26b1b99](https://github.com/vitejs/vite/commit/26b1b9988db1ab980ca816d1914b26d6d3424502))
* **deps:** update all non-major dependencies ([#3878](https://github.com/vitejs/vite/issues/3878)) ([a66a805](https://github.com/vitejs/vite/commit/a66a8053e9520d20bcf95fce870570c5195bcc91))
* **scan:** 'for await' support in script setup for dev server ([#3889](https://github.com/vitejs/vite/issues/3889)) ([dd46cd1](https://github.com/vitejs/vite/commit/dd46cd1d030dcfffcbb2f20aff2b388cd18700f4))
* **scan:** avoid breaking html comment regex inside script of scanned html-like files ([bb095db](https://github.com/vitejs/vite/commit/bb095db11db5c7a12db6dcee866694f1f68d1e15))
* **ssr:** fix binding overwrite at nested function, fix [#3856](https://github.com/vitejs/vite/issues/3856) ([#3869](https://github.com/vitejs/vite/issues/3869)) ([85f51c1](https://github.com/vitejs/vite/commit/85f51c191d4d3317c5796e6c614ade6f7c21dddf))
* **ssr:** normalize manifest filenames ([#3706](https://github.com/vitejs/vite/issues/3706)) ([aa8ca3f](https://github.com/vitejs/vite/commit/aa8ca3f35218c9fb48f87d3f6f4681d379ee45ca)), closes [#3303](https://github.com/vitejs/vite/issues/3303)
* **ssr:** not flatten export * as (fix [#3934](https://github.com/vitejs/vite/issues/3934)) ([#3954](https://github.com/vitejs/vite/issues/3954)) ([7381d27](https://github.com/vitejs/vite/commit/7381d27564045a05cffbe4229d71d64b5a791042))
* **ssr:** not importing browser exports, fix [#3772](https://github.com/vitejs/vite/issues/3772) ([#3933](https://github.com/vitejs/vite/issues/3933)) ([f623ba3](https://github.com/vitejs/vite/commit/f623ba37dbc517656a7ffb10bc1b3cb221a4bc72))
* do not end server process in CI ([#3659](https://github.com/vitejs/vite/issues/3659)) ([5999444](https://github.com/vitejs/vite/commit/5999444496b6309460687b0769afad018aa21859))
* missing styles with build watch ([#3742](https://github.com/vitejs/vite/issues/3742)) ([#3887](https://github.com/vitejs/vite/issues/3887)) ([c9a6efe](https://github.com/vitejs/vite/commit/c9a6efe17108a899e1d1f4cb490973486223da99))
* multiple css url separation (fix [#3922](https://github.com/vitejs/vite/issues/3922)) ([#3926](https://github.com/vitejs/vite/issues/3926)) ([2d01e62](https://github.com/vitejs/vite/commit/2d01e62a70e534694ee1d87f4a328e796ae4c8fe))
* only downgrade target to es2019 when actually using terser ([bd8723e](https://github.com/vitejs/vite/commit/bd8723eb36be368b4a45240e1f0159fbd40a81a4))


### Features

* add client events to import.meta.hot.on ([#3638](https://github.com/vitejs/vite/issues/3638)) ([de1ddd4](https://github.com/vitejs/vite/commit/de1ddd401802784a74f5106c5173945e760d3f03))
* fs-serve import graph awareness ([#3784](https://github.com/vitejs/vite/issues/3784)) ([c45a02f](https://github.com/vitejs/vite/commit/c45a02f0279103be922a2d24b8cd05141e0ff165))
* generate inline sourcemaps for bundled vite.config.js files ([#3949](https://github.com/vitejs/vite/issues/3949)) ([cff2fcd](https://github.com/vitejs/vite/commit/cff2fcd8db98bb1c046816fd2e01dcbffbe86629))
* support for regex for ssr.noExternal ([#3819](https://github.com/vitejs/vite/issues/3819)) ([330c94c](https://github.com/vitejs/vite/commit/330c94c4355e4f091e6e4f46c6a47dbfba410e40))
* support new URL(url, import.meta.url) usage ([4cbb40d](https://github.com/vitejs/vite/commit/4cbb40d2f1a4050c9944e7e1d9e0f5b204b7e37b))



## [2.3.8](https://github.com/vitejs/vite/compare/v2.3.7...v2.3.8) (2021-06-19)


### Bug Fixes

* **css:** filter out function name suffixes with url ([#3752](https://github.com/vitejs/vite/issues/3752)) ([9aa255a](https://github.com/vitejs/vite/commit/9aa255a0abcb9f5b23c34607b2188f796f4b6c94))
* **deps:** update all non-major dependencies ([#3791](https://github.com/vitejs/vite/issues/3791)) ([74d409e](https://github.com/vitejs/vite/commit/74d409eafca8d74ec4a6ece621ea2895bc1f2a32))
* **hmr:** always invalidate all affected modules ([e048114](https://github.com/vitejs/vite/commit/e048114d3657fc8e2fec645eba3f5f2fe230ceb7))
* **hmr:** avoid css propagation infinite loop ([7362e6e](https://github.com/vitejs/vite/commit/7362e6e9a7a0f0177b467f1cf80552acf22c46a0))
* **hmr:** avoid duplicated modules for css dependency ([385ced9](https://github.com/vitejs/vite/commit/385ced9c2e9b5f06e9c06669fe19a0a98cc82c8b))
* **hmr/css:** check CSS importers for hmr boundaries - fix Tailwind 2.2 compat ([6eaec3a](https://github.com/vitejs/vite/commit/6eaec3ab74d126310d93f8a93f8577bed1c3f474))
* **hmr/css:** fix infinite recursion on hmr ([#3865](https://github.com/vitejs/vite/issues/3865)) ([0d5726f](https://github.com/vitejs/vite/commit/0d5726fff2fe724ffec3c0621e3dcd6775b0fe8b))
* ?import with trailing = added by some servers ([#3805](https://github.com/vitejs/vite/issues/3805)) ([460d1cd](https://github.com/vitejs/vite/commit/460d1cda317e4c4d03434f2b3d8de9152620005b))
* don't replace `process.env` if `process` not global variable ([#3703](https://github.com/vitejs/vite/issues/3703)) ([5aeadb7](https://github.com/vitejs/vite/commit/5aeadb719944152be7ed9f9472aa2238ea3557c0))
* upgrade esbuild for esm compatibility ([#3718](https://github.com/vitejs/vite/issues/3718)) ([dbb5eab](https://github.com/vitejs/vite/commit/dbb5eabe246747abab187a6c8d90cd418856e048)), closes [#3399](https://github.com/vitejs/vite/issues/3399) [#3413](https://github.com/vitejs/vite/issues/3413)


### Features

* allow 'hidden' sourcemap to remove //# sourceMappingURL from generated maps ([#3684](https://github.com/vitejs/vite/issues/3684)) ([19e479b](https://github.com/vitejs/vite/commit/19e479ba0dd1da4d1de075bdf11edabe00af6cb6))



## [2.3.7](https://github.com/vitejs/vite/compare/v2.3.6...v2.3.7) (2021-06-08)


### Bug Fixes

* Include src files in vite npm bundle (for sourcemaps) ([#3656](https://github.com/vitejs/vite/issues/3656)) ([294d8b4](https://github.com/vitejs/vite/commit/294d8b472ca5d5079d8fe35ecb1b0bf6cf7720db))
* show error message above the stack when HMR overlay is disabled ([#3677](https://github.com/vitejs/vite/issues/3677)) ([6b4c355](https://github.com/vitejs/vite/commit/6b4c3550f673253ca175a1e2ca2efb8d1ec85b3b))
* tolerant fs error in formatError ([#3665](https://github.com/vitejs/vite/issues/3665)) ([5146cc5](https://github.com/vitejs/vite/commit/5146cc5eb2bfe4317e3a7c8590963cbebaa5b3e9))
* update `sirv` to decode url in preview ([#3680](https://github.com/vitejs/vite/issues/3680)) ([0430127](https://github.com/vitejs/vite/commit/0430127b7b7216d92a351fcb9c80753563a318e6))


### Features

* **css:** support postcss dir-dependency message type ([#3707](https://github.com/vitejs/vite/issues/3707)) ([665d438](https://github.com/vitejs/vite/commit/665d43872914c7a79a5a79aa4b6349961e68a10d))



## [2.3.6](https://github.com/vitejs/vite/compare/v2.3.5...v2.3.6) (2021-06-02)


### Bug Fixes

* revert avoid css leaking into emitted javascript ([#3402](https://github.com/vitejs/vite/issues/3402)) ([#3630](https://github.com/vitejs/vite/issues/3630)) ([91eb2a6](https://github.com/vitejs/vite/commit/91eb2a6bc30103569cce05f6da1acdd72d5f71f0))
* **types:** add '*?.sharedworker' typing ([#3618](https://github.com/vitejs/vite/issues/3618)) ([690ff99](https://github.com/vitejs/vite/commit/690ff999cdebf390a84506c5b62a17e6e8f47c17))



## [2.3.5](https://github.com/vitejs/vite/compare/v2.3.4...v2.3.5) (2021-06-01)


### Bug Fixes

* cannot recognize JS url correctly([#3568](https://github.com/vitejs/vite/issues/3568)) ([#3572](https://github.com/vitejs/vite/issues/3572)) ([ab08652](https://github.com/vitejs/vite/commit/ab0865223f2fd8c460ee9b5108dbe67b9ad534a1))
* **tests:** fix tests run fail in the Chinese directory ([#3586](https://github.com/vitejs/vite/issues/3586)) ([3cab2c2](https://github.com/vitejs/vite/commit/3cab2c2202c2c7188b4f76d872c94a9f6acaf122))
* update esbuild to 0.12 ([#3570](https://github.com/vitejs/vite/issues/3570)) ([421c530](https://github.com/vitejs/vite/commit/421c530eae668f0ddadd9b4ef6d366a58d74febc))


### Features

* **config:** add `envDir` option ([#3407](https://github.com/vitejs/vite/issues/3407)) ([472ba5d](https://github.com/vitejs/vite/commit/472ba5d7198e5db631ddafc1fd2adf78ce26003e))
* **plugins/worker:** support SharedWorker (resolve [#2093](https://github.com/vitejs/vite/issues/2093)) ([#2505](https://github.com/vitejs/vite/issues/2505)) ([d78191c](https://github.com/vitejs/vite/commit/d78191c5ce5f9c0e5a2329c7b113fc25b27535b9))
* **ssr:** include non-CSS assets in the manifest ([#3556](https://github.com/vitejs/vite/issues/3556)) ([adc7170](https://github.com/vitejs/vite/commit/adc7170dac0b08f3cffd49fa4844a6fa871067dc))
* added clientPort to HmrOptions ([#3578](https://github.com/vitejs/vite/issues/3578)) ([7db69a3](https://github.com/vitejs/vite/commit/7db69a3c284d58ebb51f91c5f44da9890d056b19))



## [2.3.4](https://github.com/vitejs/vite/compare/v2.3.3...v2.3.4) (2021-05-25)


### Bug Fixes

* allow passing an array as sass / scss importer ([#3529](https://github.com/vitejs/vite/issues/3529)) ([e344cdd](https://github.com/vitejs/vite/commit/e344cdd28425e08b2481b1a6289b820764f25928))
* avoid css leaking into emitted javascript ([#3402](https://github.com/vitejs/vite/issues/3402)) ([65d333d](https://github.com/vitejs/vite/commit/65d333d8eb95ea3ab3d611d9c21d05de9657f134))
* clean manifest plugin state at build start ([#3530](https://github.com/vitejs/vite/issues/3530)) ([c9da635](https://github.com/vitejs/vite/commit/c9da635841cc20e65df6a51c3f0b7a7fb79a814f))
* data-uri plugin cache reset at buildStart ([#3537](https://github.com/vitejs/vite/issues/3537)) ([9d97b6d](https://github.com/vitejs/vite/commit/9d97b6d0084a543b6e692890d8a095e4bee5dfac))
* do not cache module while the file contains import.meta.glob ([#3005](https://github.com/vitejs/vite/issues/3005)) ([e7b8f41](https://github.com/vitejs/vite/commit/e7b8f41c45ea95cfd12801dfd22fa9be99de8ac8))
* ensure new assets cache at build start, fix [#3271](https://github.com/vitejs/vite/issues/3271) ([#3512](https://github.com/vitejs/vite/issues/3512)) ([9484c0f](https://github.com/vitejs/vite/commit/9484c0f392407d71efad64b585b8656202c9b411))
* ensure new CSS modules cache at build start ([#3516](https://github.com/vitejs/vite/issues/3516)) ([07ad2b4](https://github.com/vitejs/vite/commit/07ad2b494b14701f54376afe6ce49bf24a3e7cd9))
* **preview:** [#3487](https://github.com/vitejs/vite/issues/3487) preview should serve latest content by default ([#3488](https://github.com/vitejs/vite/issues/3488)) ([9a4183d](https://github.com/vitejs/vite/commit/9a4183dbc0d4dcf278ac829b96230b3d2b24bd5e))
* **preview:** allow to disable HTTPS ([#3514](https://github.com/vitejs/vite/issues/3514)) ([cf1632e](https://github.com/vitejs/vite/commit/cf1632ea525b4e3230afaee908ef42f0e7321fe8))
* **preview:** support custom hostname ([#3506](https://github.com/vitejs/vite/issues/3506)) ([5979d0e](https://github.com/vitejs/vite/commit/5979d0e3b2c071ee15408aa67974af04f7bb1c3d))
* **types:** add .module.pcss typings, fix [#3518](https://github.com/vitejs/vite/issues/3518) ([#3519](https://github.com/vitejs/vite/issues/3519)) ([3475351](https://github.com/vitejs/vite/commit/3475351a371df2e17689a99968fdee827b0b2d16))
* handle HMR for files with more than one glob import ([#3497](https://github.com/vitejs/vite/issues/3497)) ([05bd96e](https://github.com/vitejs/vite/commit/05bd96e21ced682251378c4ad7ae0dee59195eae))
* inline webworker safari support ([#3468](https://github.com/vitejs/vite/issues/3468)) ([2671546](https://github.com/vitejs/vite/commit/26715465f7430e6fd9a0cf2ae9e49fb099cced3a))
* invalidate import globs upon new/removed files (fix [#3499](https://github.com/vitejs/vite/issues/3499)) ([#3500](https://github.com/vitejs/vite/issues/3500)) ([b31604e](https://github.com/vitejs/vite/commit/b31604e08c4333bed5a3c4cc6876d1eb337a100b))
* track deps for css [@import](https://github.com/import) in build watch mode, fix [#3387](https://github.com/vitejs/vite/issues/3387) ([#3478](https://github.com/vitejs/vite/issues/3478)) ([13bda33](https://github.com/vitejs/vite/commit/13bda3368e73ade311f1c113894c2dcb329cef8d))


### Features

* support serving `index.html` in middleware mode ([#2871](https://github.com/vitejs/vite/issues/2871)) ([b1598ce](https://github.com/vitejs/vite/commit/b1598cec7ee185f796d8679f0a97d36b80fe1949))



## [2.3.3](https://github.com/vitejs/vite/compare/v2.3.2...v2.3.3) (2021-05-17)


### Bug Fixes

* ignore ids that start with \0 in plugin asset, fix [#3424](https://github.com/vitejs/vite/issues/3424) ([#3436](https://github.com/vitejs/vite/issues/3436)) ([f6cfe30](https://github.com/vitejs/vite/commit/f6cfe30abfc5179262aea807173d7591fd4dc876))
* restore dynamic-import-polyfill ([#3434](https://github.com/vitejs/vite/issues/3434)) ([4112c5d](https://github.com/vitejs/vite/commit/4112c5d103673b83c50d446096086617dfaac5a3))
* sass importer can't be undefined (fix: [#3390](https://github.com/vitejs/vite/issues/3390)) ([#3395](https://github.com/vitejs/vite/issues/3395)) ([30ff5a2](https://github.com/vitejs/vite/commit/30ff5a235d2a832cb45a761a03c5947460417b40))
* skip fs fallback for out of root urls, fix [#3364](https://github.com/vitejs/vite/issues/3364) ([#3431](https://github.com/vitejs/vite/issues/3431)) ([19dae99](https://github.com/vitejs/vite/commit/19dae997f91607424af2d0e159ae2570463bbcb3))
* warn about dynamic import polyfill only during build ([#3446](https://github.com/vitejs/vite/issues/3446)) ([5fe0550](https://github.com/vitejs/vite/commit/5fe05507dd28bbd863469628bc61b45a04f938bd))



## [2.3.2](https://github.com/vitejs/vite/compare/v2.3.1...v2.3.2) (2021-05-12)


### Bug Fixes

* **css:** fix sass importer error ([#3368](https://github.com/vitejs/vite/issues/3368)) ([3f04abf](https://github.com/vitejs/vite/commit/3f04abf0ff21c7b2969902c3d8d87f4b1b93740f))
* **server:** hostname defaults to localhost, fix [#3355](https://github.com/vitejs/vite/issues/3355) ([#3383](https://github.com/vitejs/vite/issues/3383)) ([8b5a6a8](https://github.com/vitejs/vite/commit/8b5a6a855091e6f744cc7b886cf927d14dc74d50))



## [2.3.1](https://github.com/vitejs/vite/compare/v2.3.0...v2.3.1) (2021-05-12)

### Notable Changes

We introduced a security fix in v2.3.0 to restrict file access outside of the workspace root. We received reports of issues with symlinks and monorepo setups, so we are marking this feature as experimental and disabling it by default to avoid disruption in the ecosystem.

A new experimental option `server.fsServe.strict` was added defaulting to `false`. This **disables the restrictions by default**. The `fsServe` restrictions are going to be enabled by default in a future version, once the issues are been resolved and the logic becomes more robust. You can opt-in to this security change using (experimental)

```js
// vite.config.js
export default {
  server: {
    fsServe: {
      strict: true
    }
  }
}
```

### Bug Fixes

* bump @rollup/plugin-commonjs to v19, fix [#3312](https://github.com/vitejs/vite/issues/3312) ([#3353](https://github.com/vitejs/vite/issues/3353)) ([c6ef6d0](https://github.com/vitejs/vite/commit/c6ef6d084c2368f6c73e03cc18bcab05aea9cfa6))
* disable fsServe restrictions by default ([#3377](https://github.com/vitejs/vite/issues/3377)) ([5433a65](https://github.com/vitejs/vite/commit/5433a655534cd4c716c2eba2f89f20bfa328e812))
* normalize url in `ensureServingAccess` ([#3350](https://github.com/vitejs/vite/issues/3350)) ([deb465b](https://github.com/vitejs/vite/commit/deb465ba412312ccae2d5b767de327d6f8562e7e))
* use the closest package.json as root when workspace not found fo… ([#3374](https://github.com/vitejs/vite/issues/3374)) ([42b35ac](https://github.com/vitejs/vite/commit/42b35ac567b02b8142a7a51df320d7deb2ec4ac1))



# [2.3.0](https://github.com/vitejs/vite/compare/v2.2.4...v2.3.0) (2021-05-11)

## BREAKING CHANGES

- Browser default targets changed (PR [#2976](https://github.com/vitejs/vite/pull/2976))
    - Default browser support range has changed. The minimum requirement is now [native dynamic import support](https://caniuse.com/es6-module-dynamic-import). Most notably, this means support for legacy Microsoft Edge (16-18) has been dropped.
    - `vite/dynamic-import-polyfill` removed and no longer required in custom entries

### Why are there breaking changes in a minor?

- **Limited impact:** The affected target browsers are ones that natively support [ES6 modules](https://caniuse.com/es6-module) (92.83% of global usage) but do not support [native dynamic imports](https://caniuse.com/es6-module-dynamic-import) (92.34% of global usage). So this is a small range affecting only 0.49% of global usage.

    This number should continue to decrease in the future as most modern browsers are evergreen. You are also not affected if you are already targeting legacy browsers using `@vitejs/plugin-legacy`.

- **Easy migration:** if you do intend to support browsers that fall into this category, you can use [dynamic-import-polyfill](https://github.com/GoogleChromeLabs/dynamic-import-polyfill).

    To make the polyfill work, you will also need to use a plugin with [`renderDynamicImport`](https://rollupjs.org/guide/en/#renderdynamicimport) to change the import calls to `__import__`. You can follow the installation guide in [this example](https://github.com/antfu/vite-dynamic-import-polyfill-example).

- **Required for bug fixes:** This change is required for upgrading esbuild from v0.9 to [v0.11](https://github.com/evanw/esbuild/releases/tag/v0.11.0), which includes a lot of bug fixes and improvements. And it also allows us to remove the complexity of the dynamic import polyfill.

## Security Fixes

- Dev server only listens to localhost by default now (PR [#2977](https://github.com/vitejs/vite/pull/2977))
    - Pass `--host 0.0.0.0` to change back to the previous behavior.
- Dev server only serves files under workspace root by defualt (PR [#2850](https://github.com/vitejs/vite/pull/2850), [#3321](https://github.com/vitejs/vite/pull/3321))
    - Accessing files outside of workspace root will result in a 403 response.
    - Vite will try to search up for workspace root defined in `package.json` or `pnpm-workspace.yaml`
    - To set the workspace root explicitly, see [configurations](https://vitejs.dev/config/#server-fsserve-root)

### Bug Fixes

* **dev:** rewrite importee path at html files at spa fallback ([#3239](https://github.com/vitejs/vite/issues/3239)) ([13d41d8](https://github.com/vitejs/vite/commit/13d41d864219bcc0e952f42f69adb97147e15520))
* **hmr:** respect server https options when running as middleware ([#1992](https://github.com/vitejs/vite/issues/1992)) ([24178b0](https://github.com/vitejs/vite/commit/24178b05825245b9f36b5a8e4730996184cc7e8e))
* **serve:** prevent serving unrestricted files ([#3321](https://github.com/vitejs/vite/issues/3321)) ([7231b5a](https://github.com/vitejs/vite/commit/7231b5a882a2db8dd2d9cb88a0f446edb5e2cf43))
* only provide npm package names to resolveSSRExternal ([#2717](https://github.com/vitejs/vite/issues/2717)) ([6dde32a](https://github.com/vitejs/vite/commit/6dde32a1641e91470da73315272f14e62369b65b))
* prevent serving unrestricted files (fix [#2820](https://github.com/vitejs/vite/issues/2820)) ([#2850](https://github.com/vitejs/vite/issues/2850)) ([792a6e1](https://github.com/vitejs/vite/commit/792a6e1ee8fa288ce8e641f7fa378fe8d76e52d4))
* type error by [#3151](https://github.com/vitejs/vite/issues/3151) ([#3292](https://github.com/vitejs/vite/issues/3292)) ([fd4146b](https://github.com/vitejs/vite/commit/fd4146b8624100a609ae43b2d73681d260dfe131))
* upgrade to esbuild@0.11.19 ([#3282](https://github.com/vitejs/vite/issues/3282)) ([b0dd69d](https://github.com/vitejs/vite/commit/b0dd69d305c268b2ea326ec4f344da7f7b989e69))
* warning for vite/dynamic-import-polyfill ([#3328](https://github.com/vitejs/vite/issues/3328)) ([8b80512](https://github.com/vitejs/vite/commit/8b80512c03bc053e101b1047bfd142260a15e2ac))
* **ci:** fix ci lint step ([#2988](https://github.com/vitejs/vite/issues/2988)) ([4e8ffd8](https://github.com/vitejs/vite/commit/4e8ffd8865e6303d19b5a5ea4501fc54bff4e180))
* **resolve:** normalize node_modules and bare imports, fix [#2503](https://github.com/vitejs/vite/issues/2503) ([#2848](https://github.com/vitejs/vite/issues/2848)) ([0c97412](https://github.com/vitejs/vite/commit/0c9741222532b9fa7818e0a2ce9c918bda03c6a0))
* **server:** Listen only to 127.0.0.1 by default ([#2977](https://github.com/vitejs/vite/issues/2977)) ([1e604d5](https://github.com/vitejs/vite/commit/1e604d5b60900098f201f90394445fea55642e74))
* **ssr:** resolve dynamic import vars modules ([#3177](https://github.com/vitejs/vite/issues/3177)) ([b1e7395](https://github.com/vitejs/vite/commit/b1e73951ed402a64882fb771bf433938ad171e19))


### Features

* add optimizeDeps.esbuildOptions ([#2991](https://github.com/vitejs/vite/issues/2991)) ([77a882a](https://github.com/vitejs/vite/commit/77a882a385147957b3100b3ec21de7cb212887bf))
* set publicDir to false to disable copied static assets to build dist dir ([#3152](https://github.com/vitejs/vite/issues/3152)) ([f4ab90a](https://github.com/vitejs/vite/commit/f4ab90a79f3ff56647631fa8891dc665081b45a2))
* webworker ssr target ([#3151](https://github.com/vitejs/vite/issues/3151)) ([1c59ef1](https://github.com/vitejs/vite/commit/1c59ef14dec3b60c67e70800af9d88a2255a54ae))



## [2.2.4](https://github.com/vitejs/vite/compare/v2.2.3...v2.2.4) (2021-05-03)


### Bug Fixes

* **dev:** strip utf-8 bom ([#3162](https://github.com/vitejs/vite/issues/3162)) ([#3171](https://github.com/vitejs/vite/issues/3171)) ([19a2869](https://github.com/vitejs/vite/commit/19a28692209564202ce7303a5664696cfbf3ef28))
* call `buildStart` hook in middleware mode ([#3080](https://github.com/vitejs/vite/issues/3080)) ([c374a54](https://github.com/vitejs/vite/commit/c374a5405050a6ed9013082027774fa275c2d324))
* **scan:** improve script regular matching (fixes [#2942](https://github.com/vitejs/vite/issues/2942)) ([#2961](https://github.com/vitejs/vite/issues/2961)) ([1e785d1](https://github.com/vitejs/vite/commit/1e785d1af54ae5e305dd1bef9af513f2c3a91ad3))
* dependencies are analyzed multiple times ([#3154](https://github.com/vitejs/vite/issues/3154)) ([28a67ad](https://github.com/vitejs/vite/commit/28a67ad023fd7e43e3024d1a698c49a0f7156b59))
* **emptyOutDir:** never remove .git ([#3043](https://github.com/vitejs/vite/issues/3043)) ([82dc588](https://github.com/vitejs/vite/commit/82dc5880c97daca2b7b8d55c27c30a6d810849a1))


### Features

* Allow overwrite `TerserOptions.safari10` from `UserConfig` ([#3113](https://github.com/vitejs/vite/issues/3113)) ([7cd8d78](https://github.com/vitejs/vite/commit/7cd8d7832e12e2facf7dfc163320a8798e19c6fd))



## [2.2.3](https://github.com/vitejs/vite/compare/v2.2.2...v2.2.3) (2021-04-25)


### Bug Fixes

* revert [#2541](https://github.com/vitejs/vite/issues/2541), fix [#3084](https://github.com/vitejs/vite/issues/3084) [#3101](https://github.com/vitejs/vite/issues/3101) ([#3144](https://github.com/vitejs/vite/issues/3144)) ([f4e7918](https://github.com/vitejs/vite/commit/f4e7918d0784d4f20f7f9a5575cd7e4a9cfd69fb))
* **build:** vendor chunk strategy uses static imports, fix [#2672](https://github.com/vitejs/vite/issues/2672) ([#2934](https://github.com/vitejs/vite/issues/2934)) ([949b818](https://github.com/vitejs/vite/commit/949b8184310ac073faf7f5271301ad0d9a884487))
* add .svelte to list of known js src files ([#3128](https://github.com/vitejs/vite/issues/3128)) ([0f09eaf](https://github.com/vitejs/vite/commit/0f09eaff374065a866c0f23db1217704eeb637a6))
* await bundle close in worker plugin ([#2997](https://github.com/vitejs/vite/issues/2997)) ([0e7125a](https://github.com/vitejs/vite/commit/0e7125a0480d2a50cd1d88c7a8d046af75be3a75))
* dymamic import polyfill path when base is a URL ([#3132](https://github.com/vitejs/vite/issues/3132)) ([02ba4ba](https://github.com/vitejs/vite/commit/02ba4ba32cd40f1cc3943781022c05f9df3b57e6))
* handle null/empty sources in source maps ([#3074](https://github.com/vitejs/vite/issues/3074)) ([3e9f128](https://github.com/vitejs/vite/commit/3e9f128d15f154a2e140fa65c5f617824f0c4916))
* support postcss .pcss extension ([#3130](https://github.com/vitejs/vite/issues/3130)) ([6d602a0](https://github.com/vitejs/vite/commit/6d602a0a4d2c1e77ded1344d59733eb93d4009c3))



## [2.2.2](https://github.com/vitejs/vite/compare/v2.2.1...v2.2.2) (2021-04-24)


### Bug Fixes

* **ssr:** skip resolving browser field for SSR build, fix [#3036](https://github.com/vitejs/vite/issues/3036) ([#3039](https://github.com/vitejs/vite/issues/3039)) ([61ea320](https://github.com/vitejs/vite/commit/61ea32056048e902ca69d88e1b0a2d21660dae2a))


### Features

* add marko file extensions ([#3073](https://github.com/vitejs/vite/issues/3073)) ([d34fd88](https://github.com/vitejs/vite/commit/d34fd88e46cdcbbfbc266f431f47af285b1e8702))



## [2.2.1](https://github.com/vitejs/vite/compare/v2.2.0...v2.2.1) (2021-04-19)


### Bug Fixes

* **optimizer:** depScan resolve with flatIdDeps ([#3053](https://github.com/vitejs/vite/issues/3053)) ([cb441ef](https://github.com/vitejs/vite/commit/cb441ef0f5c4a21117ea42d3fcee110a62371196))



# [2.2.0](https://github.com/vitejs/vite/compare/v2.1.5...v2.2.0) (2021-04-19)


### Bug Fixes

* require.resolve to correct sub node_modules ([#3003](https://github.com/vitejs/vite/issues/3003)) ([da11d43](https://github.com/vitejs/vite/commit/da11d43d9a246b0e721d6c33cd6a47a0675843cf))
* **optimizer:** ensure consistency with replace define ([#2929](https://github.com/vitejs/vite/issues/2929)) ([ddb7a91](https://github.com/vitejs/vite/commit/ddb7a91f0085f832d438f9523397c8a55f3d0764)), closes [#2893](https://github.com/vitejs/vite/issues/2893)
* A static and dynamically imported module is loaded twice ([#2935](https://github.com/vitejs/vite/issues/2935)) ([266fb55](https://github.com/vitejs/vite/commit/266fb55adc1e3580bab86d30fcd1dfd1d80748a9))
* avoid endless loop in resolveSSRExternal (fix [#2635](https://github.com/vitejs/vite/issues/2635)) ([#2636](https://github.com/vitejs/vite/issues/2636)) ([59871ef](https://github.com/vitejs/vite/commit/59871ef16142412d78ec79fe5ed06390d86c49e6))
* don't resolve import using browser during SSR (fix [#2995](https://github.com/vitejs/vite/issues/2995)) ([#2996](https://github.com/vitejs/vite/issues/2996)) ([fd1c9ba](https://github.com/vitejs/vite/commit/fd1c9ba11bff634c10e23a9cad2e5d639145ccf6))
* filter out empty srcset, fix [#2863](https://github.com/vitejs/vite/issues/2863) ([#2888](https://github.com/vitejs/vite/issues/2888)) ([0d4f803](https://github.com/vitejs/vite/commit/0d4f803d6edc51f31a5e20a161aa77688823b689))
* **build:** avoid import duplicate chunks, fix [#2906](https://github.com/vitejs/vite/issues/2906) ([#2940](https://github.com/vitejs/vite/issues/2940)) ([8b02abf](https://github.com/vitejs/vite/commit/8b02abf537cb731fcfe84cf8e93ba3e923e83114))
* **build:** properly handle alias key in config merge ([#2847](https://github.com/vitejs/vite/issues/2847)) ([41261c7](https://github.com/vitejs/vite/commit/41261c70e6d65ddf1dca52a6e94e5aa555539581))
* **build:** support `cssCodeSplit` for cjs format, fix [#2575](https://github.com/vitejs/vite/issues/2575) ([#2621](https://github.com/vitejs/vite/issues/2621)) ([2a89c57](https://github.com/vitejs/vite/commit/2a89c57d3fb2dedbe595c4d49c454f3d138e6414))
* **css:** properly pass options to stylus compiler, fix [#2587](https://github.com/vitejs/vite/issues/2587) ([#2860](https://github.com/vitejs/vite/issues/2860)) ([8dbebee](https://github.com/vitejs/vite/commit/8dbebeed4c1dd13e13aa7201ad6922d4d4c20368))
* **define:** ensure the normal use of NODE_ENV, fix [#2759](https://github.com/vitejs/vite/issues/2759) ([#2764](https://github.com/vitejs/vite/issues/2764)) ([fa85749](https://github.com/vitejs/vite/commit/fa8574921195dd03b539c150a2ae5f97121a0aea))
* **scan:** avoid crawling type only import ([#2810](https://github.com/vitejs/vite/issues/2810)) ([daf7838](https://github.com/vitejs/vite/commit/daf783866b744c09e2b10234ced853c6f9a84dff))
* **ssr:** fix ssrTransform catch clause error (fix [#2667](https://github.com/vitejs/vite/issues/2667)) ([#2966](https://github.com/vitejs/vite/issues/2966)) ([c9e0bcf](https://github.com/vitejs/vite/commit/c9e0bcf5653c31ffa00819083a9ce58a24e0bd17))
* **types:** clean-css types ([#2971](https://github.com/vitejs/vite/issues/2971)) ([9be7449](https://github.com/vitejs/vite/commit/9be7449544b078d572b93e7df463a0c4756a84f5))
* chunks are analysed multiple times ([#2541](https://github.com/vitejs/vite/issues/2541)) ([1451b78](https://github.com/vitejs/vite/commit/1451b78e7b1a34b89e2768315832087c686fb5aa))
* serve .js, .jsx, .ts, .tsx as application/javascript, fix [#2642](https://github.com/vitejs/vite/issues/2642) ([#2769](https://github.com/vitejs/vite/issues/2769)) ([b08e973](https://github.com/vitejs/vite/commit/b08e973da0477481970cdf6d49532bb6129aaa24))


### Features

* **createLogger:** allow custom prefix for logger ([#2019](https://github.com/vitejs/vite/issues/2019)) ([344d77e](https://github.com/vitejs/vite/commit/344d77e9735bc907b9383ad729afb0a8daa2af5f))
* add async support for vite config file ([#2758](https://github.com/vitejs/vite/issues/2758)) ([aee8b37](https://github.com/vitejs/vite/commit/aee8b3770cd081632fefb327b38ab704b97aa860))
* add inlineConfig.envFile option ([#2475](https://github.com/vitejs/vite/issues/2475)) ([81b80c6](https://github.com/vitejs/vite/commit/81b80c69d6bb00f54aae0481ea78f869db35725d))
* export manifest types ([#2901](https://github.com/vitejs/vite/issues/2901)) ([ffcb7ce](https://github.com/vitejs/vite/commit/ffcb7ce0ac4fe61fbd02da05090d48835a0dd1e4))
* parameter settings when packaging the library ([#2750](https://github.com/vitejs/vite/issues/2750)) ([f17e19a](https://github.com/vitejs/vite/commit/f17e19a80ced16401d00fef266493dd11fc69f2f))
* support cacheDir ([#2899](https://github.com/vitejs/vite/issues/2899)) ([57980d2](https://github.com/vitejs/vite/commit/57980d27ee10f1f92e532a0975d4ab39ce27d3ed))
* watch the dependencies of config file ([#3031](https://github.com/vitejs/vite/issues/3031)) ([bb419cb](https://github.com/vitejs/vite/commit/bb419cb969fec2a752dc45ab43b34351fe771f3a))
* **cli:** build watch mode, fix [#1434](https://github.com/vitejs/vite/issues/1434) ([#1449](https://github.com/vitejs/vite/issues/1449)) ([0dc6e37](https://github.com/vitejs/vite/commit/0dc6e37298e2e3efda74a1042f37bd70e3f5d3a5))
* **plugin:** plugin config hook supports return promise ([#2800](https://github.com/vitejs/vite/issues/2800)) ([5dfd0e8](https://github.com/vitejs/vite/commit/5dfd0e85978f77c8d12f7b83f25a383ae9c2f7e9))
* **plugin-api:** support async configResolved hooks (fixes [#2949](https://github.com/vitejs/vite/issues/2949)) ([#2951](https://github.com/vitejs/vite/issues/2951)) ([8b38168](https://github.com/vitejs/vite/commit/8b38168f7bc5be1d3417f3115ac723baec736ed6))
* support globbing from dependencies ([#2519](https://github.com/vitejs/vite/issues/2519)) ([7121553](https://github.com/vitejs/vite/commit/71215533ac60e8ff566dc3467feabfc2c71a01e2)), closes [#2390](https://github.com/vitejs/vite/issues/2390)



## [2.1.5](https://github.com/vitejs/vite/compare/v2.1.4...v2.1.5) (2021-03-31)


### Bug Fixes

* do not inject ?import query to external urls ([be3a4f5](https://github.com/vitejs/vite/commit/be3a4f5beb39a83bb62aef19f9e18177047618fa))
* replace __dirname and __filename in config file, fix [#2728](https://github.com/vitejs/vite/issues/2728) ([#2780](https://github.com/vitejs/vite/issues/2780)) ([eb57ac6](https://github.com/vitejs/vite/commit/eb57ac6ab1aa1256cadcea2bf8d31881023a568c))



## [2.1.4](https://github.com/vitejs/vite/compare/v2.1.3...v2.1.4) (2021-03-30)


### Bug Fixes

* **scan:** properly crawl imports in lang=ts blocks in vue/svelte files ([8f527fd](https://github.com/vitejs/vite/commit/8f527fd09c494fd23121aded0b836ff60a62835c))
* invalidate module cache on unlinked ([#2629](https://github.com/vitejs/vite/issues/2629)), fix [#2630](https://github.com/vitejs/vite/issues/2630) ([57f2a69](https://github.com/vitejs/vite/commit/57f2a698dcce47e11510bbff4c4716aac49a202b))
* reload only once on socket reconnect ([#2340](https://github.com/vitejs/vite/issues/2340)) ([d73c1fa](https://github.com/vitejs/vite/commit/d73c1fa6824397515adaf42ec29732013c8c54de))
* **client:** don't inject queries for data URLs ([#2703](https://github.com/vitejs/vite/issues/2703)), fix [#2658](https://github.com/vitejs/vite/issues/2658) ([86753d6](https://github.com/vitejs/vite/commit/86753d6e3d2be88f2f885c27fef8245c5d4b3b1b))
* **resolve:** fix resolver not following node resolve algorithm ([#2718](https://github.com/vitejs/vite/issues/2718)), fix [#2695](https://github.com/vitejs/vite/issues/2695) ([669c591](https://github.com/vitejs/vite/commit/669c591696788df844e7b26e600df86ffc70792c))
* **resolve:** improve browser filed substitutions ([#2701](https://github.com/vitejs/vite/issues/2701)), fix [#2598](https://github.com/vitejs/vite/issues/2598) ([cc213c6](https://github.com/vitejs/vite/commit/cc213c68d54db338ce0e6cf8fafe1b05a414fa6a))
* fix types errors ([#2726](https://github.com/vitejs/vite/issues/2726)) ([9716582](https://github.com/vitejs/vite/commit/97165828ecbcea867e927c62033002359d83a0db))


### Features

* **dev:** support keepNames option for optimizeDependencies config ([#2742](https://github.com/vitejs/vite/issues/2742)) ([130bf5a](https://github.com/vitejs/vite/commit/130bf5a03af2733dff9a34ef74450740d7cdb991))



## [2.1.3](https://github.com/vitejs/vite/compare/v2.1.2...v2.1.3) (2021-03-25)


### Bug Fixes

* add a timeout to the res.sep when discovering dependencies, fix [#2525](https://github.com/vitejs/vite/issues/2525) ([#2548](https://github.com/vitejs/vite/issues/2548)) ([31d10cb](https://github.com/vitejs/vite/commit/31d10cbacf292cbd1064f847673281745c977b0d))
* handle paths with special characters in injectQuery (fix [#2585](https://github.com/vitejs/vite/issues/2585)) ([#2614](https://github.com/vitejs/vite/issues/2614)) ([ed321ba](https://github.com/vitejs/vite/commit/ed321ba3f3364c0d93097d0ecfeb22aee3daa909))
* **css:** alias for background url in sass/less link error (fix [#2316](https://github.com/vitejs/vite/issues/2316)) ([#2323](https://github.com/vitejs/vite/issues/2323)) ([9499d26](https://github.com/vitejs/vite/commit/9499d26ead3214cebeab43cfb6f91adad69ae2a9))
* **dev:** remove process listeners on server close ([#2619](https://github.com/vitejs/vite/issues/2619)) ([74b360b](https://github.com/vitejs/vite/commit/74b360b6c53149c04ab5472aac7e327793a8a493))
* json should be bundled ([#2573](https://github.com/vitejs/vite/issues/2573)) ([2eb7682](https://github.com/vitejs/vite/commit/2eb76827a364f015727da521e55ec5fa54202a71)), closes [#2543](https://github.com/vitejs/vite/issues/2543)


### Features

* let `plugins` array contain falsy values ([#1649](https://github.com/vitejs/vite/issues/1649)) ([be76a30](https://github.com/vitejs/vite/commit/be76a304aacb52ac5e333552d30024be34a8a6a9))



## [2.1.2](https://github.com/vitejs/vite/compare/v2.1.1...v2.1.2) (2021-03-17)


### Bug Fixes

* update esbuild target to allow destructuring ([#2566](https://github.com/vitejs/vite/issues/2566)) ([da49782](https://github.com/vitejs/vite/commit/da497823e249aaf4d3a7da80e2211501f6159e1e))
* **manifest:** do not fail when using rollupOtions.external ([#2532](https://github.com/vitejs/vite/issues/2532)) ([e44cc11](https://github.com/vitejs/vite/commit/e44cc11bcf265d0bc4eaf5679c3b84d4b31d10ad))



## [2.1.1](https://github.com/vitejs/vite/compare/v2.1.0...v2.1.1) (2021-03-16)


### Bug Fixes

* decode path before reading sourcemap source content ([73b80d5](https://github.com/vitejs/vite/commit/73b80d5da99bbf35afe95c588d30c5b38655e225)), closes [#2524](https://github.com/vitejs/vite/issues/2524)
* **scan:** handle await replacement edge case ([cbfc3e9](https://github.com/vitejs/vite/commit/cbfc3e9dbabc4b4863a7f659b59d2e5115a81481)), closes [#2528](https://github.com/vitejs/vite/issues/2528)
* enable latest syntax when parsing for ssr ([407ce3b](https://github.com/vitejs/vite/commit/407ce3b7c5c07a51b5e20e97bc2fff2f173c74c0)), closes [#2526](https://github.com/vitejs/vite/issues/2526)



# [2.1.0](https://github.com/vitejs/vite/compare/v2.0.5...v2.1.0) (2021-03-15)


### Bug Fixes

* **json:** support importing json with ?url and ?raw queries ([fd0a0d9](https://github.com/vitejs/vite/commit/fd0a0d9bcaf0fd9098c5eb1a0c53226575fdcccb)), closes [#2455](https://github.com/vitejs/vite/issues/2455)
* **ssr:** fix mistakenly overwriting destructure variables as import bindings ([#2417](https://github.com/vitejs/vite/issues/2417)) ([24c866f](https://github.com/vitejs/vite/commit/24c866f0de4fddec45fd6aa757185d5e74d0e7f3)), closes [#2409](https://github.com/vitejs/vite/issues/2409)
* correctly handle explicit ts config file ([#2515](https://github.com/vitejs/vite/issues/2515)) ([e8f3c78](https://github.com/vitejs/vite/commit/e8f3c784b338a87a274dce44c73230d621cecb62))
* **hmr:** never invalidate an accepting importer ([#2457](https://github.com/vitejs/vite/issues/2457)) ([63bd250](https://github.com/vitejs/vite/commit/63bd2502781b87a2c04a375d9e7b770f63d8857c))
* **ssr:** handle empty sourcemaps (fix [#2391](https://github.com/vitejs/vite/issues/2391)) ([#2441](https://github.com/vitejs/vite/issues/2441)) ([103dec9](https://github.com/vitejs/vite/commit/103dec9fe80c333e1e8daec53fb08ab597f1120b))
* fix early logger definiton in resolveConfig ([#2425](https://github.com/vitejs/vite/issues/2425)) ([96ea9f4](https://github.com/vitejs/vite/commit/96ea9f4ad4522548248a951ed0cded46413b6193))
* Improve how [@fs](https://github.com/fs) urls are printed ([#2362](https://github.com/vitejs/vite/issues/2362)) ([5d4e82d](https://github.com/vitejs/vite/commit/5d4e82d90238b0d52ded1eea6359947eefc5e054))
* Improve injectQuery path handling ([#2435](https://github.com/vitejs/vite/issues/2435)) ([a5412f8](https://github.com/vitejs/vite/commit/a5412f86be80fa55cf41ac286b0a9675098c6ab8)), closes [#2422](https://github.com/vitejs/vite/issues/2422)
* keep process running when fail to load config in restarting server ([#2510](https://github.com/vitejs/vite/issues/2510)) ([b18af15](https://github.com/vitejs/vite/commit/b18af15fe83d1fcea7800fab9b550018476f740f)), closes [#2496](https://github.com/vitejs/vite/issues/2496)
* make import resolution failures easier to track down ([#2450](https://github.com/vitejs/vite/issues/2450)) ([f6ac860](https://github.com/vitejs/vite/commit/f6ac8600d944a5ce92df92c0cbef162a165c6b94))
* respect cors and proxy options in preview command ([f7d85ae](https://github.com/vitejs/vite/commit/f7d85ae4c25e7f9481261d691696554113c2d58b)), closes [#2279](https://github.com/vitejs/vite/issues/2279)
* url linked to wmr rollup-plugin-container.js found 404 ([#2368](https://github.com/vitejs/vite/issues/2368)) ([209232c](https://github.com/vitejs/vite/commit/209232cc0417f46ea73458650efa5bf6d9306e65))
* **build:** respect rollupOtions.external  at generate manifest([#2353](https://github.com/vitejs/vite/issues/2353)) ([b05a567](https://github.com/vitejs/vite/commit/b05a5676eb4c46852c0833cc5ff264533d8053ef))


### Features

* allow custom websocket server ([#2338](https://github.com/vitejs/vite/issues/2338)) ([9243cc9](https://github.com/vitejs/vite/commit/9243cc9e8ea6271eb5d548ff459eb7cc5f260598))
* bundle vite config file with esbuild instead of rollup ([#2517](https://github.com/vitejs/vite/issues/2517)) ([e034ee2](https://github.com/vitejs/vite/commit/e034ee2d9c7ef1497d1c9248ef05cdd8e0efb6ad))
* **dev:** support keepNames for dependencies ([#2376](https://github.com/vitejs/vite/issues/2376)) ([b5cd8c8](https://github.com/vitejs/vite/commit/b5cd8c8dc33e920a301ef03c097147d841d08200))



## [2.0.5](https://github.com/vitejs/vite/compare/v2.0.4...v2.0.5) (2021-03-02)


### Bug Fixes

* serving static files from root ([#2309](https://github.com/vitejs/vite/issues/2309)) ([4f942be](https://github.com/vitejs/vite/commit/4f942bef3ee2dc496a3a6854de9ea7b208829ff6))
* **scan:** handle race condition for tempDir removal ([#2299](https://github.com/vitejs/vite/issues/2299)) ([67e56e4](https://github.com/vitejs/vite/commit/67e56e48dac7875a2916845614bfb970722744a0))
* await bundle close ([#2313](https://github.com/vitejs/vite/issues/2313)) ([c988574](https://github.com/vitejs/vite/commit/c988574c3253ff133c2395c1d3884945e67641aa))



## [2.0.4](https://github.com/vitejs/vite/compare/v2.0.3...v2.0.4) (2021-02-26)


### Bug Fixes

* **build:** css tags injection priority ([#2272](https://github.com/vitejs/vite/issues/2272)) ([55ad23e](https://github.com/vitejs/vite/commit/55ad23ed44af35cb34c81881bdb12bff844c913e))
* **css:** ignore css commonjs-proxy modules ([#2160](https://github.com/vitejs/vite/issues/2160)) ([de33d32](https://github.com/vitejs/vite/commit/de33d3233708088a94217045069b4a1d9d38d1a7))
* **optimizer:** detect re-exports in dep entries ([a3abf99](https://github.com/vitejs/vite/commit/a3abf99a19e117fc71e6ea8596c6cda68a6a85ad)), closes [#2219](https://github.com/vitejs/vite/issues/2219)
* **sourcemap:** avoid cjs import interop line offset messing up sourcemap ([4ce972d](https://github.com/vitejs/vite/commit/4ce972df23dfe68543bd960ecf95091a6ffc4fdb)), closes [#2280](https://github.com/vitejs/vite/issues/2280)
* **sourcemap:** inject `sourcesContent` for .map requests ([#2283](https://github.com/vitejs/vite/issues/2283)) ([8d50b18](https://github.com/vitejs/vite/commit/8d50b18f64e3a342b2f1c4f79f306f0fb2b86f69))
* **ssr:** allow ssr module export overwrites ([#2228](https://github.com/vitejs/vite/issues/2228)) ([6fae0b7](https://github.com/vitejs/vite/commit/6fae0b7d119cf97904ae276176f8bb4374aee300))
* add source and sourcesContent to transformed SSR modules ([#2285](https://github.com/vitejs/vite/issues/2285)) ([72be67b](https://github.com/vitejs/vite/commit/72be67b70867fbbb2df63ce5484f56e6c95e2759)), closes [#2284](https://github.com/vitejs/vite/issues/2284)
* **optimizer:** fix deps aliased to cdns that are imported by optimized deps ([06d3244](https://github.com/vitejs/vite/commit/06d32447b465c045604d9f111d6fa46a98f7a7ea)), closes [#2268](https://github.com/vitejs/vite/issues/2268)
* **ssr:** handle imported binding being used as super class ([167a9c3](https://github.com/vitejs/vite/commit/167a9c31b9709f3c9627149fa5b6da378f8e09ad)), closes [#2221](https://github.com/vitejs/vite/issues/2221)
* **ssr:** handle ssrLoadModule failures in post pending ([#2253](https://github.com/vitejs/vite/issues/2253)) ([ea323cc](https://github.com/vitejs/vite/commit/ea323ccdfb5a2aef2128dd3ebd09a261d371a897)), closes [#2252](https://github.com/vitejs/vite/issues/2252)
* **ssr:** ssr transform method definition ([#2223](https://github.com/vitejs/vite/issues/2223)) ([8e0c0fa](https://github.com/vitejs/vite/commit/8e0c0fa8db5247fb1be94d5b8d3def2c4bc27923))
* decode url before serving static files ([#2201](https://github.com/vitejs/vite/issues/2201)) ([1342108](https://github.com/vitejs/vite/commit/1342108a04f7e9068301ecd04a5b391c1ed8e15d)), closes [#2195](https://github.com/vitejs/vite/issues/2195)
* determine anonymous function wrapper offset at runtime ([#2266](https://github.com/vitejs/vite/issues/2266)) ([a2ee885](https://github.com/vitejs/vite/commit/a2ee885e52547703f66367fec589f372d2b9e8a8)), closes [#2265](https://github.com/vitejs/vite/issues/2265)



## [2.0.3](https://github.com/vitejs/vite/compare/v2.0.2...v2.0.3) (2021-02-24)


### Bug Fixes

* **resolve:** compat for babel 7.13 helper resolution ([39820b9](https://github.com/vitejs/vite/commit/39820b96cec2c672e849e160b92b42c979b85285))
* **ssr:** fix ssr external check for mjs entries ([5095e04](https://github.com/vitejs/vite/commit/5095e041deaced2db8fc3c3af504367bc57bb93f)), closes [#2161](https://github.com/vitejs/vite/issues/2161)
* do not prepend base to double slash urls during dev ([#2143](https://github.com/vitejs/vite/issues/2143)) ([7a1b5c6](https://github.com/vitejs/vite/commit/7a1b5c670e2088a65f9866ecfe1b98f041980683))
* handle escape sequences in import specifiers ([#2162](https://github.com/vitejs/vite/issues/2162)) ([bbda31e](https://github.com/vitejs/vite/commit/bbda31ef695d3f9b89160435f73fcb948c3b07f1)), closes [#2083](https://github.com/vitejs/vite/issues/2083)
* should transform the img tag's srcset arrtibute and css' image-set property ([#2188](https://github.com/vitejs/vite/issues/2188)) ([0f17a74](https://github.com/vitejs/vite/commit/0f17a74c64a6664c68f23c92d572c22d1a4de059)), closes [#2177](https://github.com/vitejs/vite/issues/2177)
* treat the watcher path as literal name ([#2211](https://github.com/vitejs/vite/issues/2211)) ([58bed16](https://github.com/vitejs/vite/commit/58bed165e996cf8131ba3439ef6d8bf8d33598af)), closes [#2179](https://github.com/vitejs/vite/issues/2179)
* use proper esbuild loader for .cjs and .mjs files ([#2215](https://github.com/vitejs/vite/issues/2215)) ([a0d922e](https://github.com/vitejs/vite/commit/a0d922e7d9790f998c246f8122bc339717b6088f))
* **optimizer:** let esbuild resolve transitive deps ([0138ef3](https://github.com/vitejs/vite/commit/0138ef3eeec4bda73204ae68d5d068175335f38c)), closes [#2199](https://github.com/vitejs/vite/issues/2199)
* **scan:** avoid replacing await in import specifiers ([94e5b9a](https://github.com/vitejs/vite/commit/94e5b9a06f764d576eeeb7f35cae6bdc03b878be)), closes [#2210](https://github.com/vitejs/vite/issues/2210)



## [2.0.2](https://github.com/vitejs/vite/compare/v2.0.1...v2.0.2) (2021-02-22)


### Bug Fixes

* **build:** do not handle asset url when its url is "#" ([#2097](https://github.com/vitejs/vite/issues/2097)) ([0092a35](https://github.com/vitejs/vite/commit/0092a35632d31590409530639e33fc90274d6488)), closes [#2096](https://github.com/vitejs/vite/issues/2096)
* **cli:** fix short flags being ignored ([#2131](https://github.com/vitejs/vite/issues/2131)) ([cbb3eff](https://github.com/vitejs/vite/commit/cbb3eff96f54ed76c6ed7ca793d50914c96a67da))
* **optimizer:** do not optimize deps w/ jsx entrypoints ([1857652](https://github.com/vitejs/vite/commit/1857652f6153f1cfd7d171e75d567dd05731c711)), closes [#2107](https://github.com/vitejs/vite/issues/2107)
* **optimizer:** externalize jsx/tsx files in dependencies ([37a103f](https://github.com/vitejs/vite/commit/37a103fd2aadd42b0cda0bdfa81e0624a64b1a09))
* **optimizer:** fix .styl externalization ([87cfd9e](https://github.com/vitejs/vite/commit/87cfd9e556a0e633694805ae2497a656722d3abb)), closes [#2168](https://github.com/vitejs/vite/issues/2168)
* **resolve:** fix browser mapping fallback ([de58967](https://github.com/vitejs/vite/commit/de58967c570822e7a345bb63b81ca113ed8a8127)), closes [#2115](https://github.com/vitejs/vite/issues/2115)
* **scan:** set namespace when resolving to html ([#2174](https://github.com/vitejs/vite/issues/2174)) ([3be4fac](https://github.com/vitejs/vite/commit/3be4facebd383ea74db6274fc53848fb0149b902)), closes [#2163](https://github.com/vitejs/vite/issues/2163)
* **ssr:** avoid duplicate ssr module instantiation on shared imports ([a763ffd](https://github.com/vitejs/vite/commit/a763ffd5135fbd34bc1bdebe349e80b51884e1d4)), closes [#2060](https://github.com/vitejs/vite/issues/2060)
* **ssr:** fix ssr export * from ([8ed67cf](https://github.com/vitejs/vite/commit/8ed67cf6782bec72f8fbb4237fadfb415f86129d)), closes [#2158](https://github.com/vitejs/vite/issues/2158)
* typo ([#2149](https://github.com/vitejs/vite/issues/2149)) ([2b19e3c](https://github.com/vitejs/vite/commit/2b19e3c2d36f87e84d8bf34982a06f573a56c008))
* **ssr:** reject ssrLoadModule promises if evaluation fails ([#2079](https://github.com/vitejs/vite/issues/2079)) ([e303c4e](https://github.com/vitejs/vite/commit/e303c4e9395e6770b1f00104f28dee03e37c26ac)), closes [#2078](https://github.com/vitejs/vite/issues/2078)
* stricter html fallback check in transformRequest ([d0eac2f](https://github.com/vitejs/vite/commit/d0eac2fca9bc16caca7b9043b9c614c7044fb9fa)), closes [#2051](https://github.com/vitejs/vite/issues/2051)



## [2.0.1](https://github.com/vitejs/vite/compare/v2.0.0...v2.0.1) (2021-02-17)


### Bug Fixes

* allow custom process.env.VAR defines ([#2055](https://github.com/vitejs/vite/issues/2055)) ([7def49a](https://github.com/vitejs/vite/commit/7def49a49c83539b6a65c895c276fa83f7c89349))
* do not error on failed load for SPA html requests ([44a30d5](https://github.com/vitejs/vite/commit/44a30d5df8257bed9c59360b9751bf63151880b4)), closes [#2051](https://github.com/vitejs/vite/issues/2051)
* more inclusive config syntax error hanlding for Node 12.x ([27785f7](https://github.com/vitejs/vite/commit/27785f7fcc5b45987b5f0bf308137ddbdd9f79ea)), closes [#2050](https://github.com/vitejs/vite/issues/2050)



# [2.0.0](https://github.com/vitejs/vite/compare/v2.0.0-beta.70...v2.0.0) (2021-02-16)


### Bug Fixes

* **css/assets:** respect alias in css url() paths ([ad50060](https://github.com/vitejs/vite/commit/ad50060ed43c8d84c22a5c60592404a4e1180e2d)), closes [#2043](https://github.com/vitejs/vite/issues/2043)
* **resolve:** handle hash fragment in fs resolve ([34064c8](https://github.com/vitejs/vite/commit/34064c89aba3690667e4f5fedcbc564f6d759153))
* **scan:** fix top level await handling in script setup ([24ed098](https://github.com/vitejs/vite/commit/24ed098eedf9e90da69c328bb4d2749fec957fb3)), closes [#2044](https://github.com/vitejs/vite/issues/2044)
* **scan:** ignore virtual entries during scan ([6dc2d56](https://github.com/vitejs/vite/commit/6dc2d561cf2d8e0ea5806764314582a6f434c1d6)), closes [#2047](https://github.com/vitejs/vite/issues/2047)
* always transform applicable requests ([#2041](https://github.com/vitejs/vite/issues/2041)) ([4fd61ab](https://github.com/vitejs/vite/commit/4fd61abc05c686088b9f0ece421138311a8428c8))



# [2.0.0-beta.70](https://github.com/vitejs/vite/compare/v2.0.0-beta.69...v2.0.0-beta.70) (2021-02-15)


### Bug Fixes

* respect host option when listening ([f05ae32](https://github.com/vitejs/vite/commit/f05ae32156211d3bbf82ccfaea6d4f2fc137e609)), closes [#2032](https://github.com/vitejs/vite/issues/2032)
* **css:** resolve pre-processors from project root ([ddfcbce](https://github.com/vitejs/vite/commit/ddfcbce05753da3e525c1bb9bdf449a322e997f4)), closes [#2030](https://github.com/vitejs/vite/issues/2030)
* reject preload promise if link fails to load ([#2027](https://github.com/vitejs/vite/issues/2027)) ([f74d65d](https://github.com/vitejs/vite/commit/f74d65d41d898982839abb13787ed310555c7980)), closes [#2009](https://github.com/vitejs/vite/issues/2009)
* **ssr:** ignore base when normalizing urls for ssr ([26d409b](https://github.com/vitejs/vite/commit/26d409bbfb9bf661a19cc6619242b382f7181d05)), closes [#1995](https://github.com/vitejs/vite/issues/1995)


### Code Refactoring

* make define option perform direct replacement instead ([059070e](https://github.com/vitejs/vite/commit/059070e10aaee27a03ec5fd52e77fa04effe4c8f))


### Features

* **css:** allow async additionalData function for css pre-processors ([20f609d](https://github.com/vitejs/vite/commit/20f609dcc4f588da89b4f81eb64fb59c16fd7e07)), closes [#2002](https://github.com/vitejs/vite/issues/2002)
* allow `getJSON` option on `css.modules` ([#2025](https://github.com/vitejs/vite/issues/2025)) ([e324e36](https://github.com/vitejs/vite/commit/e324e36e04ba76e2c5203126306f1cb5ac09df8d))


### BREAKING CHANGES

* `define` option no longer calls `JSON.stringify` on
string values. This means string define values will be now treated as
raw expressions. To define a string constant, explicit quotes are now
required.



# [2.0.0-beta.69](https://github.com/vitejs/vite/compare/v2.0.0-beta.68...v2.0.0-beta.69) (2021-02-11)


### Bug Fixes

* fix out of root static file serving on windows ([4d34a73](https://github.com/vitejs/vite/commit/4d34a7362e57ba8b04e8fee0e0f2f74ce05f13eb)), closes [#1982](https://github.com/vitejs/vite/issues/1982)
* Remove negative count in stdout with 0 rows ([#1983](https://github.com/vitejs/vite/issues/1983)) ([09b13ed](https://github.com/vitejs/vite/commit/09b13eddd98810fef82858bab7997ea895ab3289)), closes [#1981](https://github.com/vitejs/vite/issues/1981)
* **ssr:** handle virtual modules during ssr ([108be94](https://github.com/vitejs/vite/commit/108be949cd814ec8fc6214c6cdfa440c0dfd7e13)), closes [#1980](https://github.com/vitejs/vite/issues/1980)
* prevent crash on malformed URI ([#1977](https://github.com/vitejs/vite/issues/1977)) ([f1b0bc9](https://github.com/vitejs/vite/commit/f1b0bc9b9bf25d206e3db93c242d5a25af0c15d6))
* user define on import.meta.env should apply during dev ([603d57e](https://github.com/vitejs/vite/commit/603d57ebc61970902ed9a275dd2e74a6c3eabe65))


### Features

* pass config env to plugin config hook ([19f3503](https://github.com/vitejs/vite/commit/19f35033045582b05c50ecad10bf2b75a0425383))



# [2.0.0-beta.68](https://github.com/vitejs/vite/compare/v2.0.0-beta.67...v2.0.0-beta.68) (2021-02-11)


### Bug Fixes

* **css/assets:** properly replace multiple css asset urls on the same line ([1d805a6](https://github.com/vitejs/vite/commit/1d805a6beb212f1812b1b13460c910c848ca3772)), closes [#1975](https://github.com/vitejs/vite/issues/1975)
* **scan:** handle lang=jsx in sfcs ([2f9549c](https://github.com/vitejs/vite/commit/2f9549c910b954b0ed4257a7a3a2e0ae6004c701)), closes [#1972](https://github.com/vitejs/vite/issues/1972)
* fix path normalization for windows paths w/ non ascii chars ([03b323d](https://github.com/vitejs/vite/commit/03b323d39cafe2baabef74e6051a9640add82590)), closes [#1384](https://github.com/vitejs/vite/issues/1384)


### Features

* support --open for `vite preview` command ([#1968](https://github.com/vitejs/vite/issues/1968)) ([446b815](https://github.com/vitejs/vite/commit/446b815d8911440f178f7b36aadc9a5a3cf46fe0))
* **resolve:** expose full resolve options via config ([0318c64](https://github.com/vitejs/vite/commit/0318c64cc3efe970a5cd3ef6624fe3625af06012)), closes [#1951](https://github.com/vitejs/vite/issues/1951)


### Performance Improvements

* ignore node_modules when globbing import.meta.glob ([8b3d0ea](https://github.com/vitejs/vite/commit/8b3d0ea41265870b9b0741bde3a31bde81078277)), closes [#1974](https://github.com/vitejs/vite/issues/1974)



# [2.0.0-beta.67](https://github.com/vitejs/vite/compare/v2.0.0-beta.66...v2.0.0-beta.67) (2021-02-09)


### Bug Fixes

* **html:** avoid duplicate preload link injection ([6e71596](https://github.com/vitejs/vite/commit/6e7159675c55f46bcc030f9c6fd35dee9a92cfca)), closes [#1957](https://github.com/vitejs/vite/issues/1957)
* **ssr:** fix ssr node require for virtual modules ([fa2d7d6](https://github.com/vitejs/vite/commit/fa2d7d66c16c2156354b6888a2f0bd4b47262ca2))
* do not open browser when restarting server ([#1952](https://github.com/vitejs/vite/issues/1952)) ([9af1517](https://github.com/vitejs/vite/commit/9af1517e47f66bb793447d998cf1a4d2fa3ef758))



# [2.0.0-beta.66](https://github.com/vitejs/vite/compare/v2.0.0-beta.65...v2.0.0-beta.66) (2021-02-08)


### Bug Fixes

* **import-analysis:** fix literal dynamic id false positive ([6a6508e](https://github.com/vitejs/vite/commit/6a6508edb9b31a4ea8bbc54b841f5227ba2b562a)), closes [#1902](https://github.com/vitejs/vite/issues/1902)
* **resolve:** avoid race condition in resolve skip check ([85f1e7b](https://github.com/vitejs/vite/commit/85f1e7bdcb9d454bd17b96ef98e2dc0cad58776b)), closes [#1937](https://github.com/vitejs/vite/issues/1937)
* **resolve:** pass down resolve skip via context ([9066f27](https://github.com/vitejs/vite/commit/9066f27c591b356107239e9cef36c1cad73864c0)), closes [#1937](https://github.com/vitejs/vite/issues/1937)
* **scan:** only scan supported entry file types ([a93e61d](https://github.com/vitejs/vite/commit/a93e61d02405728278ac905a9539450927dc7364))
* use dedicated endpoint for hmr reconnect ping ([b433607](https://github.com/vitejs/vite/commit/b433607aca0986c6e1592c3f64adb2ef30689c5e)), closes [#1904](https://github.com/vitejs/vite/issues/1904)
* **ssr:** ssr external should take scannd imports into account ([92934d4](https://github.com/vitejs/vite/commit/92934d4c18329cc51879aca5016a408b467c1fa0)), closes [#1916](https://github.com/vitejs/vite/issues/1916)
* brotli skipped is printed when build.brotliSize is false ([#1912](https://github.com/vitejs/vite/issues/1912)) ([db3c324](https://github.com/vitejs/vite/commit/db3c324134db2bf371700cc4d838a49ac6148045))



# [2.0.0-beta.65](https://github.com/vitejs/vite/compare/v2.0.0-beta.64...v2.0.0-beta.65) (2021-02-05)


### Bug Fixes

* **build:** ignore html asset urls that do not exist on disk ([02653f0](https://github.com/vitejs/vite/commit/02653f0b93cacd0f1b3464204d24c0d57f407aa0)), closes [#1885](https://github.com/vitejs/vite/issues/1885)
* better dependency non-js type file handling ([1fdc710](https://github.com/vitejs/vite/commit/1fdc710a391b968f85f6a150dc06e51e53742b02))
* **dev:** check wasClean in onclose event ([#1872](https://github.com/vitejs/vite/issues/1872)) ([5d3107a](https://github.com/vitejs/vite/commit/5d3107a4a787929810fbfaef37bf3002aa0bcc17))
* **resolve:** prioritize file over dir with same name for resolve ([c741872](https://github.com/vitejs/vite/commit/c741872e6ca975f507ec89581b742a1da19a0cb0)), closes [#1871](https://github.com/vitejs/vite/issues/1871)
* **ssr:** respect user defines for ssr ([3fad3ba](https://github.com/vitejs/vite/commit/3fad3ba861fb56edd22941db645f2d73b02bf7b1))
* do not include vite in ssr externals ([578c591](https://github.com/vitejs/vite/commit/578c591ffe7b7c1ffa68e711a7df043afe013daa)), closes [#1865](https://github.com/vitejs/vite/issues/1865)


### Code Refactoring

* **css:** use default CSS modules localsConvention settings ([fee7393](https://github.com/vitejs/vite/commit/fee739325fd4dbf7f6d842c205608e39271db513))


### Features

* **cli:** make --ssr flag value optional ([3c7b652](https://github.com/vitejs/vite/commit/3c7b652f24fdb5e67c5f56db3cea0769bcd9263b)), closes [#1877](https://github.com/vitejs/vite/issues/1877)
* **proxy:** support conditional options for proxy request ([#1888](https://github.com/vitejs/vite/issues/1888)) ([e81a118](https://github.com/vitejs/vite/commit/e81a118735045a40f0ab93c1bedef5b7d674f2f0))
* support absolute glob patterns ([159cc79](https://github.com/vitejs/vite/commit/159cc799f19482da3626f906cde45accdf780823)), closes [#1875](https://github.com/vitejs/vite/issues/1875)
* support resolving style/sass entries in css [@import](https://github.com/import) ([f90a85c](https://github.com/vitejs/vite/commit/f90a85c2ba8c9ba215fe75c49035a7e38fa81a7d)), closes [#1874](https://github.com/vitejs/vite/issues/1874)


### Performance Improvements

* improve resolve cache ([6a793d3](https://github.com/vitejs/vite/commit/6a793d319cf7adab061b056692c331a9d66fdac5))


### BREAKING CHANGES

* **css:** CSS modules now defaults to export class names as-is.
To get camelCase exports like before, explictly set
`css.modules.localsConvention` via config.



# [2.0.0-beta.64](https://github.com/vitejs/vite/compare/v2.0.0-beta.63...v2.0.0-beta.64) (2021-02-03)


### Bug Fixes

* **ssr:** do not resolve to optimized deps during ssr ([d021506](https://github.com/vitejs/vite/commit/d0215060e87c9464c97549cdbb008184796d0f8f)), closes [#1860](https://github.com/vitejs/vite/issues/1860)
* **ssr:** fix externalized cjs deps that exports compiled esmodule ([8ec2d6f](https://github.com/vitejs/vite/commit/8ec2d6f77eb04e015156769f4f004a4792077770))



# [2.0.0-beta.63](https://github.com/vitejs/vite/compare/v2.0.0-beta.62...v2.0.0-beta.63) (2021-02-03)


### Bug Fixes

* **css:** hoist external [@import](https://github.com/import) in concatenated css ([000ee62](https://github.com/vitejs/vite/commit/000ee62ef41e4964d1002ab7862303cec0419c47)), closes [#1845](https://github.com/vitejs/vite/issues/1845)
* **css:** respect sass partial import convention ([cb7b6be](https://github.com/vitejs/vite/commit/cb7b6becd0a566c58aca6cc47ae785ac2c4b4482))
* **vite:** close server and exit if stdin ends ([#1857](https://github.com/vitejs/vite/issues/1857)) ([b065ede](https://github.com/vitejs/vite/commit/b065ede3cca3bc72d3bb3e6f9cd945d1b36ccb42))
* consistently use mode for NODE_ENV in deps ([cd13ef0](https://github.com/vitejs/vite/commit/cd13ef009abd23d2676dda470638c81895034a91))
* do not shim process with actual object ([8ad7ecd](https://github.com/vitejs/vite/commit/8ad7ecd1029bdc0b47e55877db10ac630829c7e5))
* make ssr external behavior consistent between dev/build ([e089eff](https://github.com/vitejs/vite/commit/e089eff8f8108fa5463e2e42e16244f7edfd5a1e))
* only close if http server has listened ([94a8042](https://github.com/vitejs/vite/commit/94a804233682581c0f920ed5c0d42aa85ea3f163)), closes [#1855](https://github.com/vitejs/vite/issues/1855)
* **scan:** handle import glob in jsx/tsx files ([24695fe](https://github.com/vitejs/vite/commit/24695fe47727b7b4e3ac85bb389477f673c57c18))
* **ssr:** improve ssr external heuristics ([928fc33](https://github.com/vitejs/vite/commit/928fc33b6fffb3bb22c2daa4b478ead7715a2c5f)), closes [#1854](https://github.com/vitejs/vite/issues/1854)
* respect config.build.brotliSize in reporter ([1d5437d](https://github.com/vitejs/vite/commit/1d5437d56bb0974c21561c1cdf5ad1588baefea3))


### Features

* **ssr:** graduate ssr method types ([0fe2634](https://github.com/vitejs/vite/commit/0fe2634756b6311f0489613460eeadc6c8280192))



# [2.0.0-beta.62](https://github.com/vitejs/vite/compare/v2.0.0-beta.61...v2.0.0-beta.62) (2021-02-02)


### Bug Fixes

* properly cascade asset hash change ([f8e4eeb](https://github.com/vitejs/vite/commit/f8e4eebcc48ad5e98e52d12ce6595da014a43276))
* **optimizer:** fix cjs interop check on entries with identical ending ([338d17a](https://github.com/vitejs/vite/commit/338d17a197c9835fbce79919b58b8c4e094f4bb9)), closes [#1847](https://github.com/vitejs/vite/issues/1847)
* **scan:** handle tsx lang in SFCs during dep scan ([#1837](https://github.com/vitejs/vite/issues/1837)) ([be9bc3f](https://github.com/vitejs/vite/commit/be9bc3ff6eb72386876af17b61ccabae1ee249db))


### Features

* **dev:** inject env for webworker ([#1846](https://github.com/vitejs/vite/issues/1846)) ([5735692](https://github.com/vitejs/vite/commit/5735692b571ad193c04f236325df97bca7ef92bc)), closes [#1838](https://github.com/vitejs/vite/issues/1838)
* better build output + options for brotli / chunk size warning ([da1b06f](https://github.com/vitejs/vite/commit/da1b06f3771371b72c8ba68f3428c48ebf2082ad))



# [2.0.0-beta.61](https://github.com/vitejs/vite/compare/v2.0.0-beta.60...v2.0.0-beta.61) (2021-02-01)


### Bug Fixes

* **less:** fix less [@import](https://github.com/import) url rebasing ([41783fa](https://github.com/vitejs/vite/commit/41783fade0604adb98e468d4a4f8b50c9624899a)), closes [#1834](https://github.com/vitejs/vite/issues/1834)
* **manifest:** include assets referenced via CSS in manifest entries ([34894a2](https://github.com/vitejs/vite/commit/34894a2c41871a08a86fb9a1852563bc698d9c00)), closes [#1827](https://github.com/vitejs/vite/issues/1827)
* yarn pnp resolveDir ([9c6edef](https://github.com/vitejs/vite/commit/9c6edefd45634becbd51c1bf25b735770aeb752a))
* **optimizer:** fix cjs export interop for webpacked output ([4b6ebc3](https://github.com/vitejs/vite/commit/4b6ebc3f3b117cbe45aff55746dd5f588dfe1587)), closes [#1830](https://github.com/vitejs/vite/issues/1830)
* **ssr:** do not inject hmr timestamp when transforming for ssr ([#1825](https://github.com/vitejs/vite/issues/1825)) ([8ace645](https://github.com/vitejs/vite/commit/8ace6456b682a9ae7d550225817f3270524d96a3))



# [2.0.0-beta.60](https://github.com/vitejs/vite/compare/v2.0.0-beta.59...v2.0.0-beta.60) (2021-01-31)


### Bug Fixes

* **hmr:** do not update on file unlink when there are no affected modules ([#1818](https://github.com/vitejs/vite/issues/1818)) ([59fe913](https://github.com/vitejs/vite/commit/59fe913f122696ed94ac3f78655576fe7eef98d6))
* **optimizer:** entry resolving for yarn pnp ([febff7b](https://github.com/vitejs/vite/commit/febff7b837a09eec64bfe8a7cf380dd8001bba67)), closes [#1813](https://github.com/vitejs/vite/issues/1813)
* **optimizer:** fix cjs interop for packages that cannot be ([3b85296](https://github.com/vitejs/vite/commit/3b852964344e4b7e3b45b3af30f27baa89660261)), closes [#1821](https://github.com/vitejs/vite/issues/1821)
* **scan:** skip non-absolute resolved paths during scan ([f635971](https://github.com/vitejs/vite/commit/f6359716ae9f3b206cca1e63b6c1240d3bbc74fa))


### Features

* support ?url special query ([0006e89](https://github.com/vitejs/vite/commit/0006e89af419472a3c4c3f0f5328242aade2939a))



# [2.0.0-beta.59](https://github.com/vitejs/vite/compare/v2.0.0-beta.58...v2.0.0-beta.59) (2021-01-30)


### Bug Fixes

* **optimizer:** exclude should apply to deep imports ([3c22f84](https://github.com/vitejs/vite/commit/3c22f8404ecd8504448ffbe05763145887d05928))
* **optimizer:** separate dep entry proxy modules from actual modules ([8e1d3d8](https://github.com/vitejs/vite/commit/8e1d3d82f6d3ba9e48adb60a1b016c35f0aab627))



# [2.0.0-beta.58](https://github.com/vitejs/vite/compare/v2.0.0-beta.57...v2.0.0-beta.58) (2021-01-29)


### Bug Fixes

* **optimizer:** handle rollup plugin virtual ids ([a748896](https://github.com/vitejs/vite/commit/a748896b2058b0bbc2a45ef9cf84969f5681b49e)), closes [#1804](https://github.com/vitejs/vite/issues/1804)
* do not generate import specifier if not needed ([e438802](https://github.com/vitejs/vite/commit/e438802803d11acf99918690e4010b601fd7e40d))


### Features

* add ViteDevServer.transformIndexHtml method for ssr ([dbe1f4a](https://github.com/vitejs/vite/commit/dbe1f4aeadfb9f927f8cd0eec95a32aeee9c3601)), closes [#1745](https://github.com/vitejs/vite/issues/1745)
* support configuring publicDir via config ([470ceb8](https://github.com/vitejs/vite/commit/470ceb827629ab6cccf76cec3249caee08db247a)), closes [#1799](https://github.com/vitejs/vite/issues/1799)



# [2.0.0-beta.57](https://github.com/vitejs/vite/compare/v2.0.0-beta.56...v2.0.0-beta.57) (2021-01-29)


### Bug Fixes

* **optimizer:** fix entry cross imports ([a9ca3da](https://github.com/vitejs/vite/commit/a9ca3da4f1d2c584499bbbf2f16bdbf60d4f12e9)), closes [#1801](https://github.com/vitejs/vite/issues/1801)
* **optimizer:** respect ids that resolve to external urls during scan ([328b6b9](https://github.com/vitejs/vite/commit/328b6b9f7049ec9661cf42f4f43d0ea92fe9b9d0)), closes [#1798](https://github.com/vitejs/vite/issues/1798)
* still account for plugins in optimizer hash ([82dce90](https://github.com/vitejs/vite/commit/82dce90e9d5d3ad1ea516a2a66635960766afb65))
* **optimizer:** check qualified deps length after accounting for include ([6a03813](https://github.com/vitejs/vite/commit/6a0381311b173b133772efe8d5f174e9bdf989cd))
* **optimizer:** exclude ?worker and ?raw from runtime dep discovery ([d216da0](https://github.com/vitejs/vite/commit/d216da0e59bd5ab05a8eac38e99e9b6dd9461478))
* **optimizer:** properly externalize unknown types ([c3b81a8](https://github.com/vitejs/vite/commit/c3b81a8f6a3c8b2199dd42c09f5a722121891334)), closes [#1793](https://github.com/vitejs/vite/issues/1793)



# [2.0.0-beta.56](https://github.com/vitejs/vite/compare/v2.0.0-beta.55...v2.0.0-beta.56) (2021-01-29)


### Bug Fixes

* **optimizer:** handle alias to optimized entries ([81eb7a0](https://github.com/vitejs/vite/commit/81eb7a09ddb0042ec94561052e961c1ee7463bb3)), closes [#1780](https://github.com/vitejs/vite/issues/1780)


### Performance Improvements

* use esbuild service mode during pre-bundling ([b24b07c](https://github.com/vitejs/vite/commit/b24b07ce689df721d63b68e2647cc0609e58df32))



# [2.0.0-beta.55](https://github.com/vitejs/vite/compare/v2.0.0-beta.54...v2.0.0-beta.55) (2021-01-28)


### Bug Fixes

* **optimizer:** use js loader for resolved mjs files in esbuild ([0f2c2ce](https://github.com/vitejs/vite/commit/0f2c2ce4875c3ed87264c4904b047f06ee1c5d2d))



# [2.0.0-beta.54](https://github.com/vitejs/vite/compare/v2.0.0-beta.53...v2.0.0-beta.54) (2021-01-28)


### Bug Fixes

* **optimizer:** map entries to their file paths when passed as importer ([32ba8fb](https://github.com/vitejs/vite/commit/32ba8fb2b63b43dd4018dbbe5b6b431375e1c3d0))



# [2.0.0-beta.53](https://github.com/vitejs/vite/compare/v2.0.0-beta.52...v2.0.0-beta.53) (2021-01-28)


### Bug Fixes

* **css:** pure css chunk removal + manifest entry with multiple css files ([cadf38c](https://github.com/vitejs/vite/commit/cadf38cdedf5d47c63e8476b16bb74434df35878)), closes [#1776](https://github.com/vitejs/vite/issues/1776)
* **optimizer:** add separate hash for invalidating optimized deps ([216ae8e](https://github.com/vitejs/vite/commit/216ae8e95cc43dca47da4607086d2948d538fc53))
* **optimizer:** externalize json ([c3e52f2](https://github.com/vitejs/vite/commit/c3e52f2b204cdcfcab46e4b5e4992a6cefecba6a))
* **optimizer:** invalidate all modules on deps rebundle ([02053a2](https://github.com/vitejs/vite/commit/02053a2bfc2db82f277625fdf0563b257ef9c221))
* **optimizer:** use vite resolver for yarn 2 fallback ([475aae4](https://github.com/vitejs/vite/commit/475aae4ee29f9951f715d0ea98746202cfb586d4)), closes [#1778](https://github.com/vitejs/vite/issues/1778)
* fix pure css chunk removal ([d69d49d](https://github.com/vitejs/vite/commit/d69d49d4ae89b3f8ed37e1cf4345197634514546))
* **optimizer:** use all inputs for optimized entry matching ([9ecf52b](https://github.com/vitejs/vite/commit/9ecf52b27a3bdd0ce487e142fb45578eea76a3b6)), closes [#1769](https://github.com/vitejs/vite/issues/1769)
* dependency scan with esbuild when using non-HTML entrypoints ([#1772](https://github.com/vitejs/vite/issues/1772)) ([ca862a2](https://github.com/vitejs/vite/commit/ca862a2ea12853876e38100e8894fa22d9dbbc6e)), closes [#1763](https://github.com/vitejs/vite/issues/1763)
* hold missing dep requests while re-bundling ([8e28803](https://github.com/vitejs/vite/commit/8e288039a871b56803a7a5b66cc3766b6c2267db))
* more stable request hold ([be0e698](https://github.com/vitejs/vite/commit/be0e6981f764cb653d107966a755c8daa18d20c9))


### Reverts

* Revert "chore: remove unused logic" ([6b154f0](https://github.com/vitejs/vite/commit/6b154f0df3bd73cc3d3bdd91a999a7a4268e6c6b))


### BREAKING CHANGES

* **css:** the "css" property of build manifest entries is now an
array because it is possible for an entry to link to multiple generated
css files.



# [2.0.0-beta.52](https://github.com/vitejs/vite/compare/v2.0.0-beta.51...v2.0.0-beta.52) (2021-01-28)


### Bug Fixes

* **optimizer:** fix ?raw import and import with queries in pre-bundling ([2f1efa3](https://github.com/vitejs/vite/commit/2f1efa383f5f5e07618101898ce99ccbcbfc2654)), closes [#1759](https://github.com/vitejs/vite/issues/1759)
* always normalize fs prefix slashes ([99e4edd](https://github.com/vitejs/vite/commit/99e4edd468c5e27f66fd276b2ebf22d1c3424c31))
* **optimizer:** fix optimizer updates on new dep discovery ([b2110af](https://github.com/vitejs/vite/commit/b2110af04564f184bac9308926116138b9ab7aeb)), closes [#1755](https://github.com/vitejs/vite/issues/1755)



# [2.0.0-beta.51](https://github.com/vitejs/vite/compare/v2.0.0-beta.50...v2.0.0-beta.51) (2021-01-27)


### Bug Fixes

* avoid removing double slash in fileToUrl ([f6db155](https://github.com/vitejs/vite/commit/f6db155aa7a06e687d2982069db3d1619495afec))
* **build:** ensure lib mode file name is correctly inferred for scoped packages ([#1754](https://github.com/vitejs/vite/issues/1754)) ([c2e8806](https://github.com/vitejs/vite/commit/c2e88060624d73b544c31f92e5fee5d84503f6a4))
* **hmr:** fix hmr for [@fs](https://github.com/fs) urls ([b5987c1](https://github.com/vitejs/vite/commit/b5987c1f603f628ce6c075bbc83e37cafb5ea923)), closes [#1749](https://github.com/vitejs/vite/issues/1749)
* **optimizer:** attempt resolve node builtin first before externalizing ([74b55b8](https://github.com/vitejs/vite/commit/74b55b854200c3847cf13e7e036c0dc299820c64)), closes [#1746](https://github.com/vitejs/vite/issues/1746)
* allow ssr css preloads in preload-helper ([#1734](https://github.com/vitejs/vite/issues/1734)) ([1dfda16](https://github.com/vitejs/vite/commit/1dfda1618801b904b721fbd81d52a874b057ac65))
* handle vite client path with dollar signs ([#1732](https://github.com/vitejs/vite/issues/1732)) ([20bacf7](https://github.com/vitejs/vite/commit/20bacf7cacb7a0a180a9f38b18b306177a59b40d)), closes [#1423](https://github.com/vitejs/vite/issues/1423)
* scan on windows ([5f7698b](https://github.com/vitejs/vite/commit/5f7698b1f22545584e533bd0cd9abbb49c54d2b8))
* **optimizer:** entry matching for .mjs entries ([ebe71c4](https://github.com/vitejs/vite/commit/ebe71c42a481c140bbb1999f3bfa37dc15699170)), closes [#1739](https://github.com/vitejs/vite/issues/1739)
* css [@import](https://github.com/import) alias for windows ([71fcfdf](https://github.com/vitejs/vite/commit/71fcfdf219c0dd2aab6612e6b5ba89af1f63cd85))
* don't override resolver options ([#1740](https://github.com/vitejs/vite/issues/1740)) ([73196e5](https://github.com/vitejs/vite/commit/73196e517643af88a790ab5222d3e6b68dbbf987))
* resolve css [@import](https://github.com/import) relative imports without leading dot ([78eb32c](https://github.com/vitejs/vite/commit/78eb32c17998a96aff0f787cf4629b2683c6cd09)), closes [#1737](https://github.com/vitejs/vite/issues/1737)
* **optimizer:** do not perform tree-shaking for pre-bundling ([6b619c4](https://github.com/vitejs/vite/commit/6b619c4be210dbab0164f42ee4b358c3ac34a896))


### Code Refactoring

* adjust optimizeDeps options ([fd5e7c0](https://github.com/vitejs/vite/commit/fd5e7c01bae67f7dfc3e631aa87a8d08429b819a))


### Features

* auto re-run dep optimization on discovery of new imports ([470b4e4](https://github.com/vitejs/vite/commit/470b4e4a8cb040ec368b3702d82f8caa145b6698))
* dep optimizer entry option ([64ba807](https://github.com/vitejs/vite/commit/64ba807f25df82e51eeacbc11d525df75cf84235))
* import resolving + url rebasing for less ([f266bb7](https://github.com/vitejs/vite/commit/f266bb7417167e752bbbbd64fe3c82dceb13794b))
* new manifest format ([51bc1ec](https://github.com/vitejs/vite/commit/51bc1ecc1c130eba7eabdbaf1e5693d1c9967628))
* proper css resolving + sass import url rebase ([477f174](https://github.com/vitejs/vite/commit/477f1749d938d5ce95df3093de7154b749fe3667))
* use esbuild to scan imports ([d0f8b12](https://github.com/vitejs/vite/commit/d0f8b1248890c1eea0b81b1d6f61a81d3dc6e44a))
* **css:** support alias in css [@imports](https://github.com/imports) ([82d87d9](https://github.com/vitejs/vite/commit/82d87d91048b90282c4cae079ee142deb2a782d5)), closes [#650](https://github.com/vitejs/vite/issues/650)


### BREAKING CHANGES

* `optimizeDeps` options have been adjusted.
    - Dependencies are now automatically scanned from source code. There
      is no longer the need to specify deep imports.
    - `optimizeDeps.include` and `optimizeDeps.exclude` now expect type `string[]`.
    - `optimizeDpes.link` and `optimizeDeps.auto` are removed.
* the build manifest format has changed. See
https://vitejs.dev/guide/backend-integration.html for more details.



# [2.0.0-beta.50](https://github.com/vitejs/vite/compare/v2.0.0-beta.49...v2.0.0-beta.50) (2021-01-26)


### Bug Fixes

* json plugin error report line regex ([#1719](https://github.com/vitejs/vite/issues/1719)) ([35e1f52](https://github.com/vitejs/vite/commit/35e1f520c99581248f8241b82a1d568518e72d3f))
* **optimizer:** externalize cross-package imported css ([0599908](https://github.com/vitejs/vite/commit/0599908dcd233dd5108069ea501a651043c28d5c)), closes [#1722](https://github.com/vitejs/vite/issues/1722)
* **optimizer:** fix entry analysis fs read on case-sensitive systems ([1a9b321](https://github.com/vitejs/vite/commit/1a9b321c744b830fe8eb3275c4150eb763d9ba76)), closes [#1720](https://github.com/vitejs/vite/issues/1720)
* **optimizer:** fix entry matching edge case ([c5fe45f](https://github.com/vitejs/vite/commit/c5fe45fdd2c90436e2ee00754aedde2a32325ac6)), closes [#1661](https://github.com/vitejs/vite/issues/1661)
* **optimizer:** handle special case where esm entry gets converted to cjs by esbuild ([32413ce](https://github.com/vitejs/vite/commit/32413cec52ab12a835d3b3ec7a1e294946d11505)), closes [#1724](https://github.com/vitejs/vite/issues/1724)
* **optimizer:** pnp compat to match relative paths ([#1714](https://github.com/vitejs/vite/issues/1714)) ([8fb74f5](https://github.com/vitejs/vite/commit/8fb74f5d0983237a95aab683d800d3546b31729f))
* **sourcemap:** empty source map chain on nullified sourcemap ([52c9416](https://github.com/vitejs/vite/commit/52c94161b5c0f5eb0ad7e676a7b30a2de4a23116)), closes [#1726](https://github.com/vitejs/vite/issues/1726)
* properly handle base + path in hmr config ([1e67d66](https://github.com/vitejs/vite/commit/1e67d669318fac320c61ea00e0e01e972183fa27))


### Features

* allow speicfying ssr entry directly via build.ssr option ([45d8bf4](https://github.com/vitejs/vite/commit/45d8bf4da234f73badcf47e574e1e3ee3dc55b6c))



# [2.0.0-beta.49](https://github.com/vitejs/vite/compare/v2.0.0-beta.48...v2.0.0-beta.49) (2021-01-25)


### Bug Fixes

* **config:** fix native esm config loading on windows ([33d3cca](https://github.com/vitejs/vite/commit/33d3cca78607e14e4d0b13e7012d065a94d184b1))
* **optimizer:** entry matching on windows ([e6120d5](https://github.com/vitejs/vite/commit/e6120d582051f3535951698df40dc9b6fc485ae0))
* **optimizer:** fix output to entry matching logic ([6c96883](https://github.com/vitejs/vite/commit/6c96883d794d3396e890907df6b799d79a027420)), closes [#1704](https://github.com/vitejs/vite/issues/1704)
* **ssr:** generate same asset url links for ssr build ([68960f7](https://github.com/vitejs/vite/commit/68960f7867be13cfdce9ea49a8cc05448dff5e60)), closes [#1711](https://github.com/vitejs/vite/issues/1711)
* **watcher:** ensure only add normalized file paths ([a19c456](https://github.com/vitejs/vite/commit/a19c4565542c2c3575ab47642f80737a3bf26f3a))
* **watcher:** watch fs specific root paths ([64d2c17](https://github.com/vitejs/vite/commit/64d2c1772a57b024373e33015740c11c172dba85))
* do not move css modules to vendor chunk ([3d55e83](https://github.com/vitejs/vite/commit/3d55e8304e0faa71aec49326901048c46d196210)), closes [#1703](https://github.com/vitejs/vite/issues/1703)
* fix hmr.path option normalization ([cbeb9ba](https://github.com/vitejs/vite/commit/cbeb9ba7c7a192e61279fb00b543b81843663bc1)), closes [#1705](https://github.com/vitejs/vite/issues/1705)



# [2.0.0-beta.48](https://github.com/vitejs/vite/compare/v2.0.0-beta.47...v2.0.0-beta.48) (2021-01-25)


### Bug Fixes

* externalize known css types during dep-prebundling ([02a0324](https://github.com/vitejs/vite/commit/02a0324a56fcc3659ace4b62f96b2a8b10979f4c)), closes [#1695](https://github.com/vitejs/vite/issues/1695)
* fallback to static middleware on unfound source maps ([2096309](https://github.com/vitejs/vite/commit/2096309bee0f4ad838cde2a9dd9114b819e462c4))
* preload marker incorrect replacement ([7f83deb](https://github.com/vitejs/vite/commit/7f83deb7fe5add6117f8f715fc3165511761d07b))
* remove preload markers in all cases ([6cd2d35](https://github.com/vitejs/vite/commit/6cd2d35d791311de953b7a832a877b1c98e2b2ed)), closes [#1694](https://github.com/vitejs/vite/issues/1694)
* resolve library entry ([3240db1](https://github.com/vitejs/vite/commit/3240db19d33f0816e3c52a5042161a94753879d9))


### Features

* resolved ids rollup compat for win32 ([#1693](https://github.com/vitejs/vite/issues/1693)) ([e2137b7](https://github.com/vitejs/vite/commit/e2137b71a5a82580b2cf45e84ead136052014ac7)), closes [#1522](https://github.com/vitejs/vite/issues/1522)



# [2.0.0-beta.47](https://github.com/vitejs/vite/compare/v2.0.0-beta.46...v2.0.0-beta.47) (2021-01-24)


### Bug Fixes

* do not apply json plugin to commonjs proxy ([a92f430](https://github.com/vitejs/vite/commit/a92f4303253c9423093bedad6b06744d66dd1d39)), closes [#1679](https://github.com/vitejs/vite/issues/1679)
* esbuild optimizer yarn 2 pnp compat ([028c3bb](https://github.com/vitejs/vite/commit/028c3bb1a6c5f56eaa7f8f122200d6262a1a8683)), closes [#1688](https://github.com/vitejs/vite/issues/1688)
* fix incorrect preload placeholder regex ([5ca43ef](https://github.com/vitejs/vite/commit/5ca43ef6e91e41f09e06d92adef79953a3df9782)), closes [#1686](https://github.com/vitejs/vite/issues/1686)
* fix server.watch option ignore overwriting defaults ([#1680](https://github.com/vitejs/vite/issues/1680)) ([33cffa3](https://github.com/vitejs/vite/commit/33cffa3910600c5adfb10f2cab07029f1ff8f35f))


### Performance Improvements

* **build:** improve performance of default vendor chunk splitting ([#1690](https://github.com/vitejs/vite/issues/1690)) ([0bed9c4](https://github.com/vitejs/vite/commit/0bed9c44b2c89ad4fb7439907959f78d946b42cd))



# [2.0.0-beta.46](https://github.com/vitejs/vite/compare/v2.0.0-beta.45...v2.0.0-beta.46) (2021-01-24)


### Bug Fixes

* **css:** fix extract concurrency issue when disabling cssCodeSplit ([4ac7e7e](https://github.com/vitejs/vite/commit/4ac7e7ec9915bd044454f90a6a3d5a9676b3615c))



# [2.0.0-beta.45](https://github.com/vitejs/vite/compare/v2.0.0-beta.44...v2.0.0-beta.45) (2021-01-24)


### Bug Fixes

* **hmr:** fix nested hmr accept calls with base ([2950c3c](https://github.com/vitejs/vite/commit/2950c3c278e20174184e44c194393b098c0d4305))
* **hmr:** preserve host when updating link CSS ([60f9782](https://github.com/vitejs/vite/commit/60f9782a8481a4ce4d4c90ca246f5de44065d314)), closes [#1665](https://github.com/vitejs/vite/issues/1665)
* **html:** ensure quote in rebased asset urls in html ([7306610](https://github.com/vitejs/vite/commit/73066105727e669fe15d926fbe07d1788a469844)), closes [#1668](https://github.com/vitejs/vite/issues/1668)
* **import-anaysis:** markPos out-of-range  for overwrite ([#1671](https://github.com/vitejs/vite/issues/1671)) ([226e984](https://github.com/vitejs/vite/commit/226e9849253677770f11f8a26e6ec205067dc902))
* **optimizer:** repsect alias in pre-bundling ([2824d06](https://github.com/vitejs/vite/commit/2824d067d5239b506f93dc9c073c21d7e059bbe3)), closes [#1674](https://github.com/vitejs/vite/issues/1674)
* **resolve:** handle paths starting with slash in entry fields ([13da32e](https://github.com/vitejs/vite/commit/13da32e9ce22b1916a1b98bba7ad83bd145563c1)), closes [#1676](https://github.com/vitejs/vite/issues/1676)
* import analysis dynamic import check ([d4909b9](https://github.com/vitejs/vite/commit/d4909b936994d4fec37dfbafd27cd24494de8d14))
* revert trailing slash handling + improve dev base usage ([01e9ac0](https://github.com/vitejs/vite/commit/01e9ac0222dcc36c075c25e3fe8f7e8881867e9c)), closes [#1664](https://github.com/vitejs/vite/issues/1664)
* support empty, relative and external base values ([00bc446](https://github.com/vitejs/vite/commit/00bc4466567bd5613d67abd1bdf46d9c9cb23a80)), closes [#1669](https://github.com/vitejs/vite/issues/1669)


### Features

* default vendor chunk splitting ([f6b58a0](https://github.com/vitejs/vite/commit/f6b58a0f535b1c26f9c1dfda74c28c685402c3c9))
* disable prompts and clearScreen on CI ([63dd1a2](https://github.com/vitejs/vite/commit/63dd1a2829ea0764c12e11f2f3510bc1c096febf)), closes [#1673](https://github.com/vitejs/vite/issues/1673)
* source map for optimized deps ([972b13e](https://github.com/vitejs/vite/commit/972b13e09f9f0d43de9b7fb1d7bd706b4a10984b))
* support stringifying json ([98c321b](https://github.com/vitejs/vite/commit/98c321b3694dc77dd66e8064f14467e909832171)), closes [#1672](https://github.com/vitejs/vite/issues/1672)
* vite preview command for previewing build output ([a198990](https://github.com/vitejs/vite/commit/a198990efe4f96c2155928ac23264437d393d54e)), closes [#1627](https://github.com/vitejs/vite/issues/1627)



# [2.0.0-beta.44](https://github.com/vitejs/vite/compare/v2.0.0-beta.43...v2.0.0-beta.44) (2021-01-23)


### Bug Fixes

* esbuild dep resolving on windows ([62e4d72](https://github.com/vitejs/vite/commit/62e4d724a8a008cb6bd6f2122753880ec3568192))



# [2.0.0-beta.43](https://github.com/vitejs/vite/compare/v2.0.0-beta.42...v2.0.0-beta.43) (2021-01-23)


### Bug Fixes

* **optimizer:** force vite resolver for esbuild pre-bundle ([4c4d629](https://github.com/vitejs/vite/commit/4c4d629c391415351c797cf9b9c54d22be6244fe))



# [2.0.0-beta.42](https://github.com/vitejs/vite/compare/v2.0.0-beta.41...v2.0.0-beta.42) (2021-01-23)


### Bug Fixes

* **optimizer:** ensure esbuild use vite-resolved entries ([bdb9b3c](https://github.com/vitejs/vite/commit/bdb9b3c5a5c8da83d8b8082e936cb3cc16eeb1e0))



# [2.0.0-beta.41](https://github.com/vitejs/vite/compare/v2.0.0-beta.40...v2.0.0-beta.41) (2021-01-23)


### Bug Fixes

* lower .mjs resolve priority ([b15e90e](https://github.com/vitejs/vite/commit/b15e90e6893582d04f9506ef56cc9d03c9c6d775)), closes [#1660](https://github.com/vitejs/vite/issues/1660)



# [2.0.0-beta.40](https://github.com/vitejs/vite/compare/v2.0.0-beta.39...v2.0.0-beta.40) (2021-01-23)


### Bug Fixes

* **optimizer:** compiled esmdoule interop ([6826624](https://github.com/vitejs/vite/commit/68266245338d4f1c27d9552d5d54eff3420af8b6)), closes [#1659](https://github.com/vitejs/vite/issues/1659)



# [2.0.0-beta.39](https://github.com/vitejs/vite/compare/v2.0.0-beta.38...v2.0.0-beta.39) (2021-01-23)


### Bug Fixes

* **optimizer:** fix es interop heuristics for entry with only export * from ([ef1a7e3](https://github.com/vitejs/vite/commit/ef1a7e33cc19bac7893bca85b6df14adeb847516))
* **ssr:** do not inject ?import query for ssr transforms ([7d26119](https://github.com/vitejs/vite/commit/7d261191e5ebf0c2fede0c6fc82137999d58cc5c)), closes [#1655](https://github.com/vitejs/vite/issues/1655)
* hmr port fallback in middlewareMode ([36a9456](https://github.com/vitejs/vite/commit/36a94560399e03cdbdbdbdb16913c05deb87ab9b))
* **ssr:** avoid resolving externals to mjs ([3955fe3](https://github.com/vitejs/vite/commit/3955fe37fe4498e6c7df122376a942d63afe6acb))
* file dir resolve should prioritize package.json ([ce2d49a](https://github.com/vitejs/vite/commit/ce2d49ab396aa7b4ed582650e569d7f2f6d3ef9f))
* **ssr:** remove import query in ssrLoadModule ([80473c1](https://github.com/vitejs/vite/commit/80473c1423209824d143df77b38f1bdb8723f47b))



# [2.0.0-beta.38](https://github.com/vitejs/vite/compare/v2.0.0-beta.37...v2.0.0-beta.38) (2021-01-23)


### Bug Fixes

* **dev:** remove comment for sourcemap reference at debug ([#1658](https://github.com/vitejs/vite/issues/1658)) ([16248c0](https://github.com/vitejs/vite/commit/16248c02844c5447eeb7c441cc4b051becef2346))
* **optimizer:** improve exports analysis ([406cbea](https://github.com/vitejs/vite/commit/406cbeaa4f52472ce356980840f1a2a824eaa497))
* **ssr:** fix ssr transform edge cases ([f22ddbd](https://github.com/vitejs/vite/commit/f22ddbdb52d4579a5756215c320a13cd674a38a0)), closes [#1646](https://github.com/vitejs/vite/issues/1646)
* exclude spa-fallback middleware in middlewareMode ([#1645](https://github.com/vitejs/vite/issues/1645)) ([843c879](https://github.com/vitejs/vite/commit/843c87915082b36f7d1ffeb81515b45d5d65aabb))


### Code Refactoring

* remove optimizeDeps.plugins ([38524f6](https://github.com/vitejs/vite/commit/38524f6c6e864f9805dd0083da1dfa8ce20fa816))


### Features

* esbuild based dep pre-bundling ([6e7f652](https://github.com/vitejs/vite/commit/6e7f652d89dde43806a2323560486c9b4b771a35))
* support `base` option during dev, deprecate `build.base` ([#1556](https://github.com/vitejs/vite/issues/1556)) ([809d4bd](https://github.com/vitejs/vite/commit/809d4bd3bf62d3bc6b35f182178922d2ab2175f1))


### BREAKING CHANGES

* `optimizeDeps.plugins` has been removed. The dep
optimizer is now using `esbuild`, and all non-js files are automatically
externalized to be processed by Vite's transform pipeline when imported.



# [2.0.0-beta.37](https://github.com/vitejs/vite/compare/v2.0.0-beta.35...v2.0.0-beta.37) (2021-01-22)


### Bug Fixes

* **css:** fix url rewriting in [@imported](https://github.com/imported) css ([52ae44f](https://github.com/vitejs/vite/commit/52ae44fe97b53ce82633268030bb46594f385860)), closes [#1629](https://github.com/vitejs/vite/issues/1629)
* **manifest:** avoid chunks with same name overwriting one another ([cf81aa3](https://github.com/vitejs/vite/commit/cf81aa399b2df1ee8441a1b8922908f4e36358d6)), closes [#1632](https://github.com/vitejs/vite/issues/1632)
* **ssr:** do not inject inlined css in ssr build ([5d77665](https://github.com/vitejs/vite/commit/5d77665def42ffafc699a0006e4527536dfd1114)), closes [#1643](https://github.com/vitejs/vite/issues/1643)
* always reload when html is edited in middleware mode ([85c89be](https://github.com/vitejs/vite/commit/85c89bea9807090d928942a72b972183ebf8483a))
* handle esm config syntax error in Node 12 ([20cf718](https://github.com/vitejs/vite/commit/20cf718ac77abfce5656ee9836f8c06ddbbc440d)), closes [#1635](https://github.com/vitejs/vite/issues/1635)
* normalize paths for cjs optimized deps on windows ([#1631](https://github.com/vitejs/vite/issues/1631)) ([b462e33](https://github.com/vitejs/vite/commit/b462e33ce3d31df49ada436324a9c32cd5c9053a))
* still resolve jsnext fields ([4e0cd73](https://github.com/vitejs/vite/commit/4e0cd7384e850e4b7f23b68e5b591bb717650b79))


### Features

* allow inline postcss config ([6bd2140](https://github.com/vitejs/vite/commit/6bd21402a9e5955433656024f5548f12b12ea2fa)), closes [#1061](https://github.com/vitejs/vite/issues/1061)
* hmr for glob import ([edd2fd9](https://github.com/vitejs/vite/commit/edd2fd9de904a194f25e18136dfe298c7bcbbd8d))



# [2.0.0-beta.36](https://github.com/vitejs/vite/compare/v2.0.0-beta.35...v2.0.0-beta.36) (2021-01-21)


### Bug Fixes

* always reload when html is edited in middleware mode ([85c89be](https://github.com/vitejs/vite/commit/85c89bea9807090d928942a72b972183ebf8483a))
* still resolve jsnext fields ([6e06108](https://github.com/vitejs/vite/commit/6e061089c62898086c07fad7154b178446a18da5))


### Features

* allow inline postcss config ([6bd2140](https://github.com/vitejs/vite/commit/6bd21402a9e5955433656024f5548f12b12ea2fa)), closes [#1061](https://github.com/vitejs/vite/issues/1061)
* hmr for glob import ([edd2fd9](https://github.com/vitejs/vite/commit/edd2fd9de904a194f25e18136dfe298c7bcbbd8d))



# [2.0.0-beta.35](https://github.com/vitejs/vite/compare/v2.0.0-beta.34...v2.0.0-beta.35) (2021-01-20)


### Bug Fixes

* allow direct inspection of static file via browser ([a3c334f](https://github.com/vitejs/vite/commit/a3c334f66dbe1e5c49c4e5d77381aa0098c4a8a9)), closes [#1612](https://github.com/vitejs/vite/issues/1612)
* also resolve for module condition ([3a3029e](https://github.com/vitejs/vite/commit/3a3029effa0b83775f02fbd9469ef104eb6adb33)), closes [#1583](https://github.com/vitejs/vite/issues/1583)
* do not apply jsxInject on ts files ([a72a59c](https://github.com/vitejs/vite/commit/a72a59c55355a2a247b84178e63ce8c7cc1d7564))
* inline async css for legacy builds ([940d483](https://github.com/vitejs/vite/commit/940d48333f6572314576da9312f36018fd70bdc8))
* manually test global regex codeframeRE index ([#1608](https://github.com/vitejs/vite/issues/1608)) ([20d6c0f](https://github.com/vitejs/vite/commit/20d6c0fae160e25ab6cb76484baf910388dccdc6))
* properly format css pre-processor errors from [@imported](https://github.com/imported) files ([ec18bde](https://github.com/vitejs/vite/commit/ec18bde7ee4045a47362240a6f5ff4997657c7ba)), closes [#1600](https://github.com/vitejs/vite/issues/1600) [#1601](https://github.com/vitejs/vite/issues/1601)
* **asset:** use stricter asset url marker and regex ([e6c8478](https://github.com/vitejs/vite/commit/e6c8478dd765e63f56e2c4559daf03f976f60b4c)), closes [#1602](https://github.com/vitejs/vite/issues/1602)
* **plugin-dynamic-import:** include assetDir in dynamic import polyfill module path ([#1610](https://github.com/vitejs/vite/issues/1610)) ([47ff0f4](https://github.com/vitejs/vite/commit/47ff0f4307da6a90db2fc43fcf0aaffdb9e36643))
* **resolve:** get pkg  from importer for relative id ([#1599](https://github.com/vitejs/vite/issues/1599)) ([c821f09](https://github.com/vitejs/vite/commit/c821f094c25a7acde87b868dced265aa6e792a57))


### Features

* **manifest:** include dynamic entries and dynamic imports ([#1609](https://github.com/vitejs/vite/issues/1609)) ([9ed4908](https://github.com/vitejs/vite/commit/9ed49085ae860fb96d51ac50845f96ceb9fa649f))
* detect and warn against imports to transitively optimized deps ([3841e70](https://github.com/vitejs/vite/commit/3841e702213efac178aa90ab01825a813d3b4819)), closes [#1543](https://github.com/vitejs/vite/issues/1543)



# [2.0.0-beta.34](https://github.com/vitejs/vite/compare/v2.0.0-beta.33...v2.0.0-beta.34) (2021-01-20)


### Bug Fixes

* default changeOrigin to true in proxy option shorthand ([b008bd5](https://github.com/vitejs/vite/commit/b008bd59674c6d46ca41108b1c9d5076374bd1b8)), closes [#1577](https://github.com/vitejs/vite/issues/1577)
* emit css only once when there are multiple outputs ([6bce108](https://github.com/vitejs/vite/commit/6bce1081991501f3779bff1a81e5dd1e63e5d38e)), closes [#1590](https://github.com/vitejs/vite/issues/1590)
* **optimizer:** handle commonjs require css ([#1568](https://github.com/vitejs/vite/issues/1568)) ([3d09b50](https://github.com/vitejs/vite/commit/3d09b50b8774cf85a8c1dee24b3e379cbd3e9eb5)), closes [#1566](https://github.com/vitejs/vite/issues/1566)
* handle legacy chunks in manifest ([123b6f6](https://github.com/vitejs/vite/commit/123b6f67f7e159d098109d5c65a74dc0d17bd495)), closes [#1551](https://github.com/vitejs/vite/issues/1551)
* use safe dynamic import rewrite ([5cb02ce](https://github.com/vitejs/vite/commit/5cb02ce0b24ff167b7da3e2de9b0237186d9e95a)), closes [#1563](https://github.com/vitejs/vite/issues/1563)
* **hmr:** fix hmr invalidation on circular deps ([ca8442c](https://github.com/vitejs/vite/commit/ca8442c19e51526e2fa75f0c4976941a2b9089e6)), closes [#1477](https://github.com/vitejs/vite/issues/1477)
* **resolve:** node resolve from virtual modules ([c6d5ed8](https://github.com/vitejs/vite/commit/c6d5ed833befafaaea14fbd2fb62a7ed8d58c409))



# [2.0.0-beta.33](https://github.com/vitejs/vite/compare/v2.0.0-beta.32...v2.0.0-beta.33) (2021-01-19)


### Bug Fixes

* fix ssr module invalidation infinite loop ([30885d1](https://github.com/vitejs/vite/commit/30885d1673a282a12e0c7471fc80236b72ebeb16)), closes [#1591](https://github.com/vitejs/vite/issues/1591)



# [2.0.0-beta.32](https://github.com/vitejs/vite/compare/v2.0.0-beta.31...v2.0.0-beta.32) (2021-01-19)


### Bug Fixes

* avoid preloading owner chunk ([61969d7](https://github.com/vitejs/vite/commit/61969d787200ab0b03179ecf2855c5b4aff3baa6))
* ssr transform check valid inMap ([bf4b3e9](https://github.com/vitejs/vite/commit/bf4b3e9b416bb0f2a8ee8bfce969d452429a8282))
* support resolving .json ext to be consistent with Node ([a1d1dde](https://github.com/vitejs/vite/commit/a1d1dde70c4626ab603ed07234fe296ef8d5a65f))


### Code Refactoring

* rename ViteDevServer.app -> ViteDevServer.middlewares ([394390a](https://github.com/vitejs/vite/commit/394390a983deccd8cbca101066db93f60577b810))


### Features

* import.meta.env.SSR ([fe7396d](https://github.com/vitejs/vite/commit/fe7396d3896d04db17f73ea265eebe0397414e65))
* ssr manifest for preload inference ([107e79e](https://github.com/vitejs/vite/commit/107e79e7b7d422f0d1dbe8b7b435636df7c6281c))
* **ssr:** isolated mode ([e954ed2](https://github.com/vitejs/vite/commit/e954ed25099d9217d30a5a4d38e5dfee5acee0fd))
* ssr sourcemap + stacktrace fix ([6cb04fa](https://github.com/vitejs/vite/commit/6cb04fa3b3a7a4ac4676a7b1c41d9d5068fae5de))


### BREAKING CHANGES

* `ViteDevServer.app` is now `ViteDevServer.middlewares`.
In addition, Vite no longer serves `index.html` in middleware mode. The
server using Vite as middleware is responsible for serving HTML with
`/@vite/client` injected.



# [2.0.0-beta.31](https://github.com/vitejs/vite/compare/v2.0.0-beta.30...v2.0.0-beta.31) (2021-01-18)


### Bug Fixes

* workaround for ts config + native esm w/ imports ([4a7d2eb](https://github.com/vitejs/vite/commit/4a7d2ebca1719d83c22d7dce5214e61f7906a772)), closes [#1560](https://github.com/vitejs/vite/issues/1560)
* **resolve:** also respect browser mapping of dependencies ([12b706d](https://github.com/vitejs/vite/commit/12b706d6ecd99c98f326deae53f9aa79cd8a81f4)), closes [#1547](https://github.com/vitejs/vite/issues/1547)



# [2.0.0-beta.30](https://github.com/vitejs/vite/compare/v2.0.0-beta.29...v2.0.0-beta.30) (2021-01-15)


### Bug Fixes

* **config:** delete cache correctly when restarting server ([#1541](https://github.com/vitejs/vite/issues/1541)) ([bd3b1bf](https://github.com/vitejs/vite/commit/bd3b1bfd83488b05a188a9d1c7093e3003721d91))
* **config:** load native esm ts config string with base64 encoding ([55b05db](https://github.com/vitejs/vite/commit/55b05dba3d157da72eaf9c445b0bb5084b9858d0)), closes [#1548](https://github.com/vitejs/vite/issues/1548)



# [2.0.0-beta.29](https://github.com/vitejs/vite/compare/v2.0.0-beta.28...v2.0.0-beta.29) (2021-01-14)


### Bug Fixes

* **optimizer:** fix empty exclude filter ([4579c38](https://github.com/vitejs/vite/commit/4579c382d4a1b0385510bb708f74305c87c4a68a))
* fix graceful shutdown on sigint ([fe7238c](https://github.com/vitejs/vite/commit/fe7238c530533d7ea7bff20ce97485669c7dfb46))
* warn failed source map load instead of erroring ([7a1261b](https://github.com/vitejs/vite/commit/7a1261b51695cbe7d41da6835c360b9bb26d189e))



# [2.0.0-beta.28](https://github.com/vitejs/vite/compare/v2.0.0-beta.27...v2.0.0-beta.28) (2021-01-14)


### Bug Fixes

* alias should work for optimized deps ([54dab71](https://github.com/vitejs/vite/commit/54dab71e41cdd9f516460d153b024d0c0cc05097))
* serve out of root static file on windows ([#1537](https://github.com/vitejs/vite/issues/1537)) ([506bf2d](https://github.com/vitejs/vite/commit/506bf2d542a27ee19a1b1b2d05aad845f4387cf6))
* **dev:** correct responce for html qurey ([#1526](https://github.com/vitejs/vite/issues/1526)) ([49d294d](https://github.com/vitejs/vite/commit/49d294d36d0f32d00a025a03017c9049d3f48ebd)), closes [#1524](https://github.com/vitejs/vite/issues/1524)
* **optimizer:** should respect rollup external during pre-bundling ([db97317](https://github.com/vitejs/vite/commit/db9731753abf36563172b02961ded54be23dd215)), closes [#1528](https://github.com/vitejs/vite/issues/1528)


### Features

* add clearScreen option ([c5c3298](https://github.com/vitejs/vite/commit/c5c32982f207055229b6bce61ce205d8d20db023))
* close server on sigint/sigterm ([4338d7d](https://github.com/vitejs/vite/commit/4338d7d6f32c8e0e67ff58f0cb8c1a9120294756)), closes [#1525](https://github.com/vitejs/vite/issues/1525)
* support specifying URL path via server.open option ([#1514](https://github.com/vitejs/vite/issues/1514)) ([25e9c44](https://github.com/vitejs/vite/commit/25e9c44992c8b868cec97dbdeddd3a4837d5bb07))
* support using vite as a middleware ([960b420](https://github.com/vitejs/vite/commit/960b42068579dddc2c216720a7f16d8d189e8225))



# [2.0.0-beta.27](https://github.com/vitejs/vite/compare/v2.0.0-beta.26...v2.0.0-beta.27) (2021-01-13)


### Bug Fixes

* transform import.meta.url in config files ([98e57de](https://github.com/vitejs/vite/commit/98e57deb9d16b23b7ae0c382cca49a9420443b47)), closes [#1511](https://github.com/vitejs/vite/issues/1511)


### Features

* **vite:** support RegExp strings as server.proxy keys ([#1510](https://github.com/vitejs/vite/issues/1510)) ([f39a2aa](https://github.com/vitejs/vite/commit/f39a2aafd35a70effc298d53b0b7539fbac79e89))
* warn unintended dependency during pre-bundling ([ae6cc27](https://github.com/vitejs/vite/commit/ae6cc27349e66945a0964635e6ad64933fe33960))



# [2.0.0-beta.26](https://github.com/vitejs/vite/compare/v2.0.0-beta.25...v2.0.0-beta.26) (2021-01-13)


### Bug Fixes

* properly externalize resolved external urls ([6cda88d](https://github.com/vitejs/vite/commit/6cda88d882ffcd5b3fdaa005296bfe1f0991925c))



# [2.0.0-beta.25](https://github.com/vitejs/vite/compare/v2.0.0-beta.24...v2.0.0-beta.25) (2021-01-12)


### Bug Fixes

* Revert "feat: allow browser new window view source ([#1496](https://github.com/vitejs/vite/issues/1496))" ([64fde38](https://github.com/vitejs/vite/commit/64fde3883e07f66fee6f6234f84ad35288a24b62)), closes [#1507](https://github.com/vitejs/vite/issues/1507)


### Features

* support aliasing to external url ([abf7844](https://github.com/vitejs/vite/commit/abf784403e1d9e36653ee4fd167c4cf341fd343f))



# [2.0.0-beta.24](https://github.com/vitejs/vite/compare/v2.0.0-beta.23...v2.0.0-beta.24) (2021-01-12)


### Bug Fixes

* **hmr:** watch file changes even when HMR is disabled ([#1504](https://github.com/vitejs/vite/issues/1504)) ([cc5fa6e](https://github.com/vitejs/vite/commit/cc5fa6efb3448e2f83b5d6d428e79803c8993657))
* always replace preload marker with value ([2d6f524](https://github.com/vitejs/vite/commit/2d6f5243e16f7debd7ba0de4bf22706df35ccf73))
* more consistent outDir formatting ([50bff79](https://github.com/vitejs/vite/commit/50bff797c536b08661791a833cfbb9179ff54422)), closes [#1497](https://github.com/vitejs/vite/issues/1497)
* show target build mode in logs ([#1498](https://github.com/vitejs/vite/issues/1498)) ([ae2e14b](https://github.com/vitejs/vite/commit/ae2e14baf1771c2ccdeece8bbc2b9bd11b279490))
* support import.meta.url in ts esm config file ([cf5f3ab](https://github.com/vitejs/vite/commit/cf5f3ab2c33aca6ab6bff8d600854f93586adcf0)), closes [#1499](https://github.com/vitejs/vite/issues/1499)


### Features

* allow browser new window view source ([#1496](https://github.com/vitejs/vite/issues/1496)) ([1629c54](https://github.com/vitejs/vite/commit/1629c546158253f155afecb55846771013f90ec0))
* require explicit option to empty outDir when it is out of root ([730d2f0](https://github.com/vitejs/vite/commit/730d2f0d8081e11c88b1151086d99b23e0c58823)), closes [#1501](https://github.com/vitejs/vite/issues/1501)



# [2.0.0-beta.23](https://github.com/vitejs/vite/compare/v2.0.0-beta.22...v2.0.0-beta.23) (2021-01-12)


### Bug Fixes

* fix ts config loading on windows ([ec370d2](https://github.com/vitejs/vite/commit/ec370d22db875cca0b2319073d9025b05e7ffc54)), closes [#1493](https://github.com/vitejs/vite/issues/1493)



# [2.0.0-beta.22](https://github.com/vitejs/vite/compare/v2.0.0-beta.21...v2.0.0-beta.22) (2021-01-11)


### Bug Fixes

* handle http proxy error ([4ca20f2](https://github.com/vitejs/vite/commit/4ca20f2e16c1bba0dc330c7e5879ca322b2ab21c)), closes [#1485](https://github.com/vitejs/vite/issues/1485)
* optimizer hash should take inline mode into account ([0aed0e8](https://github.com/vitejs/vite/commit/0aed0e89f84aff26cfdf57879925a76fa696331d)), closes [#1490](https://github.com/vitejs/vite/issues/1490)
* support resolved Ids that start with null bytes ([7074414](https://github.com/vitejs/vite/commit/70744143cd09863412a59aad14de888067bd8531)), closes [#1471](https://github.com/vitejs/vite/issues/1471)
* **config:** support native esm config on windows + support TS config in native esm projects ([803f6da](https://github.com/vitejs/vite/commit/803f6da2ad04846c3ae2622e15b5a18f0691204e)), closes [#1487](https://github.com/vitejs/vite/issues/1487)


### Features

* **resolve:** support subpath patterns + production/development conditinals in exports field ([62cbd53](https://github.com/vitejs/vite/commit/62cbd53f25411ddfc7cfd5446c2f487a260da191))
* **server:** add strict-port option ([#1453](https://github.com/vitejs/vite/issues/1453)) ([0501084](https://github.com/vitejs/vite/commit/05010846cb266f540039f13e280b486c97803f03))



# [2.0.0-beta.21](https://github.com/vitejs/vite/compare/v2.0.0-beta.20...v2.0.0-beta.21) (2021-01-11)


### Bug Fixes

* properly remove dynamic import args for full dynamic imports ([d9c3fdb](https://github.com/vitejs/vite/commit/d9c3fdb4073d49d427d825007154e873d8aa3d9a))



# [2.0.0-beta.20](https://github.com/vitejs/vite/compare/v2.0.0-beta.19...v2.0.0-beta.20) (2021-01-11)


### Bug Fixes

* **optimizer:** exclude should not be resolve ([#1469](https://github.com/vitejs/vite/issues/1469)) ([f8c34ee](https://github.com/vitejs/vite/commit/f8c34eeb89e327f484293f3156119ba6d14f6aee))
* **resolve:** heuristics for browser vs. module field ([1865e6e](https://github.com/vitejs/vite/commit/1865e6ee4c3e07c0f4a199c1ba7e1c1c4f68862f)), closes [#1467](https://github.com/vitejs/vite/issues/1467)


### Features

* allow passing options to rollup commonjs plugin via build.commonjsOptions ([6ed8e28](https://github.com/vitejs/vite/commit/6ed8e286f149f9474e0fc624110de5f787551d62)), closes [#1460](https://github.com/vitejs/vite/issues/1460)
* async chunk loading optimizations ([e6f7fba](https://github.com/vitejs/vite/commit/e6f7fbad75c1b406b9a95060c5d2a42d3a8994a8))



# [2.0.0-beta.19](https://github.com/vitejs/vite/compare/v2.0.0-beta.18...v2.0.0-beta.19) (2021-01-10)


### Bug Fixes

* transform json in deep import ([#1459](https://github.com/vitejs/vite/issues/1459)) ([cf8342b](https://github.com/vitejs/vite/commit/cf8342bef45bebb05d020d4f220b12d2bf526256)), closes [#1458](https://github.com/vitejs/vite/issues/1458)



# [2.0.0-beta.18](https://github.com/vitejs/vite/compare/v2.0.0-beta.17...v2.0.0-beta.18) (2021-01-10)


### Bug Fixes

* fix dynamic import with parent relative paths ([bbfe06c](https://github.com/vitejs/vite/commit/bbfe06ce1af8f89490032e609377c6516f7da773)), closes [#1461](https://github.com/vitejs/vite/issues/1461)
* **optimizer:** properly externalize css/asset imports in optimized deps ([5d180db](https://github.com/vitejs/vite/commit/5d180db4bd19e26de20bb816d594226b4d492804)), closes [#1443](https://github.com/vitejs/vite/issues/1443)


### Features

* **optimizer:** support specifying plugins for the optimizer ([1ea0168](https://github.com/vitejs/vite/commit/1ea016823975f3d0e37bf7b65614eded213e0869))



# [2.0.0-beta.17](https://github.com/vitejs/vite/compare/v2.0.0-beta.16...v2.0.0-beta.17) (2021-01-10)


### Code Refactoring

* support glob import under `import.meta.glob` ([23d0f2b](https://github.com/vitejs/vite/commit/23d0f2b85d8eb8677e30456342000cabed8e684e))


### BREAKING CHANGES

* Glob import syntax has changed. The feature is now
exposed under `import.meta.glob` (lazy, exposes dynamic import functions)
and `import.meta.globEager` (eager, exposes already imported modules).



# [2.0.0-beta.16](https://github.com/vitejs/vite/compare/v2.0.0-beta.15...v2.0.0-beta.16) (2021-01-09)


### Bug Fixes

* inject css link when cssCodeSplit is disabled ([51a02ff](https://github.com/vitejs/vite/commit/51a02ff902c3afa4dff76b43f75b9221768cd7f8)), closes [#1141](https://github.com/vitejs/vite/issues/1141)
* set NODE_ENV for build ([d7ceabe](https://github.com/vitejs/vite/commit/d7ceabe92efe1c523ee05a6941e3f5042733b2bf)), closes [#1445](https://github.com/vitejs/vite/issues/1445) [#1452](https://github.com/vitejs/vite/issues/1452)


### Features

* allow tag injection after body open (body-prepend) ([#1435](https://github.com/vitejs/vite/issues/1435)) ([432487e](https://github.com/vitejs/vite/commit/432487e24cb8688c86502e3b4e284e25c81b7dd8))



# [2.0.0-beta.15](https://github.com/vitejs/vite/compare/v2.0.0-beta.14...v2.0.0-beta.15) (2021-01-09)


### Bug Fixes

* **hmr:** ensure all modules are fetched as import ([98bc767](https://github.com/vitejs/vite/commit/98bc7675a0f515ec6a908c6f18b2947a4a117836))



# [2.0.0-beta.14](https://github.com/vitejs/vite/compare/v2.0.0-beta.13...v2.0.0-beta.14) (2021-01-09)


### Features

* support ../ paths in glob import ([7f399e1](https://github.com/vitejs/vite/commit/7f399e1a628240fdcd866cddc45c5522b07fd7f6))



# [2.0.0-beta.13](https://github.com/vitejs/vite/compare/v2.0.0-beta.12...v2.0.0-beta.13) (2021-01-09)


### Bug Fixes

* always rebase path against root ([d704b7c](https://github.com/vitejs/vite/commit/d704b7c55fcbf347b5277a1d92dee4cc9583bab5)), closes [#1413](https://github.com/vitejs/vite/issues/1413)
* handle potential imports that has no correspodning chunks ([d47e10c](https://github.com/vitejs/vite/commit/d47e10c77d642b0446cb6ea1d5fd5a33346e9391))
* raw fetch requests should not be transformed ([0356c3c](https://github.com/vitejs/vite/commit/0356c3c5193a5aeb8586e5588c8c873df7a1a427)), closes [#1433](https://github.com/vitejs/vite/issues/1433)
* skip cjs rewrite for export * declarations ([cca015b](https://github.com/vitejs/vite/commit/cca015b1c46fff41e047a92430937f31df5e6dfb)), closes [#1439](https://github.com/vitejs/vite/issues/1439)
* **cli:** fix help for --root ([#1429](https://github.com/vitejs/vite/issues/1429)) ([7a55c5b](https://github.com/vitejs/vite/commit/7a55c5be36a6d04a5a1e434147f4208c4a64c492))
* **dev:** decode url before `sirv` resolve ([#1432](https://github.com/vitejs/vite/issues/1432)) ([7cc3cf1](https://github.com/vitejs/vite/commit/7cc3cf1044594297320ed62e1b38b27883f3f6c0)), closes [#1426](https://github.com/vitejs/vite/issues/1426)


### Features

* allow user define to overwrite default process.env. defines ([351ad4e](https://github.com/vitejs/vite/commit/351ad4ee56d46eb8837b6a90af19ef953e3fe28b))
* build support for data uri import ([4fd0b86](https://github.com/vitejs/vite/commit/4fd0b8615ef5ecff704ed44cadece613368cf18b))
* support import "glob:./*" ([8d8e2cc](https://github.com/vitejs/vite/commit/8d8e2cc9ea0e1cc8f620c0a9d143294c1efb37b0))



# [2.0.0-beta.12](https://github.com/vitejs/vite/compare/v2.0.0-beta.11...v2.0.0-beta.12) (2021-01-07)


### Bug Fixes

* **plugin-legacy:** avoid esbuild transform on legacy chunks ([7734105](https://github.com/vitejs/vite/commit/7734105093c6dabf64da6bfc11486aa9ac62efea))



# [2.0.0-beta.11](https://github.com/vitejs/vite/compare/v2.0.0-beta.10...v2.0.0-beta.11) (2021-01-07)


### Bug Fixes

* preserve html comments during dev ([b295400](https://github.com/vitejs/vite/commit/b2954009f48da0a0d3202eee802e51eb7a1fb6c5)), closes [#1420](https://github.com/vitejs/vite/issues/1420)
* **resolve:** respect exports env key order ([b58c860](https://github.com/vitejs/vite/commit/b58c860f1771deecb78e126dfe8b6f663bd5e7c9)), closes [#1418](https://github.com/vitejs/vite/issues/1418)
* avoid excessive quote in css public urls ([1437129](https://github.com/vitejs/vite/commit/1437129541b36c0453fcecb1f1d44b574cc3326f)), closes [#1399](https://github.com/vitejs/vite/issues/1399)
* do not rewrite dynamic import if format is not native es ([eb35bd5](https://github.com/vitejs/vite/commit/eb35bd546333f4edea94607d05581b887b2ce9b6))
* esbuild transform should filter id with and wihtout query ([4cda5be](https://github.com/vitejs/vite/commit/4cda5beb9f62c766dc8a8ab5d7b17704355348fc))
* fix cache invalidation for non-optimized deps with cross imports ([11c407a](https://github.com/vitejs/vite/commit/11c407a085e9facd810914a5d4256946c11a1ca9)), closes [#1401](https://github.com/vitejs/vite/issues/1401)
* html transform should not render boolean attr with false value ([a59ffef](https://github.com/vitejs/vite/commit/a59ffefe1087a45cc4c13ab9e15e1d43ccac114a))
* remove vue from optimize ignore list ([9eab790](https://github.com/vitejs/vite/commit/9eab79088079e95fb32f458a4bf573af7618bec6)), closes [#1408](https://github.com/vitejs/vite/issues/1408)
* support serving extension-less files in /public ([a7bca9c](https://github.com/vitejs/vite/commit/a7bca9c324db280ad3fa8255a36dee838a29255b)), closes [#1364](https://github.com/vitejs/vite/issues/1364)
* **build:** inline quotes css url to base64 ([#1412](https://github.com/vitejs/vite/issues/1412)) ([9b5b352](https://github.com/vitejs/vite/commit/9b5b3526de3288fc5d0e0a40fd80378db24674a1)), closes [#1409](https://github.com/vitejs/vite/issues/1409) [#1413](https://github.com/vitejs/vite/issues/1413)


### Code Refactoring

* pass `configFile` via inline config instead of extra arg in most ([24b3b5a](https://github.com/vitejs/vite/commit/24b3b5a4e4402543d45bd8e3e4ff9ff26c09d7cb))


### Features

* support specifying mode in user config ([396bbf8](https://github.com/vitejs/vite/commit/396bbf8c869b23360a39bc4d99b760e25645c84b)), closes [#1380](https://github.com/vitejs/vite/issues/1380)
* **plugin-legacy:** @vitejs/plugin-legacy ([8c34870](https://github.com/vitejs/vite/commit/8c34870040f8c2f4be7d00245a3683f9e64d894e))
* **proxy:** add rewrite support for ws ([#1407](https://github.com/vitejs/vite/issues/1407)) ([fa3bc34](https://github.com/vitejs/vite/commit/fa3bc34e23e757d57ca42e66c41dc8e712ae5547))
* also expose correspodning chunk in build html transform ([b2f4836](https://github.com/vitejs/vite/commit/b2f4836ea83d7ba86c2ef3a082773d5045f2e7d9))
* expose loadConfigFromFile API ([#1403](https://github.com/vitejs/vite/issues/1403)) ([9582171](https://github.com/vitejs/vite/commit/958217177c3173b7e5dec7f29048a2e83168649b))


### BREAKING CHANGES

* the following JavaScript APIs now expect `configFile`
as a property of the config object passed in instead of an argument:

    - `createServer`
    - `build`
    - `resolveConfig`



# [2.0.0-beta.10](https://github.com/vitejs/vite/compare/v2.0.0-beta.9...v2.0.0-beta.10) (2021-01-06)


### Bug Fixes

* **alias:** normalize alias behavior when there is ending slash ([c4739a3](https://github.com/vitejs/vite/commit/c4739a3f6d341db220cc5732857cf194c7cecc0d)), closes [#1363](https://github.com/vitejs/vite/issues/1363)
* **build:** Pass `allowNodeBuiltins` to rollup instead of empty array (Fixes [#1392](https://github.com/vitejs/vite/issues/1392)) ([#1393](https://github.com/vitejs/vite/issues/1393)) ([f209ad9](https://github.com/vitejs/vite/commit/f209ad9c858235ea317db6beb3bf2ab5ec26c153))
* avoid replacing process.env member expression ([c8f4bb9](https://github.com/vitejs/vite/commit/c8f4bb92337c8882f238ea395f169af96a59d2ae)), closes [#930](https://github.com/vitejs/vite/issues/930)



# [2.0.0-beta.9](https://github.com/vitejs/vite/compare/v2.0.0-beta.8...v2.0.0-beta.9) (2021-01-06)


### Bug Fixes

* properly handle browser: false resolving ([da09320](https://github.com/vitejs/vite/commit/da09320e3671dbf08a5f8c4a78bd273f75fdcd7d)), closes [#1386](https://github.com/vitejs/vite/issues/1386)
* properly handle ts worker source ([eea1224](https://github.com/vitejs/vite/commit/eea122434740a60d353df54cb4dc108e29d4ef87)), closes [#1385](https://github.com/vitejs/vite/issues/1385)


### Features

* **env:** also expose VITE_ variables from actual env ([956cd2c](https://github.com/vitejs/vite/commit/956cd2c76e69ba046f51a36af8e44ae9fb3a67ab))



# [2.0.0-beta.8](https://github.com/vitejs/vite/compare/v2.0.0-beta.7...v2.0.0-beta.8) (2021-01-05)


### Bug Fixes

* **resolve:** handle exports field w/ mapped directory ([724aa8a](https://github.com/vitejs/vite/commit/724aa8a5fcb0ccaea283b3bf065d29ebf2cdf5a2))


### Features

* **build:** default build target to 'modules' with dynamic import polyfill ([756e90f](https://github.com/vitejs/vite/commit/756e90ff9b7d0b838ac3a2d7a20c36c801f72d8c))
* allow boolean attr values in html transform tag descriptors ([#1381](https://github.com/vitejs/vite/issues/1381)) ([0fad96e](https://github.com/vitejs/vite/commit/0fad96e5cbff48efd3a13bb27580de894e1ec728))



# [2.0.0-beta.7](https://github.com/vitejs/vite/compare/v2.0.0-beta.6...v2.0.0-beta.7) (2021-01-05)


### Code Refactoring

* update client type usage ([245303c](https://github.com/vitejs/vite/commit/245303ca35ff2a40eca49e102b4f82cb1210f597))


### BREAKING CHANGES

* client types are now exposed under `vite/client.d.ts`.
It can now be included via the following `tsconfig.json`:

    ```ts
    {
      "compilerOptions": {
        "types": ["vite/client"]
      }
    }
    ```



# [2.0.0-beta.6](https://github.com/vitejs/vite/compare/v2.0.0-beta.5...v2.0.0-beta.6) (2021-01-05)


### Bug Fixes

* **css:** ensure options for .styl ([b3237ff](https://github.com/vitejs/vite/commit/b3237fff697b4b8b0e10adc9e0041f64c33fbc2d)), closes [#1351](https://github.com/vitejs/vite/issues/1351)
* **error-handling:** avoid serilaizing unnecessary error properties when seinding to client ([61aec65](https://github.com/vitejs/vite/commit/61aec651b470d5b97f2340a1b692b82cfe0c8ba5)), closes [#1373](https://github.com/vitejs/vite/issues/1373)
* **optimizer:** optimizer should not be affected by config rollup options ([ba08310](https://github.com/vitejs/vite/commit/ba08310b9e82668670af8a95e889e7cb68388e84)), closes [#1372](https://github.com/vitejs/vite/issues/1372)
* support aliases in html references ([68eac64](https://github.com/vitejs/vite/commit/68eac643f907fb4d57bd25925a342692441b1d97)), closes [#1363](https://github.com/vitejs/vite/issues/1363)
* **optimizer:** resolve linked dep from relative root ([#1375](https://github.com/vitejs/vite/issues/1375)) ([034bbcd](https://github.com/vitejs/vite/commit/034bbcd1738426d89e6c942f27dd1ccc8ede3990))


### Code Refactoring

* remove the need for specifying `transformInclude` ([99522d0](https://github.com/vitejs/vite/commit/99522d0edf06da4b8519c209f5f928cdf2951105))


### Features

* exclude vue from optimization ([1046fe0](https://github.com/vitejs/vite/commit/1046fe008b3288633bf8b38efdc2401a5ad2bf47))
* improve import analysis fail warning ([2b39fce](https://github.com/vitejs/vite/commit/2b39fce9450dc0d8bc99b06a6d757f4e48193001)), closes [#1368](https://github.com/vitejs/vite/issues/1368)


### BREAKING CHANGES

* `transformInclude` option has been removed and is no
longer necessary. This allows full dynamic imports to custom file types
to automatically qualify for the transform pipeline.

    - All requests that accept `*/*` AND is not declared an asset type
    will now qualify for the transform pipeline.

    - To exclude an asset type from being transformed when requested
    directly, declare it as asset via `config.assetsInclude`.



# [2.0.0-beta.5](https://github.com/vitejs/vite/compare/v2.0.0-beta.4...v2.0.0-beta.5) (2021-01-05)


### Bug Fixes

* only append dep version query for known types ([42cd8b2](https://github.com/vitejs/vite/commit/42cd8b217de6afb53163eef69e96514c75de4443))
* **css:** fix css comment removal ([7b9dee0](https://github.com/vitejs/vite/commit/7b9dee020785022acaa8e6989dcb2cc7ec03c3f2)), closes [#1359](https://github.com/vitejs/vite/issues/1359)
* **css:** inline css in all non-entry split chunks ([e90ff76](https://github.com/vitejs/vite/commit/e90ff76d1c6d5ad1d079c953ba4fbfc84be73185)), closes [#1356](https://github.com/vitejs/vite/issues/1356)
* do not bundle resolve for yarn 2 compat ([3524e96](https://github.com/vitejs/vite/commit/3524e96da0de59e5dddf2210dc78e2a1de3f07e0)), closes [#1353](https://github.com/vitejs/vite/issues/1353)
* do not error on unresolved commonjs externals ([60a4708](https://github.com/vitejs/vite/commit/60a470880034fcd7e54c15b4cf92f738b973a3df)), closes [#1339](https://github.com/vitejs/vite/issues/1339)
* only allow built-ins as externals if building for ssr ([804c9a3](https://github.com/vitejs/vite/commit/804c9a30e673386c419a0582d0da11f805c285c4))
* run mutiple output builds sequantially ([ab80522](https://github.com/vitejs/vite/commit/ab805228e55bd79275b6ac67b0408419a8ab5c70))


### Features

* **types:** separate client type shims from main types ([0cddbbc](https://github.com/vitejs/vite/commit/0cddbbc4bfc8e85329ba710117b9aec1d67d318d))
* default clean-css level to 1 + expose options ([ef100d0](https://github.com/vitejs/vite/commit/ef100d09cbd1c6745108afc2877396fe69b08bdd)), closes [#936](https://github.com/vitejs/vite/issues/936)
* support plugin.apply ([d914b54](https://github.com/vitejs/vite/commit/d914b542450cd7b4bbeb057a0fee8f79efd2bb9d))



# [2.0.0-beta.4](https://github.com/vitejs/vite/compare/v2.0.0-beta.3...v2.0.0-beta.4) (2021-01-04)


### Bug Fixes

* stop service in build esbuild plugin as well ([1a90b4e](https://github.com/vitejs/vite/commit/1a90b4e50250c4011a058e9e121b7b80caff888e))
* **build:** rollup import resolving message ([#1336](https://github.com/vitejs/vite/issues/1336)) [skip ci] ([87d55f4](https://github.com/vitejs/vite/commit/87d55f43e90edb36c2f0d49d71ffadd20f82e97a))
* **resolve:** always prioritize browser field ([409988f](https://github.com/vitejs/vite/commit/409988fbbb5d854ccbbae0dd81f757eb42e24c40))
* [@fs](https://github.com/fs) paths resolving for win32 ([#1317](https://github.com/vitejs/vite/issues/1317)) ([0a94c88](https://github.com/vitejs/vite/commit/0a94c88238f265a14c116c2f1306d3be74b182e6))
* do not error on css deep imports ([25adf1e](https://github.com/vitejs/vite/commit/25adf1eefaf6817f9443365f5ee3fcf0d63ffd6f))
* ensure consistent module entry urls by removing import query ([2b82e84](https://github.com/vitejs/vite/commit/2b82e84a272db2a4269d742dd7b9a8a1ad8351dd)), closes [#1321](https://github.com/vitejs/vite/issues/1321)
* load source map from sourceMappingURL comment ([#1327](https://github.com/vitejs/vite/issues/1327)) ([1f89b0e](https://github.com/vitejs/vite/commit/1f89b0e704d4315246836d2cd7faf3cdcdf89dd9))
* sourcemap path mangled by browser ([#1326](https://github.com/vitejs/vite/issues/1326)) ([1da12ba](https://github.com/vitejs/vite/commit/1da12baf00ab8e7c3366f9c0e088c09cce903934)), closes [#1323](https://github.com/vitejs/vite/issues/1323)
* **dev:** display localetime correctly ([#1310](https://github.com/vitejs/vite/issues/1310)) ([06663a7](https://github.com/vitejs/vite/commit/06663a7e7825bedd61593d299f00110f6ac40916))


### Features

* esbuild.(include|exclude|jsxInject) ([b5b1496](https://github.com/vitejs/vite/commit/b5b14962b53d8dcbae850b9eb6abf2ca5820b3db))
* **wasm:** use `instantiateStreaming` when available ([#1330](https://github.com/vitejs/vite/issues/1330)) ([2286f62](https://github.com/vitejs/vite/commit/2286f629ab6d96fb0b90c9825582962bf8f0f2a5)), closes [#1143](https://github.com/vitejs/vite/issues/1143)
* export normalizePath helper ([#1313](https://github.com/vitejs/vite/issues/1313)) ([37d1a5d](https://github.com/vitejs/vite/commit/37d1a5de019cfd5db397f5c8e0365222950c1dff))



# [2.0.0-beta.3](https://github.com/vitejs/vite/compare/v2.0.0-beta.2...v2.0.0-beta.3) (2021-01-03)


### Bug Fixes

* **build:** fix import-fresh shim ([b57d74c](https://github.com/vitejs/vite/commit/b57d74c2b72498aee251ed7ed45ff046a98d5499)), closes [#1306](https://github.com/vitejs/vite/issues/1306)
* decode incoming URL ([f52db58](https://github.com/vitejs/vite/commit/f52db5898dfb1eecb4b3427a73ffd7ecd2ac15d6)), closes [#1308](https://github.com/vitejs/vite/issues/1308)
* keep `this` defined in `configureServer` hook ([#1304](https://github.com/vitejs/vite/issues/1304)) ([b665b92](https://github.com/vitejs/vite/commit/b665b92323521475a568f8c5204a83c0e80a6b75))
* **resolve:** prioritize module + avoid mutating path when ([6ce6d5c](https://github.com/vitejs/vite/commit/6ce6d5c2908c20b8308725a5f91f5a618aa09d8a)), closes [#1299](https://github.com/vitejs/vite/issues/1299)


### Features

* dedupe option ([7858e62](https://github.com/vitejs/vite/commit/7858e629273269ca2aedf9891d560521a4bd0c8d)), closes [#1302](https://github.com/vitejs/vite/issues/1302)
* export `resolvePackageData` and `resolvePackageEntry` helpers ([#1307](https://github.com/vitejs/vite/issues/1307)) ([38b9613](https://github.com/vitejs/vite/commit/38b9613832d1af569ca5aba4226895f0bd7897a0))
* expose `loadEnv` in public api ([#1300](https://github.com/vitejs/vite/issues/1300)) ([9d0a8e7](https://github.com/vitejs/vite/commit/9d0a8e74d1553c8c9108caeaf0c22cd938a502c7))



# [2.0.0-beta.2](https://github.com/vitejs/vite/compare/v2.0.0-beta.1...v2.0.0-beta.2) (2021-01-02)


### Bug Fixes

* do not attempt to transform html requests ([a7a5c5b](https://github.com/vitejs/vite/commit/a7a5c5bbd9d26e46fb3a175c80bd898cdfce5572))
* fix spa fallback on paths ending with slash ([60fe476](https://github.com/vitejs/vite/commit/60fe476638930702fb94f906afcf6d1dc4dfab7b))
* **resolve:** prioritize browser field ([dfef3de](https://github.com/vitejs/vite/commit/dfef3de9a5875c238d9a795a461e47634db9809f)), closes [#1154](https://github.com/vitejs/vite/issues/1154)
* **resolve:** resolve inline package ([e27fe30](https://github.com/vitejs/vite/commit/e27fe30e7920d22f4ad786e5bfb14415d73cc2cc)), closes [#1291](https://github.com/vitejs/vite/issues/1291)
* dynamic load postcss plugin ([#1292](https://github.com/vitejs/vite/issues/1292)) ([00c7370](https://github.com/vitejs/vite/commit/00c737024a72ab3e2c5c17f74b2bf28c5b0d158f)), closes [#1287](https://github.com/vitejs/vite/issues/1287)
* fix transform result check for empty result ([2adfa8b](https://github.com/vitejs/vite/commit/2adfa8b1bdc01297a030f8cb3066df7f7a753d3c)), closes [#1278](https://github.com/vitejs/vite/issues/1278)


### Code Refactoring

* **hmr:** pass context object to `handleHotUpdate` plugin hook ([b314771](https://github.com/vitejs/vite/commit/b3147710e96a8f88ab81b2e45dbf7e7174ad976c))


### Reverts

* Revert "types: worker types" (#1295) ([806ef96](https://github.com/vitejs/vite/commit/806ef9697069db581eaa2c1721db5d3e08707a7d)), closes [#1295](https://github.com/vitejs/vite/issues/1295)


### BREAKING CHANGES

* **hmr:** `handleHotUpdate` plugin hook now receives a single
`HmrContext` argument instead of multiple args.



# [2.0.0-beta.1](https://github.com/vitejs/vite/compare/v2.0.0-alpha.5...v2.0.0-beta.1) (2021-01-02)


### Bug Fixes

* --open and --filter arguments ([#1259](https://github.com/vitejs/vite/issues/1259)) ([0c0bc4a](https://github.com/vitejs/vite/commit/0c0bc4a33c99da22be96214af872344f930732d4))
* handle hmr errors ([ff2b3ce](https://github.com/vitejs/vite/commit/ff2b3cef01750c3cb33d39dc726317cbd832568b))
* overlay z-index ([6b3278e](https://github.com/vitejs/vite/commit/6b3278eff8702c45bd8dbace35baca337fb89682))
* **css:** respect minify option for chunk css ([6a287a1](https://github.com/vitejs/vite/commit/6a287a176dd4be6e290d3be0490e39b92916a0d0))


### Features

* also call buildEnd on container close ([94a8def](https://github.com/vitejs/vite/commit/94a8def3bcc673c00ff56f9d19b9933c6426c605))
* provide default typing for supported file types ([a9c7eac](https://github.com/vitejs/vite/commit/a9c7eaca1cf8ab0f590bb605da49fd4daa766244))
* support resolveId returning arbitrary value ([b782af4](https://github.com/vitejs/vite/commit/b782af44cc968cc4f18ef0722302991406fa82de))



# [2.0.0-alpha.5](https://github.com/vitejs/vite/compare/v2.0.0-alpha.4...v2.0.0-alpha.5) (2020-12-30)


### Bug Fixes

* **css:** properly prevent css from being tree-shaken ([7f08835](https://github.com/vitejs/vite/commit/7f088352894f3fcc06e6936917de4bb70b5763dc))



# [2.0.0-alpha.4](https://github.com/vitejs/vite/compare/v2.0.0-alpha.3...v2.0.0-alpha.4) (2020-12-30)


### Bug Fixes

* **css:** fix cssCodeSplit: false ([9a02203](https://github.com/vitejs/vite/commit/9a0220304bd6bc655078b7705b95f3cfd1059e36))
* disable cssCodeSplit by default in lib mode ([e64509a](https://github.com/vitejs/vite/commit/e64509a680fdb01ff25393f9c65f34ac87eb799a))
* fix terser worker thread when vite is linked ([a28419b](https://github.com/vitejs/vite/commit/a28419bafc649192cdb6eca3f6014e3b823d1c0a))
* inline assets in lib mode ([c976d10](https://github.com/vitejs/vite/commit/c976d10ac1e40f0c59bcb02c1016ed6f39563ca0))



# [2.0.0-alpha.3](https://github.com/vitejs/vite/compare/v2.0.0-alpha.2...v2.0.0-alpha.3) (2020-12-30)



# [2.0.0-alpha.2](https://github.com/vitejs/vite/compare/v2.0.0-alpha.1...v2.0.0-alpha.2) (2020-12-29)


### Bug Fixes

* **plugin-vue:** avoid throwing on never requested file ([48a24c1](https://github.com/vitejs/vite/commit/48a24c1fa1f64e89ca853635580911859ef5881b))



# [2.0.0-alpha.1](https://github.com/vitejs/vite/compare/v1.0.0-rc.13...v2.0.0-alpha.1) (2020-12-29)

- [x] new universal plugin format
- [x] framework agnostic core
- [x] smaller and faster install
- [x] improved JS API
- [x] improved alias and resolving
- [x] improved page reload performance (strong caching of npm deps)
- [x] error overlay
- [x] better vue perf (single request in most cases)
- [x] multi entry mode
- [x] lib mode
