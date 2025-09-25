## Quick orientation

This repo is Actual (local-first personal finance app). It's a Yarn v4 monorepo with packages under `packages/`.

- Root commands: use the root workspace (always run `yarn` commands from repo root). See `package.json` scripts for common flows.
- Key packages: `loot-core`, `@actual-app/web` (desktop-client), `desktop-electron`. The sync server has been archived to `archive/sync-server-museum` in this fork.

## Architecture (big picture)

- Monorepo: packages in `packages/*`; root `package.json` orchestrates workspaces and scripts (e.g., `yarn start`, `yarn build:browser`, `yarn test`).
- Client: UI runs in `desktop-client` / `@actual-app/web`. This fork is desktop-only and no longer includes an active sync backend.
- Core library: `packages/loot-core` contains shared logic used by both server and clients (builds to browser/node targets). Look at `packages/loot-core/src` for domain models and build scripts.

## Developer workflows & important commands

- Install & bootstrap: use Yarn 4 (`yarn set version berry` is already used); run `yarn` in repo root.
- Type checking: `yarn typecheck` (root) — runs the tsc project and strict checks. See `.cursor/rules/typescript.mdc` for style hints.
- Linting & formatting: `yarn lint` and to auto-fix `yarn lint:fix` (root `package.json`).
- Tests: vitest is used across packages. Run unit tests with `yarn test` (root) or target a workspace: `yarn workspace <name> run test <path>`; always add `--watch=false` when invoking vitest in CI or non-interactive contexts. See `.cursor/rules/unit-tests.mdc`.
- Start dev servers:
  - Full browser dev: `yarn start` (root) — this runs browser frontend and related watchers.
  - (Sync server archived) The server is not run in this fork.
  - Desktop electron dev: `yarn start:desktop` (runs `rebuild-electron` and builds loot-core browser output first).
- Visual regression & e2e:
  - E2E: `yarn e2e` runs playright tests, needs a running server. See `packages/desktop-client/README.md`.
  - VRT (visual regression): `yarn vrt` and `yarn vrt:docker` for the standardized Playwright docker container. When using docker, pass `--e2e-start-url` or set `E2E_START_URL`.

## Project-specific conventions & patterns

- Workspace-first: Always execute `yarn` commands from repo root (see `.cursor/rules/commands.mdc`). Using `yarn workspaces` is common for cross-package scripts.
- Prefer named exports and functional components in TS/React code. TypeScript rules: prefer interfaces over `type`, avoid `any`, avoid enums. See `.cursor/rules/typescript.mdc` for details.
- Minimal mocking in tests: prefer fewer mocks, exercise integration where feasible (see `.cursor/rules/unit-tests.mdc`).
- Build targets: `loot-core` is built for both node and browser — check scripts like `watch:browser` and `watch:node` inside `packages/loot-core`.

## Integration points & external dependencies

- Electron: `desktop-electron` uses `electron-rebuild` and native deps; `yarn rebuild-electron` exists in root scripts.
- The sync backend has been archived to `archive/sync-server-museum` and is not part of the workspace. For historical reference inspect `archive/sync-server-museum/src`.
- Playwright & VRT: tests rely on Playwright images (`mcr.microsoft.com/playwright`) when running VRT in docker for deterministic snapshots.

## Files to consult when making changes

- High-level: `README.md`, `CONTRIBUTING.md`, `.github/PULL_REQUEST_TEMPLATE.md`
- Build & scripts: root `package.json`, `bin/package-browser`, `bin/package-electron`
- Core logic: `packages/loot-core/src`
- Server: `packages/sync-server/` (see `README.md` and `src/`)
- Client/UI: `packages/desktop-client/`, `packages/web/` (look for `vite.config.*`, `tsconfig.*`)
- Test infra: `playwright.config.ts`, `vitest.config.*`

## When editing code, quick checks to run locally

1. From repo root: `yarn` (install)
2. `yarn typecheck`
3. `yarn lint:fix` then `yarn lint`
4. `yarn test --watch=false` (or workspace-specific test) 

## Examples (concrete snippets)

 - Running E2E / tests:

  - This fork doesn't include the sync server. To run Playwright E2E tests against a server, set `E2E_START_URL` to a running instance (remote or separate host) and then run `yarn e2e`.
  - If you only want to run desktop e2e, build or run the desktop client and point tests at the built app via Playwright configuration.

- Run VRT inside docker (deterministic environment):

  - `yarn vrt:docker --e2e-start-url https://localhost:3001`

## Editing PRs & release notes

- The repo uses a release note generator: `yarn generate:release-notes` (see `bin/release-note-generator.ts`) and the PR template reminds you to run it.

---

If anything here is unclear or you'd like more examples (e.g., where to find specific domain models in `loot-core`), tell me what area to expand and I'll iterate.
