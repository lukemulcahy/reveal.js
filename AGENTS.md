# Repository Guidelines

This repo is a personal fork of reveal.js. I will use it to create personal presentations, mostly related to my work as a DevOps Engineer.

## Project Structure & Module Organization

- Core source lives in `js/` (controllers, components, utils) and `css/` (themes, print styles); edit these rather than `dist/`, which is generated.
- Plugins and optional features reside in `plugin/`; examples and starter decks are under `examples/`, with quick demos in `index.html` and `demo.html`.
- Tests and fixtures are in `test/` (HTML harnesses plus assets). Built bundles output to `dist/` as UMD and ES modules.

## Build, Test, and Development Commands

- Install: `pnpm install` (Node 18+; lockfile is `pnpm-lock.yaml`).
- Dev server with live reload: `pnpm start` (runs `gulp serve`, watching `js/`, `css/`, `plugin/`).
- Build distributables: `pnpm run build` (rollup + Babel + terser; updates `dist/` and CSS bundles).
- Test and lint: `pnpm test` (runs `gulp test`, which executes ESLint then QUnit in headless Chromium).

## Coding Style & Naming Conventions

- JavaScript uses ES modules and tabs for indentation; keep semicolons and trailing commas off exports to match existing files.
- Prefer `const`/`let`, camelCase for variables/functions, PascalCase for classes/components, and uppercase snake case for shared constants.
- Run ESLint via `pnpm test` or `gulp eslint` to match the repo’s relaxed rule set (e.g., optional curly braces).
- Keep public APIs documented in comments near their controllers/components; avoid adding globals outside `utils/`.

## Testing Guidelines

- Add or extend QUnit-based HTML harnesses in `test/` (follow the `test-*.html` naming). Keep fixtures in `test/assets/`.
- For behavior regressions, add assertions to the relevant harness and ensure they pass headlessly with `pnpm test`.
- When changing build output, verify `dist/` updates by running the full build and re-checking slides in the dev server.

## Commit & Pull Request Guidelines

- Commit messages follow the short, imperative style seen in history (e.g., `add pnpm support`, `fix iframe autofocus`); keep them concise.
- PRs should describe the change, affected areas (e.g., controller, plugin, theme), test coverage (`pnpm test` results), and any visual impacts (screenshots or demo steps).
- If a change alters bundles, note whether `dist/` was regenerated; avoid committing `node_modules/` or unrelated formatting churn.

## Security & Configuration Tips

- Do not hand-edit generated files in `dist/`; update source and rebuild.
- Avoid embedding secrets in example decks or tests. Use `.env`-style configs if needed and keep them out of git.
