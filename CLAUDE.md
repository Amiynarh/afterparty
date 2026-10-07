# CLAUDE.md — after-party project memory

You are the technical co-founder on **after-party: Lagos Style Stories**, a Nigerian fashion life-sim / dress-up game. Read the relevant doc sections before starting any phase. If code and docs disagree, stop and ask which is right, then update the other.

## Document hierarchy (when docs disagree, the higher one wins)
1. `CLAUDE.md` — engineering rules and the decided stack.
2. `docs/BRIEF.md` — product vision, MVP scope and what NOT to build. Wins on **scope** for Milestone 1.
3. `docs/ARCHITECTURE.md` — the approved architecture (created in Phase 0, approved by Bronze).
4. `docs/GDD.md` — full game design and long-term vision. Wins on **design detail** where the brief is silent.
5. `docs/ART_SPEC.md` — art direction and the asset contract.
6. `docs/ROADMAP.md` — build order and phase prompts.

## Product in one paragraph
The player arrives in Lagos with ₦50,000 and a dream of becoming the city's top stylist. Outfits *cause things to happen*: every event is a fashion challenge judged by characters (an aunty, a blogger, a rival), and great looks earn Naira, Influence, sprayed money, relationships and story progress. Signature systems: fabric-swappable garments with procedural Nigerian textiles, market haggling, an unreliable-tailor system, a gele-tying minigame, money spray, NaijaGram (in-game social feed) and photo mode.

## Stack (do not change without asking)
- **Vite + React + TypeScript (strict mode)** — app shell, menus, dress-up UI, dialogue.
- **PixiJS** — the character stage, fabric rendering, minigames, money-spray particles. Mount Pixi inside a React component; React owns UI, Pixi owns the canvas.
- **Zustand** — game state, split into slices (player, wardrobe, economy, calendar, relationships, story, social).
- **Zod** — schemas for every `data/*.json` file; content is validated at load time and the game refuses to boot on invalid content, with a clear error.
- **idb-keyval** — save games in IndexedDB (versioned save format with migrations).
- **Howler.js** — audio.
- **Vitest** — unit tests. Scoring, economy, haggling and tailor logic MUST have tests.
- **Capacitor** — later, for iOS/Android wrapping. Keep everything mobile-first from day one.
Pin exact dependency versions in package.json.

## Architecture rules
1. **Content is data.** Items, fabrics, challenges, NPCs, dialogue, locations live in `data/` as JSON validated by Zod. Never hardcode content in components.
2. **Pure logic, separate from rendering.** Scoring, haggling, tailor outcomes, economy and calendar live in `src/systems/` as pure TypeScript functions with no React/Pixi imports, so they are testable.
3. **Seeded randomness only.** All randomness goes through `src/lib/rng.ts` (seeded PRNG). Procedural fabrics are fully described by `{ motifId, paletteId, seed }` so they save, share and regenerate identically.
4. **Garment rendering contract** (see ART_SPEC): every garment = `mask` + `shading` + `lineart` (+ optional `trim`). Fabric fills the mask; shading is applied per skin/fabric with the rules in ART_SPEC; lineart on top. Never bake fabric into garment art.
5. **Layer order is defined once** in `src/render/layers.ts` and nowhere else.
6. **Placeholder art follows the real spec.** Placeholders are generated SVG/PNG at the real canvas size and anchor points so final art drops in without code changes.
7. **Mobile-first.** Design for a 390×844 portrait viewport first; touch targets ≥ 44px; everything works with touch only.
8. **Multiplayer-ready, not multiplayer.** Every content item and saved entity has a stable string ID that never changes once shipped. `PlayerProfile` (identity, progression, wallet) is separate from `CharacterAppearance` (what gets rendered), and a `Look` (saved outfit) is a plain serialisable object that could be posted, shared or judged by others later. Never assume a single global player: pass a player ID through systems. Game actions go through typed action functions so they could later be sent to a server. Do NOT build accounts, backend, chat or payments in Milestone 1.
9. **No secrets in the client.** Any future AI feature (AI stylist, NPC memory) calls a server endpoint, never the Anthropic API directly from the browser.

## Folder layout
```
data/              JSON content (validated)
docs/              GDD, ART_SPEC, ROADMAP
public/assets/     art, audio (final + placeholder)
src/
  app/             routing, screens
  components/      React UI
  render/          Pixi stage, character renderer, fabric engine, layers.ts
  systems/         pure game logic (scoring, economy, haggle, tailor, calendar, story)
  minigames/       gele, haggle, dance, henna (each self-contained)
  state/           Zustand slices + save/load
  content/         Zod schemas + loaders
  lib/             rng, utils
  config/          game.ts (name, constants, tuning numbers)
tests/
```

## Conventions
- Functional React components, hooks, no class components.
- Tuning numbers (prices, timings, score weights) live in `src/config/game.ts`, never as magic numbers.
- Currency is integer Naira. Format with `formatNaira()` (₦12,500).
- UI copy: sentence case, plain verbs, the game's warm and witty voice. NPC dialogue may use Pidgin/Yoruba/Igbo/Hausa from data files only.
- Commit messages: conventional commits (`feat:`, `fix:`, `chore:`).

## Commands (fill in after Phase 0)
- `npm run dev` — start
- `npm run test` — tests
- `npm run validate:content` — validate all data files
- `npm run build` — production build

## How to work
- For any phase: read the ROADMAP phase + referenced GDD sections, propose a short plan, then build.
- Finish each phase by running tests and `validate:content`, and summarise what changed, what's stubbed, and what I should playtest.
- When I change a design decision in conversation, update `docs/GDD.md` in the same change.
- Ask me before adding a dependency not listed above.
