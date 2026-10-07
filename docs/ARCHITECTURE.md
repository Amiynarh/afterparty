# after-party — Architecture (Milestone 1)

Version 1.0 · Status: **APPROVED by Bronze, 2026-10-08** (with changes: 1 body shape, more Northern and Muslim fashion, conflicts resolved on merit) · Answers BRIEF §30 items A–M.

Approval changes are folded into the sections below. The record of what was decided is in "Approved decisions" at the end.

Sources read: `CLAUDE.md`, `docs/BRIEF.md`, `docs/GDD.md`, `docs/ART_SPEC.md`, `docs/ROADMAP.md`, `data/fabrics.json`, `data/npcs.json`, `data/challenges.json`.

Type sketches in this document are specifications, not implementation. The Zod schemas written in Phase 1 will mirror them.

---

## 0. Ground rules and conflicts

### 0.1 How this document resolves disagreements
- **CLAUDE.md** decides stack and engineering rules.
- **BRIEF** decides what is in Milestone 1 (M1).
- **GDD** supplies design detail where the BRIEF is silent.
- **ART_SPEC §4** is the clothing-layer contract. Section B.6 below keeps it and adds to it. Nothing is replaced.

### 0.2 BRIEF ↔ GDD conflicts (resolved on merit)

At approval, Bronze asked for each conflict to go to **whichever option is better for the game**, not automatically to the higher document. Each row was re-judged on that basis. Three rows changed from the draft:
- **#2:** one body shape (Bronze's call).
- **#17:** a single NaijaGram post card on the results screen.
- **#18:** static lalle designs come in as a beauty option.

In every other row the original pick held up as the better option. The reason is in the last column.

| # | Topic | BRIEF says | GDD says | Chosen | M1 decision, and why it's the better option |
|---|---|---|---|---|---|
| 1 | Character presentation | "ONE primary player character system". Wardrobe list is womenswear (gele, heels, blouses). | Woman and man. "Men's fashion treated seriously." | **BRIEF** | Woman only in M1. Doing men's fashion properly (agbada, babban riga, senator) means a second full wardrobe; doing it badly breaks GDD's own promise. Better to do one presentation brilliantly and add men in M2 (`presentation` field ready). Men's fabrics and tailor specialties stay in data. |
| 2 | Body shapes | Architecture "should support" body type. | Women: slim, mid, curvy. | **Bronze: 1 shape** | M1 ships **one body shape (`w_mid`)**. The renderer and data still support N shapes (`bodies.json`, `bodyShapeId`). The art rules that keep heads and feet shared across shapes stay, so adding shapes later is cheap. |
| 3 | Character creation extras | Not mentioned. | Tribal marks (pending review), home state of origin, adjustable features. | **BRIEF** | Face presets only. Tribal marks need cultural review first. State of origin has nothing to affect in a one-event slice, so it would be an empty promise. `homeStateId` is reserved. |
| 4 | Scoring categories | Player-facing: Style, Cultural Fit, Colour Harmony, Accessories, Event Appropriateness, Creativity. | Shows those six but scores occasion / theme / coordination / cultural / budget underneath. | **BRIEF** | **The six categories are the real sub-scores.** What the player sees is then exactly what's computed, and judges can react to it honestly. Two parallel vocabularies is where "why did I get this score?" comes from. Gele quality feeds Accessories. Budget becomes a reward bonus (#5). |
| 5 | Budget | The player starts with a "small amount of money". | ₦50,000 start. `ch1_trad_wedding` has `budget: 60000`. | **GDD start + BRIEF** | **The wallet is the budget** (₦50,000). One constraint the player can see beats a hidden second one. "Rich look, small money" boosts the Naira/Influence reward. |
| 6 | Reputation naming | "reputation". | "Influence (✨)". | **GDD** | One stat, **Influence ✨**. It has more character than "reputation" and is already used across the GDD economy. |
| 7 | Premium currency, rent | Not in M1. | Premium post-launch, rent from M2. | **BRIEF** | Neither is built: they add nothing to a 10-minute slice. `CurrencyId` stays open. |
| 8 | Haggle moves | Too expensive · Final price? · Counter · Accept · Walk away · Return · Another fabric. | Greet properly · Compliment · Counter · Walk away · Last price · Buy now. | **Union** | The BRIEF's moves plus GDD's **Greet** (once) and **Compliment** (once). Manners lowering the price is the most Nigerian and funniest part of haggling, and it makes Iya Bisi's `likes` data mean something. |
| 9 | Tailor "late" outcome | Funny, never frustrating. | Late = after the deadline; you wear something from the wardrobe. | **BRIEF** | The outfit **arrives at the last minute**: a dramatic sequence, then you reach the Owambe late (a small penalty and an Aunty Sade line). In a single-event slice, missing the event wastes the whole run, which is frustration, not comedy. "Follow up" on day 2 is kept. |
| 10 | Calendar | Simulated time. | Morning/Afternoon/Evening slots. | **BRIEF** | Day counter only (Day 1 → Day 3). Slots only bite across several events; with one event they just add taps. The slice is ready for slots in M2. |
| 11 | Photo mode timing | After the event. | Before the event. | **BRIEF** | After. The photo then captures the triumph, or the disaster gele, which is what people share. Also reachable from the lookbook. |
| 12 | Gele depth | 3 outcomes. | Shapes (fan, rose, double-layer), unlocks, collapse mid-event. | **BRIEF + GDD collapse** | One shape (fan) × 3 tiers, practice/retry, and the GDD's **comic collapse during the dance** on a disaster tier. The collapse is cheap and is the moment players will send to friends. Shape unlocks need more art and can wait for M2. |
| 13 | Makeup | Lightweight six. | Full layered, saved presets. | **BRIEF** | The BRIEF's six, plus 3 built-in presets. The hard part is looking good on dark skin, and effort should go there, not into more sliders. |
| 14 | Hair | "hairstyle". | Long list plus options. | **BRIEF** | 4 styles × 5 colours. Hair is hidden under gele and hijab for the key moment, so depth here has the lowest payoff. |
| 15 | Wardrobe presentation | "No boring inventory screen." | A room of rails, with a grid toggle. | **GDD (light)** | Clothes-rail drawer with swatch tabs: the GDD's feel without building a walkable room. |
| 16 | Boutiques | Not in M1. | Ready-to-wear shops. | **BRIEF** | No boutique. The fabric → tailor path is the unique fantasy, and a shop would let players skip it. |
| 17 | NaijaGram | Not in M1. | A full social feed. | **Light GDD (changed)** | No feed, but the results screen shows **one NaijaGram post card**: Zara posts your look, with a fake like count and 2–3 comments from data. It's cheap, it's funny, it plants the social future and it pushes the real export/share. |
| 18 | Adire studio, lalle/henna, random events, home, competitions, AI, designer drops | Not in M1. | Described. | **BRIEF, except static lalle (changed)** | None of these systems are built. But **lalle** comes in as a *static beauty option* (2 designs on the hands, no minigame). It's very cheap and supports the Northern/Muslim content Bronze asked for. The lalle minigame stays M2+. |
| 19 | Post-event choice | 2–3 short scenes. | Choices affect relationships. | **Both** | The closing scene has one Dami choice that moves the rivalry meter. It gives the replay a thread to pull. |
| 20 | NPC memory | Silent. | NPCs reference past outfits. | **GDD (light)** | Outfit history already exists, so replays can fire "Gold again?". A huge charm-per-effort ratio. |
| 21 | Voice | No celebrity voices. | Voiced barks. | **BRIEF** | No voice in M1: text barks plus non-verbal SFX. Voicing Pidgin/Yoruba/Hausa lines before cultural review risks recording mistakes. |
| 22 | Money spray | Notes rain. | Tap to collect. | **Both** | Rain plus tap-to-collect, with uncollected notes auto-banked. Tapping turns the reward into play. |
| 23 | Names | "a market", "Owambe". | "Balogun", "Amaka's cousin's Yoruba trad". | **GDD** | Balogun market. An Owambe at Amaka's cousin's traditional wedding. Specific places beat generic ones. |
| 24 | Phase order | §26 order (Owambe before Judging). | ROADMAP: Beauty phase, Judging before Venue. | **ROADMAP + tweaks** | Building scoring before the venue means the venue is polished around real reactions. Both orders keep the game runnable. |

### 0.4 Northern and Muslim fashion and names (added at approval)

Bronze asked for more Northern and Muslim fashion and names. The Lagos Owambe makes this natural: Lagos has a large Yoruba Muslim population, Northern Nigerians live and party in Lagos, and Muslim women attend Owambes in hijab, often with a gele tied over it. **Nothing here is a "Northern mode" or a separate path.** Every piece is a normal item that scores fairly at this Owambe.

| Area | Addition |
|---|---|
| Headwear | **Hijab** (`veil_hijab_wrap`, fabric-swappable). It can be worn alone or **under a gele** ("gele over hijab"); the gele minigame works the same on top of it. When a hijab is worn, hair is fully hidden. |
| Veils | **Mayafi** (`veil_mayafi_draped`): the Hausa women's shawl/veil over head and shoulders, fabric-swappable. Worn instead of a gele. |
| Garments | **Embroidered kaftan** for women (`dress_kaftan_embroidered`), a new **tailor style** and Hauwa Stitches' specialty. Her embroidery overlay finally has a home. Plus its freestyle sibling, and a **modern abaya** (`dress_abaya_modern`, reward). |
| Fabrics | **Kano Indigo** moves from chapter-4-locked into the M1 market (a Lagos market sells it). Add an **ivory shadda** brocade colourway. Fabrics gain `localNames` so the UI can show e.g. *Ankara (Hausa: atamfa)* and *Brocade (shadda)*. Every name is `review: true`. |
| Beauty | **Lalle** as a static hand design (2 designs, henna colour from data). No minigame. |
| Gele requirement | The challenge's gele requirement becomes **"tie it if you wear it"**. Hijab-only and mayafi looks are valid and never penalised. Accessories credits headwear quality: a gele tier, or a neatly styled hijab/mayafi, which earns a fixed "well styled" credit. |
| Scoring | Cultural Fit gives full credit to ceremony-appropriate Northern and Muslim attire at this Owambe (an embroidered kaftan in lace or brocade is formal wear). Modesty-forward looks are naturally loved by Uncle Bayo. **Never** treat Muslim or Northern dress as "off-theme". |
| Names | `data/names.json`: a suggested-name list for the create screen, across Nigeria's cultures, including Hausa, Fulani, Kanuri, Nupe and Yoruba-Muslim names (e.g. Aisha, Zainab, Hadiza, Halima, Maryam, Bilkisu, Rukayya, Hauwa, Fanna, Yagana, Kafayat, Rofiat, Basirat, Aishat), plus Igbo, Yoruba, Edo, Efik and Ijaw names. Every entry is `review: true`. |
| Characters | **Zara** (judge, influencer) becomes Kaduna-born, Lagos-based, and wears hijab with editorial flair: a fashion authority who is visibly Muslim, not a side character. **Hauwa Stitches** gets more lines and her kaftan specialty. One of the 3 quick-start characters wears hijab with gele. Owambe guest barks include Hausa and Muslim-community voices (e.g. *"Masha Allah, see fine!"*, *"Kai!"*), all from data and all reviewed. |
| Review | Add a **Hausa/Fulani and Muslim cultural reviewer** to the pre-playtest review, alongside Yoruba and Igbo reviewers. |

### 0.3 Other inconsistencies I found (not BRIEF vs GDD)

| # | Where | Problem | Proposed fix |
|---|---|---|---|
| A | GDD, ROADMAP, `fabrics.json` lace spotlight | "Owambe" appears to have been find-and-replaced with "after-party" ("Lace is an after-party essential", "Nigerian pop culture (after-party, Nollywood energy…)", "after-party with a ₦10,000 budget"). | **after-party** is the game title. **Owambe** is the in-world event. Fix the lace `spotlight` text and the GDD/ROADMAP wording when approved. |
| B | CLAUDE.md rule 4 vs ART_SPEC §4 | CLAUDE says `mask + shading + lineart (+ optional trim)`. ART_SPEC says optional `fixed` and `back`, with `trim` as a mask *region*. | Compatible: "trim" is a fabric region, and `fixed`/`back` are extra optional files. I propose rewording CLAUDE rule 4 to match B.6. |
| C | CLAUDE rule 3 vs GDD 5.3 | Procedural fabric is `{ motifId, paletteId, seed }` in one, plus `layout` in the other. | Use the superset `{ typeId, motifId, paletteId, layout, seed }`. `typeId` carries texture behaviour (sheen, weave). Update CLAUDE rule 3. |
| D | `challenges.json` `ch1_trad_wedding` | Judges are `[aunty_sade, zara, dami]`. BRIEF requires 4 judges including the Uncle. | Add `uncle_bayo`. Re-key weights to the six categories. Add `venueId`, `spray`, `rewards`. |
| E | `npcs.json` judge `judges` arrays | Mixed vocabulary (`cultural`, `gele`, `event_appropriateness`, `modesty`, `colour_harmony`, `weakest`). | Replace with `focus: { categoryId: weight }` using the six category IDs plus the special keys `gele` and `weakest`. |
| F | `npcs.json` barks | Lines have no IDs, so "never repeat" and cultural review can't track them. | Every line gets a stable `id`. Barks become `lines[]` with conditions (see D.8). |
| G | `fabrics.json` | Holds 12 fabric **types** with price ranges. BRIEF wants 15–25 concrete **fabrics** (name, colour/pattern, price, rarity, tags). | Split into `fabric_types.json` (the existing 12 entries, IDs unchanged) and `fabrics.json` (22 concrete M1 fabrics). See D.4. |
| H | `fabrics.json` prices | Aso-oke at ₦15k–60k per yard means a 5-yard outfit costs ₦75k–300k against a ₦50k wallet. | Keep `pricePerYard` as real-world reference. M1 sells aso-oke only as **gele and ipele pieces**. Market asks are set per listing in data and checked against the type's range. |
| I | Hauwa Stitches | Specialties (kaftan, babban riga, embroidery) don't match any M1 women's style. | Her `embroidery` specialty always adds the embellishment overlay (the same art used for "masterpiece"). That makes her the "slow but beautiful" tailor from BRIEF §10. |
| J | ART_SPEC §5 layer order | No face, makeup or earrings layers. "Gele back" and "back hair" share one layer. | Expanded order in B.6.4. `layers.ts` stays the single source of truth. |
| K | ART_SPEC §4 `_back.png` | A single file, but backs of a gele or ipele must take fabric. | Backs follow the same mask/shading/lineart contract (B.6.2). |
| L | ART_SPEC §4 lace | Asks for a separate alpha map. | Use the PNG's own alpha channel (one RGBA greyscale tile, tinted per colourway). One fewer file, same result. |
| M | CLAUDE folder layout | `minigames/haggle` and `systems/haggle` could hold duplicate logic. | Rule: `systems/haggle.ts` is all of the logic. `minigames/` holds only real-time minigames (gele, dance). The market UI lives in `app/screens/market`. |

---

## A. Recommended technical stack

**Verdict: keep the CLAUDE.md stack unchanged.** It fits the brief well:

- The brief prefers web and asks for desktop + mobile, performance, and maintainability.
- The game is text- and UI-heavy (dialogue, haggling, judging, menus). That favours DOM/React.
- It also needs a GPU canvas for fabric compositing, particles and minigames. That favours Pixi.

Nothing in the brief justifies Phaser (it would pull the UI into canvas and lose accessible DOM text), Unity/Godot (web export size and load times on mid-range Android), or 3D.

| Layer | Choice (from CLAUDE.md) | Why it fits this brief | Notes |
|---|---|---|---|
| App shell / UI | Vite + React + TypeScript (strict) | Fast iteration. DOM text for dialogue, haggling and accessibility. Easy Capacitor wrap later. | Also turn on `noUncheckedIndexedAccess`. Expect React 19. Pin exact versions at scaffold time. |
| Canvas | PixiJS | WebGL/WebGPU 2D with custom shaders, render textures and meshes: exactly what the fabric pipeline, cloth gele and money spray need. | Expect **Pixi v8**. Used **imperatively** (one long-lived `Application`, mounted by a React component through a ref), **not** `@pixi/react`. Reason: React StrictMode double-mounts and re-renders must never recreate the WebGL context or rebuild the character. |
| State | Zustand (slices) | Small, typed, works outside React (Pixi can subscribe). | Slices: `player`, `wardrobe`, `economy`, `calendar`, `relationships`, `story`, `social` (= lookbook in M1), plus **`flow`** (run state machine) and **`settings`**. |
| Content validation | Zod | Content-as-data with a hard boot failure is the right call. | Expect Zod 4. Also checks **referential integrity** (every ID reference resolves) and **asset presence** (every referenced file exists). |
| Saves | idb-keyval (IndexedDB) | Large enough for looks and thumbnails. Async. | See risk T7 on Safari storage eviction. |
| Audio | Howler.js | Handles the iOS unlock, sprites and fades. | The rhythm game takes its clock from the WebAudio context time (risk T8). |
| Tests | Vitest | Pure systems are fully testable. | Scoring, economy, haggle and tailor are required. I add rng, flow, save migrations and content integrity. |
| Native | Capacitor (later) | Same codebase. | No work in M1 beyond mobile-first layout. |
| Routing | **No router library** | The flow is a game state machine, not URLs. | `src/app` renders the screen for `flow.state`. This counts as "routing" in the CLAUDE layout. |

**Approved additions (Bronze, 2026-10-08; none changes the core stack):**

1. **GSAP** (runtime). Timelines and tweens for both React DOM and Pixi objects: the tailor reveal, the walk-in, the spray finale, count-ups and judge card choreography. The brief's polish bar ("smooth animations") makes hand-rolled tweening a false economy. GSAP has been free for commercial use since 2025. 
2. **ESLint + Prettier** (dev). Strong reason: ESLint's `no-restricted-imports` mechanically enforces architecture rule 2 (no React/Pixi imports in `src/systems`) and rule 5 (layer order only in `layers.ts`).
3. **sharp + @resvg/resvg-js** (dev, scripts only). The asset build: SVG → PNG placeholders at real canvas sizes, transparent-trim, channel-packing and half-resolution variants (B.6.5). Never shipped to the client.
4. **Playwright** (dev). Automated screenshot grids for the Phase 2 and 4 "done when" checks (12 skin tones, 3 presets × 4 tones). 

**Deferred to M2:** Spine runtime (`spine-pixi`), which needs a Spine Editor licence. Pick Spine vs DragonBones before final animated art is commissioned.

---

## B. Project architecture

### B.1 Layer diagram

```
            data/*.json  ──(Zod + integrity + asset checks at boot)──►  ContentDB (read-only, typed)
                                                                              │
 ┌────────────────────────────── src/systems (pure TS, no React/Pixi) ───────┴──────────────┐
 │ actions.ts   applyAction(state, action, ctx) → { state, events }   ← single entry point   │
 │ scoring · judging · haggle · tailor · economy · progression · calendar · flow · story     │
 │ outfit (resolve Look → RenderParts) · colour (harmony model) · fabricSpec (hash/normalise)│
 └───────────────▲───────────────────────────────────────────┬───────────────────────────────┘
                 │ dispatch(GameAction)                       │ DomainEvents (e.g. SprayStarted)
 ┌───────────────┴──────────── src/state (Zustand) ───────────▼───────────────────────────────┐
 │ slices keyed by PlayerId · save/load (idb-keyval, versioned, migrations) · autosave         │
 └───────────────▲──────────────────────────────────────────────┬──────────────────────────────┘
                 │ selectors / subscribe                         │
 ┌───────────────┴────────── React (src/app, src/components) ────┴──── Pixi (src/render, src/minigames) ─┐
 │ screens, panels, dialogue, haggle UI, judge cards     │  StageController: one Application,           │
 │ <PixiStage/> mounts the canvas, sends StageCommands   │  scenes, CharacterRenderer, FabricEngine,    │
 │                                                       │  rig, FX, minigames                          │
 └───────────────────────────────────────────────────────┴──────────────────────────────────────────────┘
        services: AssetLoader (manifest, PH/final resolver) · AudioService (Howler) · Rng (seeded streams)
```

### B.2 Key principles in practice

- **One write path.** Every game-changing input becomes a typed `GameAction` (D.12) applied by the pure `applyAction`. Zustand stores the result. React and Pixi never mutate game state directly. Later, the same reducer can run on a server (B.8).
- **Player ID everywhere.** Every action carries `playerId`. Every per-player slice is `Record<PlayerId, …>`. M1 has one local player, but nothing assumes it.
- **Rendering reads only `CharacterAppearance` + `Outfit`.** The renderer's public API is `render(appearance, outfit, options)`. It never imports `PlayerProfile`. The same function renders NPC-worn or other-player looks later.
- **Seeded RNG streams.** `rng.ts` exposes `stream(name, seed)`. Systems receive an `Rng` in `ctx` and never call `Math.random`. Each save has a `rootSeed`. Streams (`market`, `haggle`, `tailor`, `spray`, `judging`) are derived as `hash(rootSeed, playerId, stream, counter)`. Results are reproducible, and reloading a save can't re-roll the tailor. The one exception is entity ID generation, which uses `crypto.randomUUID()`. IDs are not gameplay.
- **Content is data, and so are tuning numbers.** Content lives in `data/`. Tuning numbers (fees, weights, spray curves, XP thresholds) live in `src/config/game.ts`.

### B.3 Component structure (React)

- `app/App.tsx` loads content (or shows an error screen), loads the save, then renders `<Screen>` for `flow.state`.
- `app/screens/*`: one folder per screen in F (`title`, `create`, `room`, `market`, `tailor`, `reveal`, `styling`, `gele`, `event`, `photo`, `results`, `lookbook`, `settings`).
- `components/`: shared UI.
  - Foundations: `AsoOkePanel`, `SwatchTabs`, `WovenButton`, `NairaAmount`, `InfluenceBadge`, `ProgressStrip`.
  - Dialogue: `DialogueBox`, `Bark`, `PortraitCard`, `ChoiceList`.
  - Phone: `Phone`, `MessageThread`, `IncomingCall`.
  - Gameplay: `JudgeCard`, `ScoreBreakdown`, `FabricInspector`, `ItemDrawer`, `Toast`.
- `components/PixiStage.tsx`: the only component that touches Pixi. It mounts the canvas once at app level, then sends `StageCommand`s (`showScene`, `setCharacter`, `playFx`…) and subscribes to stage events (taps on notes, gesture results).

### B.4 Pixi structure

- **`render/stage.ts` (StageController).** Owns the `Application`, resize and DPR policy, and scene switching. It handles WebGL context loss by rebuilding render textures from state.
- **Scenes** (`render/scenes/`): `RoomScene`, `MarketScene`, `TailorScene`, `VenueScene`, `PhotoScene`, `CreateScene`. Each scene is a Container with layered backgrounds, ambient loops and a character slot.
- **`render/character/`**: `CharacterRenderer`, `SkinShader`, `rig.ts` (head/arm cutout rig), `expressions.ts`.
- **`render/fabric/`**: `FabricEngine`, which turns a `FabricRef` into a 512² tile texture (authored or procedural, cached by spec hash). Also `GarmentShader`.
- **`render/layers.ts`**: the canonical layer order (B.6.4).
- **`minigames/gele/`** and **`minigames/dance/`**: self-contained. Each takes `(appearance, outfit, rng, config)` and resolves to a typed result (`GeleResult`, `DanceResult`). Neither reads the store.

### B.5 Run flow engine
`systems/flow.ts` is a pure state machine: states, allowed transitions and guards (for example, "can't leave for the Owambe without an outfit and a gele result"). The app autosaves on every transition. Full flow in E.

### B.6 Clothing layers: ART_SPEC §4 contract, kept and extended

I'm keeping ART_SPEC §4 as the design: **tiled fabric → clipped by mask → shading blend → fixed details → lineart**, with fabric never baked into art. The additions below are improvements that keep the contract intact. Illustrators still deliver separate, simple files.

#### B.6.1 Regions (names the "separate masks per region" rule)
- A garment declares 1–3 **fabric regions**: `body` (required), `trim`, `sleeve`.
- Mask files are `{id}_{body}_mask_{region}.png`. A garment with one region uses `_mask_body`.
- Each region in data declares `acceptsFamilies` (e.g. gele accepts `aso_oke | brocade | george | finish:satin`) and a `fabricTransform` (`rotation`, `scale`, `offset`).
- The transform aligns prints with the garment's grain, so a wrapper reads horizontal and sleeves angle. This fixes the "wallpaper" look of screen-space tiling at zero art cost.

#### B.6.2 Back parts follow the same contract
Fabric-bearing back parts (gele back, ipele drape) are delivered as `_back_mask_{region}`, `_back_shading` and `_back_lineart`. ART_SPEC's single `_back.png` stays valid for non-fabric backs.

#### B.6.3 Head-region assets are anchored, not full-body
- Face parts, makeup, hair, gele and earrings are authored on a **1024 × 1024 head canvas** at the same pixel scale as the body canvas.
- They are registered to the `neck` anchor.
- They are **shared across body shapes**. This needs one ART_SPEC addition: *all body shapes share the same head size and neck point.*
- Without it, every hairstyle, gele tier and face part would multiply by the number of body shapes.
- Shoes are anchored at the ankles and shared, under the matching rule *feet are identical across body shapes*.
- Necklaces sit on the chest, so they stay per-body.

#### B.6.4 Layer order (proposed `layers.ts`, back to front)

```
 0 background
 1 hair_back          (head-anchored)
 2 headwear_back      (gele back)
 3 garment_back       (ipele drape etc.)
 4 body               (skin pipeline)
 4.5 body_art         (lalle on hands; tinted mask, routed into the arm RTs)
 5 head               (skin pipeline: head base, ears, nose)
 6 face_makeup_base   (blush, highlight, eyeshadow: under features)
 7 face_features      (eyes, brows, mouth, lashes, liner, lip colour)
 8 underlayer         (modesty base layer)
 9 bottoms            (wrappers, skirts, trousers)
10 tops               (tops, dresses)
11 outerwear          (ipele, later agbada/kaftan)
12 shoes
13 jewellery_body     (necklaces, bracelets)
14 hair_front         (hidden when a hijab or mayafi is worn)
15 jewellery_head     (earrings)
16 veil               (hijab, mayafi: over hair and earrings, under gele)
17 headwear_front     (gele front)
18 held               (bag, fan; attached to the hand, after the rig)
19 fx                 (sheen sweep, sparkle)
```

An item's `layer` field refers to these IDs by name. No other file defines order.

#### B.6.5 Engine pipeline

1. **Resolve.** `systems/outfit.ts` turns `(appearance, outfit, content)` into an ordered list of `RenderPart { layer, assetKey, anchor, regions: { regionId → FabricRef + transform }, variant }`. This step is pure and tested.
2. **Fabric tiles.** `FabricEngine.get(ref)` returns a 512² seamless texture.
   - **Authored** (aso-oke, lace, denim): load the tile. Lace is a greyscale RGBA tile tinted to the colourway.
   - **Procedural:** draw motif SVGs on a toroidal grid using the layout and seed, apply the palette, then multiply a **weave-detail tile** (plain / heavy / damask / handwoven) so prints read as cloth, not vector art.
   - Tiles are cached by `hash(normalisedSpec)`.
   - Dominant colours for scoring come from the **palette data**, never from pixels, so they're deterministic and cheap.
3. **Garment shader.** One custom shader per garment draws:
   - the fabric sample per region (mask × transformed tile),
   - **soft-light shading** from the greyscale map (#808080 = neutral), with a per-family `shadingStrength` and a shadow tint drawn from the fabric's own deep colour rather than grey. This is the same principle as the skin rule, so dark fabrics like etu still show folds,
   - lace lining (`lining: none | skin | colour`),
   - fixed details,
   - lineart in its delivered colour.

   I use a custom shader instead of Pixi blend modes because Pixi v8's overlay and soft-light blend modes are filter-based and too expensive per layer on mobile.
4. **Composite once, not per frame.** On any outfit or appearance change, each **rig part** is rendered into its own RenderTexture (B.6.6). Per frame the stage draws a handful of sprites and meshes. Animated **sheen** (aso-oke, brocade) is a separate sheen-mask RT with a moving highlight band in a cheap per-frame shader, so the expensive composite never re-runs.
5. **Asset build packing** (`scripts/build-assets`). Illustrator files are channel-packed: R = shading, G/B = region masks, A = lineart alpha. They are also trimmed to their bounding box (offsets stored in the manifest) and exported at 1× and 0.5×. That is about 4× less GPU memory than loading 1024×2048 RGBA files separately, which is necessary for mid-range Android (risk T1).

#### B.6.6 Poses without per-pose garment art: the cutout rig

Photo mode needs poses (BRIEF §18), and the dance needs movement. Authoring every garment per pose would multiply garment art. Instead:

- **Rig parts:** `head_back`, `body`, `arm_L`, `arm_R`, `head_front`, `held`.
- **Arm regions.** Each body shape ships `arm_L` and `arm_R` **region masks**. The compositor routes pixels of every layer into the torso RT or an arm RT, so sleeves, bracelets and an ipele draped on the arm all travel with the arm.
- **Arm deformation.** Arms are Pixi meshes with 2-bone (shoulder, elbow) linear-blend skinning. Angles are limited to keep seams clean.
- **Head.** The head is its own RT and can tilt and nod. Expressions are part swaps.
- **Art constraint (ART_SPEC addition):** the base pose is a **relaxed A-pose**, arms ~15–20° from the torso with a visible gap at the waist. Nothing is hidden behind the arms except a small shoulder overlap.
- **Risk handling:** a timeboxed spike in Phase 2 proves the seams on placeholders *before* any art is commissioned. If the seams are unacceptable, fall back to whole-body poses: transform + head tilt + expression + held prop, with arms fixed. The A-pose rule and arm masks cost almost nothing, so they stay either way and keep the door open for Spine later.

#### B.6.7 Tailor outcomes need no extra art pipeline

| Outcome | Visual |
|---|---|
| Perfect | The ordered garment(s). |
| Masterpiece | Garment + `_fixed_embellished` overlay + sparkle FX. Hauwa's embroidery specialty always adds the overlay. |
| Freestyle | Swaps the style's main garment for its authored `_freestyle` sibling (3 in M1). Whether it **helps or hurts** depends on scoring context: drama vs `dont_outshine_bride`. The same reveal can be a triumph or a roast. |
| Late | No art. Dialogue, phone and timing only. |

#### B.6.8 Skin and makeup
- Skin follows ART_SPEC §3 exactly: base value map tinted by tone base, shadow-mask colour and highlight-mask colour, with hue-shifted shadows and never a grey multiply.
- **Skin finish** (matte / satin / glow) is a shader parameter (highlight spread and sheen), so it needs no art.
- **Makeup shades are tone-adaptive data.** Each shade defines colours per tone band (`deep`, `deep_medium`, `medium`, `light`) and a blend recipe. For example, blush uses a chroma-preserving soft-light, and highlight uses a warm-gold additive tuned per band.
- This is how BRIEF §13's "renders beautifully across dark skin tones" becomes enforceable. Phase 4 adds a test that renders every shade on `skin_01` and `skin_12`.

### B.7 How content is added without rewriting systems
- **New garment:** add an `items.json` entry (ID, layer, regions, tags), drop files named by the convention into `public/assets/…/garments/{id}/`, then run `npm run build:assets && npm run validate:content`. No code changes.
- **New fabric:** add a `fabrics.json` entry. Procedural fabrics need only motif/palette IDs. Authored fabrics need one tile.
- **New judge line, haggle line or scene:** data only. The condition DSL (D.8) covers triggers.
- **New event:** a `challenges.json` entry plus a location. Scoring is generic over the six categories and the registered special rules. A new special rule is the only case that needs code: one pure function registered in `systems/scoring/rules.ts`.
- **Stable-ID lock:** `data/id-lock.json` lists every shipped ID. `validate:content` fails if a locked ID disappears or changes type. Removal means `deprecated: true` or an alias, never deletion.
- **Placeholders:** the asset resolver prefers `final/` over `ph/` at the same path, so final art replaces placeholders with no code change. `npm run report:placeholders` lists anything still PH.

### B.8 How multiplayer and social fit in later (no backend in M1)

| Future feature | What M1 already provides |
|---|---|
| Accounts and profiles | `PlayerProfile` keyed by `PlayerId` (UUID). A future account maps to it 1:1, and cloud save uploads `PlayerState` as-is. |
| Avatars visible to others | `CharacterAppearance` is self-contained and renderable on any client from content IDs alone. |
| Posts, likes, comments, voting | A `Look` is a self-contained, versioned JSON object (embedded appearance + outfit + procedural fabric specs + photo settings). It can be posted as-is. Photos regenerate deterministically from it. |
| Server authority, anti-cheat | Every state change is a typed `GameAction` handled by a pure reducer. A server can run the same `systems/` code. The currency ledger (D.10) makes wallets auditable. |
| Player judges and competitions | `JudgeRef = { kind: 'npc', npcId } | { kind: 'player', playerId }`. `EventResult` already stores per-judge reactions and the scored Look. |
| Friends, rivals, clubs | `Relationship` targets are typed refs (`npc:` / `player:`), so the same meters and flags work for players. |
| Multi-player events | The renderer is instance-based (no global character), and `VenueScene` takes an array of `(appearance, outfit)`. |
| Player-created fabrics, trading | Procedural fabrics are `{ typeId, motifId, paletteId, layout, seed }`. They are tiny, shareable and identical everywhere. |
| AI stylist and NPC memory | Behind a future server endpoint (CLAUDE rule 9). Outfit history already exists as EventResults. |

**Explicitly not built:** auth, network code, an API client, chat, payments or a server.

### B.9 Responsive layout
- **Portrait-first at 390 × 844:** stage on top (~55% of height), a bottom sheet for panels, touch targets ≥ 44 px.
- **Landscape and desktop at ≥ 900 px wide:** the stage goes left and a fixed-width panel (≈ 420 px) goes right. The same components, re-arranged.
- The Pixi canvas fills the stage region, and scenes are authored crop-safe (G.5).
- Input is touch-first. Mouse works the same, and the keyboard is optional (arrow keys and space for dance).

---

## C. Folder structure

This follows the CLAUDE.md layout, with sub-structure added.

```
after-party/
├─ CLAUDE.md  README.md
├─ docs/                    BRIEF, GDD, ART_SPEC, ROADMAP, ARCHITECTURE
├─ data/
│  ├─ id-lock.json          shipped-ID registry (B.7)
│  ├─ fabric_types.json     the 12 existing type entries (IDs unchanged)
│  ├─ fabrics.json          22 concrete M1 fabrics
│  ├─ finishes.json         leather, patent, satin, denim, canvas
│  ├─ motifs.json           motif library (refs to SVGs)
│  ├─ palettes.json         named palettes with colour tags + hex
│  ├─ items.json            garments, shoes, bags, jewellery, headwear
│  ├─ tailor_styles.json    iro & buba, skirt & blouse, mermaid gown
│  ├─ bodies.json           body shapes + anchors + arm-region refs
│  ├─ skins.json            12 tones (base/shadow/highlight + tone band)
│  ├─ faces.json            face presets, expression definitions
│  ├─ names.json            suggested player names across Nigeria's cultures (review: true)
│  ├─ naijagram.json        results-card comment lines (review: true)
│  ├─ hair.json             hairstyles, hair colours
│  ├─ makeup.json           finishes, tone-adaptive shades, 3 presets
│  ├─ poses.json            rig poses (bone angles), photo poses
│  ├─ npcs.json             cast incl. judge, trader and tailor blocks
│  ├─ challenges.json       events (M1: ch1_trad_wedding)
│  ├─ market.json           stalls + listings
│  ├─ locations.json        5 locations + scene layers
│  ├─ progression.json      levels, rewards pools
│  ├─ photo.json            backgrounds, lighting/filter presets, camera presets
│  ├─ starter.json          starting wallet, wardrobe, quick-start characters
│  ├─ audio.json            audio manifest (ids → files, BPM for dance)
│  └─ dialogue/             intro_mummy.json, invite_amaka.json, closing.json
├─ art-src/                 layered PSD/Procreate sources (not shipped; Git LFS)
├─ public/assets/
│  ├─ manifest.json         generated: id → file, trim offsets, packing, PH flag
│  ├─ final/  ph/           identical sub-trees; resolver prefers final/
│  │  ├─ characters/bodies/{bodyId}/
│  │  ├─ characters/heads/{facePresetId}/
│  │  ├─ characters/hair/{hairId}/
│  │  ├─ garments/{itemId}/{bodyId}/          (body-fitted)
│  │  ├─ accessories/{itemId}/                 (anchored, shared)
│  │  ├─ fabrics/tiles/  fabrics/motifs/  fabrics/weave/
│  │  ├─ scenes/{locationId}/
│  │  ├─ npcs/{npcId}/
│  │  ├─ ui/  fx/
│  └─ audio/ music/ sfx/
├─ scripts/                 build-assets, gen-placeholders, validate-content, report-placeholders
├─ src/
│  ├─ app/                  App.tsx, screen switch, screens/{…}
│  ├─ components/           shared React UI (B.3)
│  ├─ render/               stage.ts, layers.ts, scenes/, character/, fabric/, fx/
│  ├─ systems/              actions, flow, scoring/, judging, haggle, tailor, economy,
│  │                        progression, calendar, story, outfit, colour, fabricSpec
│  ├─ minigames/            gele/, dance/
│  ├─ state/                store.ts, slices/, save/ (schema, migrations, slots)
│  ├─ content/              schemas/ (Zod), load.ts, integrity.ts, ContentDB
│  ├─ lib/                  rng.ts, ids.ts, formatNaira.ts, hash.ts
│  └─ config/               game.ts (name, tuning)
└─ tests/                   systems/*.test.ts, content.test.ts, save-migrations.test.ts
```

---

## D. Data models

### D.0 ID conventions
- **Content IDs:** snake_case, unique within their collection, never renamed after shipping. Item IDs follow ART_SPEC §6 (`{category}_{shortname}_{variant}`). References are typed by field (`fabricId`, `itemId`), so collection-scoped IDs are unambiguous.
- **Entity IDs:** created at runtime as `{prefix}_{uuid}`. Prefixes: `plr_`, `app_`, `look_`, `inv_`, `fab_`, `ord_`, `res_`, `txn_`.
- **Versions:**
  - every data file has `version`,
  - every saved entity has `schemaVersion`,
  - the save has `saveVersion` and the `contentVersion` it was written with.

### D.1 Player

```ts
type PlayerId = `plr_${string}`;

interface PlayerProfile {          // identity + progression + wallet (CLAUDE rule 8)
  id: PlayerId; schemaVersion: 1;
  displayName: string;
  createdAt: string;               // ISO
  homeStateId?: string;            // reserved, unused in M1
  activeAppearanceId: AppearanceId;
  wallet: Wallet;                  // D.10
  progression: Progression;        // D.11
}

// Everything else about a player lives beside the profile, not in it:
interface PlayerState {
  profile: PlayerProfile;
  appearances: Record<AppearanceId, CharacterAppearance>;
  inventory: Inventory;                       // D.3
  relationships: Record<RelRef, Relationship>;
  story: { flags: Record<string, boolean | number>; seenSceneIds: string[]; seenLineIds: string[] };
  lookbook: LookId[];  looks: Record<LookId, Look>;
  orders: Record<OrderId, TailorOrder>;
  eventResults: Record<ResultId, EventResult>;
  ledger: LedgerEntry[];                      // bounded
  run: RunState | null;                       // E
}

type RelRef = `npc:${string}` | `player:${PlayerId}`;
interface Relationship { target: RelRef; friendship: number; rivalry: number; flags: string[] } // −100..100
```

### D.2 Character (appearance, rendered)

```ts
type AppearanceId = `app_${string}`;
interface CharacterAppearance {
  id: AppearanceId; schemaVersion: 1;
  presentation: 'woman';                         // enum grows in M2
  bodyShapeId: 'w_mid' | string;                 // M1 ships w_mid only; validated against bodies.json
  skinToneId: string;                            // skin_01..skin_12
  facePresetId: string;                          // face_01..face_04
  hair: { styleId: string; colourId: string };
  makeup: {
    finishId: 'matte' | 'satin' | 'glow';
    blush:     { shadeId: string; intensity: number } | null;   // 0..1
    eyeshadow: { shadeId: string; intensity: number } | null;
    liner: boolean;
    lashesId: 'lashes_natural' | 'lashes_dramatic' | null;
    lalle: { designId: 'lalle_floral' | 'lalle_geometric'; colourId: string } | null;
    lips:      { shadeId: string } | null;
    highlight: { shadeId: string; intensity: number } | null;
  };
  defaultExpressionId: string;
}
```

Content backing it:

- **`bodies.json`:** `{ id, presentation, canvas: { w: 1024, h: 2048, baselineY: 1940 }, anchors: { head_top, neck, shoulder_l, shoulder_r, elbow_l, elbow_r, waist, hips, wrist_l, wrist_r, hand_l, hand_r, ankle_l, ankle_r }, armRegions: { l, r }, assets }`
- **`skins.json`:** `{ id, name, base, shadow, highlight, band: 'deep' | 'deep_medium' | 'medium' | 'light' }`
- **`faces.json`:** `{ presets: [{ id, name, assets }], expressions: [{ id, eyes: 'open' | 'closed' | 'wide', brows: 'neutral' | 'raised' | 'furrowed', mouth: 'neutral' | 'smile' | 'laugh' | 'grimace' }] }`. M1 expressions: `neutral`, `smile`, `laugh`, `shock`, `unimpressed`, `oh_no`.
- **`makeup.json` shades:** `{ id, product, name, colours: { deep, deep_medium, medium, light }, blend }`.

### D.3 Clothing

```ts
interface Item {                                   // items.json
  id: string;                                      // e.g. 'top_buba_classic'
  name: string;
  category: 'top' | 'bottom' | 'dress' | 'wrapper' | 'outerwear' | 'shoes' | 'bag'
          | 'jewellery' | 'headwear' | 'veil' | 'fan' | 'base';
  slot: SlotId;                                     // where it goes in an Outfit
  layer: LayerId;                                   // name from layers.ts
  fit: 'body' | 'anchored';                         // per-body art vs shared anchored art
  anchor?: 'neck' | 'ankles' | 'wrist_l' | 'wrist_r' | 'hand_r';
  bodies?: string[];                                // body-fitted items: supported shapes
  regions: Array<{ id: 'body' | 'trim' | 'sleeve'; acceptsFamilies: string[];
                   defaultFabric: FabricRef; fabricTransform?: { rotation: number; scale: number; offsetX: number; offsetY: number };
                   lining?: 'none' | 'skin' | string }>;     // [] for fixed-art items
  colours?: ColourTag[];                            // for items with fixed colour (jewellery)
  rarity: 'common' | 'uncommon' | 'rare' | 'signature';
  price: number;                                    // integer ₦ (resale/reference)
  formality: 1|2|3|4|5;  modesty: 1|2|3|4|5;  drama: 1|2|3|4|5;
  occasions: OccasionId[];                          // event suitability
  cultures: CultureId[];                            // context, never a penalty source (see D.9)
  styleTags: string[];                              // 'aso_ebi_classic', 'modern', 'statement'…
  scoreModifiers?: Array<{ category: CategoryId; delta: number; when?: Condition }>;
  variants?: Record<string, { assetSuffix: string }>;     // gele tiers, embellished
  source: 'starter' | 'tailor' | 'reward' | 'borrow';
  spotlight?: string; review?: boolean;
}
type SlotId = 'base' | 'top' | 'bottom' | 'dress' | 'outer' | 'shoes' | 'bag' | 'neck'
            | 'wrist' | 'ears' | 'veil' | 'headwear' | 'held';
// veil + headwear: a hijab allows a gele on top; a mayafi blocks 'headwear' (data: blocksSlots)
```

A dress occupies `dress` and blocks `top`/`bottom`. The blocking rules live in `items.json` as `blocksSlots`.

```ts
interface Outfit { pieces: Partial<Record<SlotId, OutfitPiece>> }
interface OutfitPiece {
  itemId: string;
  fabrics?: Partial<Record<'body' | 'trim' | 'sleeve', FabricRef>>;
  variant?: string;                     // 'perfect' | 'good' | 'disaster' | 'embellished' | 'freestyle'
  instanceId?: InvId;                   // link to owned instance (local only; not needed to render)
}

interface Inventory {
  garments: Record<InvId, { id: InvId; itemId: string; fabrics: OutfitPiece['fabrics'];
                            variant?: string; quality?: TailorOutcome; source: Item['source'];
                            acquiredDay: number }>;
  fabrics:  Record<FabId, { id: FabId; ref: FabricRef; use: 'outfit_length' | 'gele_piece' | 'ipele_piece';
                            pricePaid: number; consumedByOrderId?: OrderId }>;
  borrowed?: { itemId: string; fromNpcId: string; returnAfterResult: true };
}
```

**Look** (saved outfit; self-contained, postable):

```ts
type LookId = `look_${string}`;
interface Look {
  id: LookId; schemaVersion: 1; contentVersion: number;
  ownerPlayerId: PlayerId;
  name: string; createdAt: string;
  appearance: CharacterAppearance;           // embedded snapshot, not a reference
  outfit: Outfit;                            // FabricRefs fully specified
  geleTier?: 'perfect' | 'good' | 'disaster';
  photo?: PhotoSettings;                     // { poseId, expressionId, cameraId, zoom, backgroundId, lightingId, filterId }
  context?: { challengeId: string; resultId: ResultId; total: number };
  thumbnail?: string;                        // small WebP data URI, local only
}
```

### D.4 Fabric

```ts
interface FabricType {         // fabric_types.json: today's fabrics.json entries, unchanged IDs
  id: string; name: string; family: string; cultures: CultureId[];
  texture: { sheen: number; weave: string; printScale: number; procedural: boolean;
             proceduralStyle?: string; transparency?: boolean };
  pricePerYard: [number, number]; formality: [number, number];
  spotlight: string; unlock?: string; review: boolean;
}

interface Fabric {             // fabrics.json: the concrete 15–25 the player sees
  id: string; typeId: string; name: string;
  authenticity: 'traditional_reference' | 'inspired';   // generated patterns are always 'inspired'
  source: { kind: 'tile'; tileId: string; colourway?: string }
        | { kind: 'procedural'; spec: ProceduralFabricSpec };
  paletteId: string;           // dominant colours for scoring come from here
  rarity: Item['rarity'];
  styleTags: string[];
  baseAsk: number;             // listing ask (integer ₦), validated against type range × yards
  sellAs: Array<'outfit_length' | 'gele_piece' | 'ipele_piece'>;
  review: boolean;
}

interface ProceduralFabricSpec { typeId: string; motifId: string; paletteId: string;
                                 layout: 'grid' | 'half_drop' | 'scatter' | 'stripe' | 'mirror' | 'radial'; seed: number; scale?: number }

type FabricRef = { kind: 'fabric'; fabricId: string }
               | { kind: 'procedural'; spec: ProceduralFabricSpec }   // player-made later
               | { kind: 'finish'; finishId: string; colour?: string };
```

**The 22 M1 fabrics:**

| Type | Count | Fabrics |
|---|---|---|
| Ankara (procedural) | 6 | sunburst, cowrie, fan, kola circles, birds, diamond |
| Adire eleko (procedural, "inspired") | 2 | comb lines, leaf spiral |
| Adire oniko (procedural noise) | 1 | ripple |
| Aso-oke (authored; gele/ipele pieces) | 3 | sanyan, alaari, etu |
| Lace (authored, tinted) | 3 | cord lace wine, beaded champagne, guipure emerald |
| Brocade (procedural damask) | 2 | gold, royal |
| George (procedural) | 2 | madras wine, embroidered gold |
| Akwete (procedural, "inspired") | 1 | — |
| Kano Indigo (authored tile + sheen; beaten-cloth glaze) | 1 | classic deep indigo (the `unlock: chapter_4` is removed) |
| Brocade, ivory shadda (procedural damask) | 1 | ivory |

- Excluded from the M1 market: `atiku` (men's fabric; M2).
- Fabrics and fabric types gain `localNames: { ha?, yo?, ig?, pcm? }`, e.g. Ankara → *atamfa* (ha), brocade → *shadda*. Shown in the inspector as "also called…". All `review: true`.
- **Palettes** (`palettes.json`): `{ id, name, colours: [{ hex, tag: ColourTag, weight }] }`. `ColourTag` is a small vocabulary (`gold`, `coral`, `emerald`, `indigo`, `wine`, `champagne`, `ivory`, `black`…) that judge lines can name.
- **Finishes:** `{ id, name, family: 'finish', tintable: boolean, tileId?: string, sheen: number }`.

### D.5 Tailor

```ts
// npcs.json → role: 'tailor' (the existing block, extended)
interface TailorProfile {
  skill: number; reliability: number; speed: number; priceMultiplier: number; creativity: number;
  specialties: string[];               // styleIds or tags; matching → quality bonus
  alwaysEmbellish?: boolean;           // Hauwa (embroidery)
  lines: Line[];                       // quote, promise, progress_msg, late, freestyle, reveal_*, at_shop_late
}

interface TailorStyle {                // tailor_styles.json
  id: 'style_iro_buba' | 'style_skirt_blouse' | 'style_gown_mermaid' | 'style_kaftan_embroidered' | string;
  name: string;
  produces: Array<{ itemId: string; regionsFrom: Record<string, 'main' | 'trim'> }>; // which bought fabric fills which region
  requires: { main: 'outfit_length'; trim?: 'outfit_length' | 'ipele_piece' };
  baseFee: number;                     // × priceMultiplier = quote
  freestyleItemId: string;             // the sibling garment
  tags: string[];
}

type TailorOutcome = 'perfect' | 'late' | 'freestyle' | 'masterpiece';
interface TailorOrder {
  id: OrderId; playerId: PlayerId; tailorId: string; styleId: string;
  fabricIds: { main: FabId; trim?: FabId };
  placedDay: number; promisedDay: number; price: number;
  rngSeed: number;                     // outcome rolled at order time → no reload re-roll
  outcome: TailorOutcome;              // hidden from UI until reveal
  followedUp: boolean;                 // day-2 visit lowers lateness
  messages: Array<{ day: number; lineId: string }>;
  status: 'sewing' | 'delivered';
  resultInvIds: InvId[];
}
```

### D.6 Event

```ts
interface Challenge {                    // challenges.json (ch1_trad_wedding updated for M1)
  id: string; chapter: number; title: string; venueId: string;
  occasion: OccasionId; culture?: CultureId; theme: string;
  budget?: number;                       // unused in M1 (see 0.2 #5)
  deadlineDays: number;                  // M1: 2 → event on day 3 evening
  requiresMinigame?: 'gele';
  targets: { formality: [number, number]; drama: [number, number]; modesty: [number, number] };
  special: string[];                     // 'dont_outshine_bride' (registered rule ids)
  judges: JudgeRef[];                    // M1: aunty_sade, zara, uncle_bayo, dami
  weights: Record<CategoryId, number>;   // six keys, sum = 1
  themeKeywords: string[];               // styleTags that count as on-theme
  spray: { baseNotes: number; maxNotes: number; denominations: number[] };
  rewards: { xp: [number, number]; influence: [number, number]; itemPoolId: string };
  dance: { enabled: boolean; trackId: string; durationSec: number };
}

type JudgeRef = { kind: 'npc'; npcId: string } | { kind: 'player'; playerId: PlayerId };

interface EventResult {
  id: ResultId; playerId: PlayerId; challengeId: string; lookId: LookId; day: number;
  scores: { categories: Record<CategoryId, number>; gele: number; dance?: number; total: number }; // 0..100
  evidence: Evidence[];                  // why: { category, kind, itemId?, colourTag?, delta }
  flags: string[];                       // 'outshine_bride', 'late_arrival', 'gele_collapse'
  reactions: Array<{ judge: JudgeRef; lineIds: string[] }>;
  spray: { notesSpawned: number; collected: number; naira: number };
  rewards: { naira: number; influence: number; xp: number; itemIds: string[] };
}

interface Location { id: string; name: string; kind: 'room' | 'market' | 'tailor' | 'venue' | 'photo';
                     layers: string[]; ambient: string[]; musicId: string }
```

### D.7 Judge

```ts
// npcs.json → role: 'judge_*' gets a judge block
type CategoryId = 'style' | 'cultural_fit' | 'colour_harmony' | 'accessories'
                | 'event_appropriateness' | 'creativity';
interface JudgeProfile {
  focus: Partial<Record<CategoryId | 'gele' | 'weakest', number>>;  // which sub-scores they react to
  tastes: { likesTags: string[]; dislikesTags: string[]; likesColours: ColourTag[] };
  maxLinesPerEvent: number;              // 2
  lines: Line[];
  portraitSet: string;                   // approve, neutral, disapprove, shocked
}
```

M1 focus values (from GDD):

| Judge | Focus |
|---|---|
| Aunty Sade | cultural_fit .4, accessories .3, gele .3 |
| Uncle Bayo | event_appropriateness .7, modesty-driven evidence .3 |
| Zara (Kaduna-born, Lagos-based hijabi influencer) | style .5, creativity .5 |
| Dami | colour_harmony .5, weakest .5 |

### D.8 Lines and conditions (shared by judges, traders, tailors, scenes)

```ts
interface Line {
  id: string;                            // stable, e.g. 'aunty_sade.gele_disaster.01'
  text: string;                          // tokens: {item:headwear}, {fabric:top}, {colour:dominant}, {naira:price}
  when: Condition;                       // all must hold
  priority: number;                      // most specific wins
  expression?: string;                   // portrait to show
  lang?: 'en' | 'pcm' | 'yo' | 'ig' | 'ha';
  review: boolean;
}
type Condition = {
  band?: { category: CategoryId | 'total' | 'gele'; is: 'low' | 'mid' | 'high' };
  flag?: string; itemTag?: string; itemCategory?: string; colourTag?: ColourTag;
  geleTier?: 'perfect' | 'good' | 'disaster'; tailorOutcome?: TailorOutcome;
  haggleEvent?: string; relationship?: { npcId: string; friendshipGte?: number };
  storyFlag?: string; not?: Condition;
};
```

**Selection:** highest priority among matching lines whose ID isn't in `seenLineIds` for this session. That gives GDD's "never repeat" rule.

### D.9 Scoring

The scoring model sits between "event" and "judge". In `systems/scoring/`, sub-scores (0–100) are computed from the Look, the challenge and the content. Every point change emits an `Evidence` entry, which is what lets reactions name what the player actually wore.

| Category | Computed from |
|---|---|
| Event Appropriateness | Formality and modesty of the main pieces vs `targets`. Occasion-tag match. Special rules (`dont_outshine_bride`: drama above the range → penalty + flag). `late_arrival` flag. |
| Cultural Fit | Ceremony-appropriate pieces for the context (iro & buba, skirt & blouse, gele, aso-oke, lace, coral). Ceremony-appropriate Northern and Muslim attire (embroidered kaftan, abaya in formal fabric, hijab, gele-over-hijab, mayafi, lalle) earns **full** credit at this Owambe, because Muslim and Northern guests are part of Lagos Owambe life. Other Nigerian traditional wear earns **partial positive** credit ("representing your roots"), **never** a penalty. Only clearly casual or off-occasion pieces score low. This is how BRIEF §7's "avoid simplistic stereotypes" is kept. |
| Colour Harmony | Palette dominant colours of every region and item colours, in OKLCH. Rewards analogous, complementary, monochrome and known pairings (gold+coral, wine+gold, indigo+white). Penalises clashing saturated hues and too many accents. |
| Accessories | Slot coverage (shoes, bag, neck/ears, headwear **or veil**; earrings hidden by a hijab still count if worn). Formality match. Headwear/outfit fabric relationship (match or deliberate contrast). **Gele tier** (perfect +, disaster −) if a gele is worn; a hijab or mayafi alone earns a fixed "well styled" credit, so no route is worse. |
| Style | Silhouette coherence (style tags agree), drama inside the target, garment quality (tailor skill, masterpiece), fabric rarity. |
| Creativity | A trim region in a different fabric, non-default combinations that still harmonise, freestyle outcome (context-dependent), not repeating your previous Look (history). |

- `total = Σ weights[c] × score[c]`.
- Special-rule modifiers are applied after the weighted sum, inside rule functions.
- Bands: low < 45 ≤ mid < 75 ≤ high (tuning).

### D.10 Currency

```ts
type CurrencyId = 'naira' | 'influence';            // open enum: 'premium' later, cosmetic only
interface Wallet { naira: number; influence: number } // integers ≥ 0
interface LedgerEntry { id: TxnId; playerId: PlayerId; currency: CurrencyId; delta: number;
                        reason: 'start' | 'fabric_purchase' | 'tailor_fee' | 'spray' | 'reward' | 'borrow' | 'safety_net';
                        refId?: string; day: number; at: string }
```

- Naira is integer, formatted with `formatNaira()`.
- **No real-world value.** Naira cannot be bought.
- `economy.ts` is the only code that changes a wallet. It always writes a ledger entry and rejects anything that would go negative.

### D.11 Progression

```ts
interface Progression { xp: number; levelId: string; unlockedItemIds: string[]; runsCompleted: number; bestTotal: number }
// progression.json
interface Level { id: 'new_stylist' | 'known_around_town' | 'rising_fashion_name'; level: 1|2|3;
                  title: string; xpRequired: number; unlocks: { itemIds: string[]; tailorIds?: string[] } }
interface RewardPool { id: string; entries: Array<{ itemId: string; weight: number; minTotal?: number }> }
```

- Indicative tuning: L2 at 100 XP, L3 at 300 XP. A good first run earns about 120 XP, so a player reaches L2 on their first strong run and L3 after 3–4 runs.
- Each completed run grants one item from the pool that the player doesn't own yet.

### D.12 Actions (the typed write path)

```ts
type GameAction =
  | { type: 'profile/create'; playerId; displayName; appearance }
  | { type: 'appearance/update'; playerId; appearanceId; patch }
  | { type: 'flow/go'; playerId; to: RunStateName }
  | { type: 'market/haggle'; playerId; listingId; move: HaggleMove; offer?: number }
  | { type: 'market/buy'; playerId; listingId; price: number }
  | { type: 'tailor/order'; playerId; tailorId; styleId; fabricIds }
  | { type: 'tailor/followUp'; playerId; orderId }
  | { type: 'calendar/sleep'; playerId }
  | { type: 'outfit/equip' | 'outfit/unequip'; playerId; slot; piece? }
  | { type: 'borrow/choose'; playerId; itemId }
  | { type: 'gele/complete'; playerId; result: GeleResult }
  | { type: 'event/score'; playerId }
  | { type: 'spray/collect'; playerId; noteIds: string[] }
  | { type: 'dance/complete'; playerId; result: DanceResult }
  | { type: 'look/save'; playerId; name; photo? }
  | { type: 'story/choose'; playerId; sceneId; choiceId }
  | { type: 'run/finish' | 'run/restart'; playerId };
```

### D.13 Save format

```ts
interface SaveGame {
  saveVersion: number; contentVersion: number; slotId: 1 | 2 | 3; savedAt: string;
  rootSeed: number; activePlayerId: PlayerId;
  world: { day: number };
  players: Record<PlayerId, PlayerState>;
  rngCounters: Record<string, number>;
}
```

`state/save/migrations.ts` holds an ordered list of `(from, to, migrate)` steps, each with a test fixture.

---

## E. Game state flow

### E.1 Persistent vs run state
- **Persistent:** profile, appearance, inventory, relationships, lookbook, results.
- **Run** (one Owambe attempt): current step, the market haggle state, the active order, the current outfit, gele/dance results.
- Replays start a new run and keep everything persistent.

### E.2 Run state machine

```
BOOT ─► CONTENT_CHECK ──fail──► CONTENT_ERROR (readable list of problems)
            │ ok
            ▼
          TITLE ─► SLOT_SELECT ─► (new) INTRO_MUMMY ─► CREATE_CHARACTER ─► INVITE_AMAKA (brief + borrow box)
            │                         (continue) ─► resume at saved state
            ▼
DAY 1   ROOM_HUB ◄────────────────────────────────────────────────┐
          ├─► MARKET ─► (browse ⇄ inspect ⇄ haggle ⇄ walk away/return) ─► ROOM_HUB
          ├─► TAILOR ─► (choose tailor → style → assign fabrics → quote → confirm) ─► ROOM_HUB
          └─► SLEEP ─► phone messages (tailor progress lines)              │
DAY 2   ROOM_HUB (optional: follow up at TAILOR · gele PRACTICE · MARKET) ─┤
          └─► SLEEP                                                         │
DAY 3   TAILOR_DELIVERY (reveal; late → arrives "just now" sequence) ──────┘
          ▼
        STYLING (outfit · hair · shoes · bag · jewellery · makeup)  ⇄  GELE_MINIGAME (retry allowed)
          │ guard: outfit valid ∧ (no gele worn ∨ gele result exists)
          ▼
        TRAVEL (keke vignette) ─► EVENT_ARRIVAL (walk-in reveal) ─► JUDGING (4 judges)
          ─► MONEY_SPRAY ─► DANCE (optional; skip allowed) ─► SPRAY_FINALE ─► PHOTO_MODE ─► SAVE_LOOK
          ─► RESULTS (Naira, Influence, XP, level-up, new item, replay suggestion)
          ─► CLOSING_SCENE (Mummy text + one Dami choice) ─► ROOM_HUB (new run) or TITLE
```

### E.3 Rules
- **Never a dead end.**
  - With no tailored outfit, the player can still style from the starter wardrobe (low score, funny lines).
  - Before each run, `economy.ts` checks that the player can afford at least the cheapest fabric plus the cheapest tailor. If not, a **safety-net** gift arrives from Amaka or Mummy, recorded in the ledger.
- **Simulated time:** `SLEEP` is two taps (confirm → message montage). No real-time waits.
- **Skips:** after the first run, story scenes, the travel vignette and the walk-in are skippable, so a replay is ≈ 5 minutes.
- **Autosave** on every state transition. Continue resumes there. Mid-minigame states resume at the start of that minigame.
- **The order rule** (BRIEF §1: style → gele → makeup/accessories) is the *suggested* path, highlighted in the styling screen, but tabs are free. The gele must be tied after choosing the gele fabric, and changing the gele fabric invalidates the result ("you'll need to re-tie it").

### E.4 Pacing target (first run)

| Step | Target time |
|---|---|
| Intro + create | 1:00 |
| Market | 2:00 |
| Tailor | 1:00 |
| Days / messages / reveal | 0:45 |
| Styling | 1:45 |
| Gele | 1:00 |
| Event (arrival, judging, spray, dance) | 2:30 |
| Photo | 0:45 |
| Results + closing | 0:30 |
| **Total** | **≈ 11:15 for a thorough player** |

That is over the 10-minute target, so every step needs a fast path (quick-start characters, "Buy at asking price", style presets). Phase 12 includes a local session-timing log for playtests.

---

## F. MVP screen and page flow

| Screen | Purpose | Portrait layout (390×844) | Key interactions |
|---|---|---|---|
| Content error | Refuses to boot on bad data | Scrollable list: file, path, message | Copy errors |
| Title | Brand moment | Key art (character in gele at the venue), logo, New / Continue | 2 buttons |
| Slot select | 3 save slots | Cards with Look thumbnail, level, day | Pick / delete (custom in-app confirm, no browser dialogs) |
| Story scene | 3 short scenes | Portrait + speech box over a dimmed scene; phone UI for Mummy | Tap to advance, choices |
| Create character | Create/select | Stage top. Tabs: Quick start (3 presets, one in hijab + gele) · Name (free text + suggestions from `names.json` across Nigeria's cultures) · Skin (12 swatches) · Face (4) · Hair (4×5). Body tab hidden while only one shape exists | Instant re-render |
| Room hub | Home base (Yaba studio) | Illustrated room. Hotspots: mirror (styling), phone, door (map), bed (sleep), invite card. Day indicator | Tap hotspots |
| Phone | Messages, calls, invite | Phone frame overlay | Read threads, which give hints |
| Map / travel | Pick destination | Three illustrated cards (Balogun, Tailors' row, Owambe when ready) | Tap → transition |
| Market | Browse fabrics | Iya Bisi's stall with 3 shelves of bolts (rendered with real fabrics). Wallet visible | Tap bolt → inspect |
| Fabric inspect | Look closely | Full-width draped swatch, pinch/drag zoom, sheen catch, name, type, spotlight note, "inspired by" label, asking price | Compare (pin up to 3), Haggle, Back |
| Haggle | The negotiation | Iya Bisi portrait large, price tag, mood hint (her face, not a bar), move buttons, counter-offer stepper | Moves (0.2 #8); a deal slams a stamp |
| Tailors' row | Choose a tailor | One location, three shopfronts, each tailor's card (price, promise, a personality line) | Choose → style → assign fabrics → quote → confirm |
| Delivery reveal | Anticipation payoff | Nylon tailor bag centre stage, shake, open, garment drops onto character | Tap to open |
| Styling | Dress-up | Stage top 55%. Bottom sheet: swatch tabs (Outfit · Fabric · Shoes · Bag · Jewellery · Gele · Hair · Makeup). Item rail. Undo. "Go to the Owambe" | Equip, swap fabric per region, preset makeup, tie gele |
| Gele minigame | Signature | Character head close-up in the mirror frame, cloth mesh, gesture prompt icons, step counter | Gestures per step; result tier; retry/practice |
| Event: arrival | The reveal | Camera dolly through the venue, character walk-in silhouette → full reveal, flashbulbs | Tap to skip (replays) |
| Event: judging | Reactions | Judge portrait cards slide in one by one with lines. A short breakdown strip (6 categories as words + small woven bars; never stars) | Tap to advance |
| Event: money spray | Reward | Notes rain around the character, counter at top | Tap notes to collect |
| Event: dance | 20–30 s rhythm | Character centre stage, prompts on a beat ring, crowd reacts | Tap / hold / swipe on beat; Skip |
| Photo mode | Shareable image | Full-screen stage. Bottom toolbar: Pose · Expression · Camera · Zoom · Background · Light/Filter. Shutter | Pinch zoom, shutter, Save Look, Share/Export |
| Results | Rewards + replay hook | Count-ups (₦, ✨, XP), level-up banner, new-item card, **NaijaGram post card** (Zara posts your look: likes + 2–3 data-driven comments), "Next time try…" suggestion | Continue |
| Lookbook | Saved looks | 2-column grid of thumbnails | Open → re-shoot in photo mode, export |
| Settings | Comfort | Volume, text size, reduced motion, high contrast, credits, reset | — |

Desktop uses the same screens with the panel on the right (B.9). There is never a separate "inventory" screen: items appear only inside the styling context.

---

## G. Art asset requirements (exact Milestone 1 list)

**Assumptions** (approved at sign-off; change these and the counts change):

- **1 body shape (`w_mid`)**
- 4 face presets, chosen to span Nigeria's diversity of features
- 4 hairstyles
- one gele shape (fan) in 3 tiers
- 17 body-fitted garments + 2 body-fitted veils (hijab, mayafi)
- head and feet assets on shared canvases (B.6.3), so a second body shape later adds only body-fitted files
- the cutout arm rig (B.6.6)

"Files" means illustrator deliverables before channel-packing. Every visual asset also gets a generated **placeholder** at the same size, anchors and file name, tagged "PH". Audio placeholders are CC0 or original.

### G.1 Character base — 191 files

| Asset | Variants | Files each | Files |
|---|---|---|---|
| Body (neck-down; ART_SPEC §3: `base`, `lineart`, `shadow_mask`, `highlight_mask`) | 1 body | 4 | 4 |
| Arm region masks (`arm_l`, `arm_r`) | 1 body | 2 | 2 |
| Underlayer `base_slip_simple` (mask, shading, lineart) | 1 body | 3 | 3 |
| Lalle hand designs (`lalle_floral`, `lalle_geometric`; tinted mask on both hands) | 2 | 1 | 2 |
| Head per face preset: head `base`, `lineart`, `shadow_mask`, `highlight_mask` | 4 presets | 4 | 16 |
| Brows (neutral, raised, furrowed; single tintable file) | 4 × 3 | 1 | 12 |
| Eyes (open, closed, wide) × (`base`, `line`) | 4 × 3 | 2 | 24 |
| Mouth (neutral, smile, laugh, grimace) × (`base`, `line`) | 4 × 4 | 2 | 32 |
| Makeup masks: eyeshadow ×3 states, liner ×3, lashes 2 styles ×3 states, lip colour ×4 states, blush ×1, highlight ×1 | 4 presets | 18 | 72 |
| Hair (knotless braids, high afro puff, sleek bob, Fulani braids) × (`back` base+line, `front` base+line, `undergele` base+line) | 4 | 6 | 24 |
| **Subtotal** | | | **191** |

Hair is fully hidden under a hijab or mayafi, so neither needs an extra hair variant.

Data-only (no art):
- 12 skin tones
- 5 hair colours (1B, dark brown, burgundy, honey, copper)
- 3 lalle colours (classic red-brown, deep black-brown, bridal dark)
- 3 skin finishes, ~18 makeup shades, 3 makeup presets
- 6 expressions, 4 poses
- 3 quick-start characters, one in hijab + gele
- ~60 suggested names (`names.json`)

### G.2 Body-fitted garments and veils (`w_mid`) — 19 items, 78 files

| # | Item ID | Role | Files |
|---|---|---|---|
| 1 | `top_buba_classic` | Tailor style: iro & buba | mask_body, shading, lineart, fixed_embellished = 4 |
| 2 | `wrapper_iro_classic` | Tailor style: iro & buba | 3 |
| 3 | `outer_ipele_classic` | Iro & buba shoulder piece (aso-oke ipele piece) | 3 + back_mask, back_shading, back_lineart = 6 |
| 4 | `top_blouse_offshoulder` | Tailor style: skirt & blouse | mask_body, mask_trim, shading, lineart, fixed_embellished = 5 |
| 5 | `bottom_skirt_mermaid` | Tailor style: skirt & blouse | 3 |
| 6 | `dress_gown_mermaid` | Tailor style: mermaid gown | mask_body, mask_trim, shading, lineart, fixed_embellished = 5 |
| 7 | `dress_kaftan_embroidered` | **Tailor style: embroidered kaftan** (Hauwa's specialty; floor-length, modest, formal in lace/brocade/shadda) | mask_body, mask_trim (neckline/placket panel), shading, lineart, fixed_embellished (embroidery) = 5 |
| 8 | `top_buba_freestyle` | Freestyle: one-shoulder ruffle buba | mask_body, mask_trim, shading, lineart = 4 |
| 9 | `top_blouse_freestyle` | Freestyle: giant puff sleeves | 3 |
| 10 | `dress_gown_freestyle` | Freestyle: dramatic slit and huge flare | 4 |
| 11 | `dress_kaftan_freestyle` | Freestyle: dramatic cape sleeves and train | mask_body, mask_trim, shading, lineart = 4 |
| 12 | `dress_abaya_modern` | Reward (modern abaya with a contrast-fabric front panel) | mask_body, mask_trim, shading, lineart = 4 |
| 13 | `dress_ankara_midi` | Starter (modern Nigerian) | 3 |
| 14 | `top_tee_basic` | Starter (casual) | 3 |
| 15 | `bottom_jeans_wide` | Starter (casual; denim finish) | mask, shading, lineart, fixed (stitching) = 4 |
| 16 | `top_peplum_modern` | Reward (modern) | 3 |
| 17 | `bottom_skirt_pencil` | Reward (modern) | 3 |
| 18 | `veil_hijab_wrap` | Starter (fabric-swappable; gele can sit on top) | mask, shading, lineart + back_mask, back_shading, back_lineart = 6 |
| 19 | `veil_mayafi_draped` | Reward/borrow (head-and-shoulder veil; blocks gele) | mask, shading, lineart + back_mask, back_shading, back_lineart = 6 |
| | **Total** | | **78** |

### G.3 Anchored accessories (shared canvases) — 53 files

| Item ID | Anchor | Files |
|---|---|---|
| `head_gele_fan` × tiers perfect / good / disaster × (front mask, shading, lineart + back mask, shading, lineart). One set works over hair or over a hijab, because the gele sits on the same head volume. | neck | 18 |
| `shoe_heels_block` (starter) | ankles | 3 |
| `shoe_stiletto_point` (reward) | ankles | 3 |
| `shoe_sandals_strappy` (starter; + fixed buckle) | ankles | 4 |
| `shoe_sneakers_basic` (starter; + fixed sole) | ankles | 4 |
| `bag_clutch_envelope` (starter; fabric-swappable + fixed clasp) | hand | 4 |
| `bag_tophandle_mini` (reward; finish + fixed hardware) | hand | 4 |
| `bag_tote_canvas` (starter) | hand | 3 |
| `fan_abebe_classic` (borrow/reward; fabric + fixed handle) | hand | 4 |
| `jewel_necklace_coral_layered` (borrow/reward; fixed art) | neck | 1 |
| `jewel_necklace_gold_pendant` (starter) | neck | 1 |
| `jewel_bracelet_coral` (borrow/reward) | wrist | 1 |
| `jewel_bangle_gold` (starter) | wrist | 1 |
| `jewel_earrings_coral_drop` (borrow/reward) | head | 1 |
| `jewel_earrings_gold_hoops` (starter) | head | 1 |
| **Subtotal** | | **53** |

**M1 item totals:**
- 34 player-facing items: 17 garments, 2 veils, 1 gele, 4 shoes, 3 bags, 1 fan, 6 jewellery.
- 1 system underlayer.
- 4 tailor styles: iro & buba, skirt & blouse, mermaid gown, embroidered kaftan.
- Amaka's borrow box (pick one per run): coral layered necklace, abebe fan, mayafi.

### G.4 Fabrics and materials — 31 files

| Asset | Count |
|---|---|
| Aso-oke tiles 512² (sanyan, alaari, etu) | 3 |
| Aso-oke `_sheen` maps | 3 |
| Kano Indigo tile + `_sheen` map (beaten-cloth glaze) | 2 |
| Lace tiles 512² RGBA greyscale (cord, beaded, guipure; tinted per colourway) | 3 |
| Weave-detail tiles (plain, heavy, damask, handwoven) | 4 |
| Finish tiles (denim, leather grain) | 2 |
| Motif SVGs: Ankara 6 (sunburst, cowrie, fan, circles, birds, diamond), adire-inspired 3 (comb lines, leaf spiral, dot grid), damask 2 (also used by ivory shadda), george embroidery 1, akwete-inspired 2 | 14 |
| **Subtotal** | **31** |

Data-only: 22 fabrics (with `localNames`), ~17 palettes, 5 finishes, adire oniko noise and george check (procedural).

### G.5 Environments and scene props — 38 files
Scenes are authored at **2732 × 2732** with a centred portrait-safe area (1260 × 2732) and a landscape-safe area (2732 × 1536), in 3 depth layers (back, mid, front) for parallax.

| Location / prop | Files |
|---|---|
| Yaba room/studio (bed, mirror, rail, window; 3 layers) | 3 |
| Balogun market: Iya Bisi's stall + market street (3 layers). Passers-by include hijab-wearing and Northern-dressed shoppers | 3 |
| Market fabric bolt (mask, shading, lineart: shows real fabrics via the engine) | 3 |
| Market inspect drape (mask, shading, lineart) | 3 |
| Tailors' row: three shopfronts in one arcade, with Hauwa's showing embroidered kaftans (3 layers) | 3 |
| Owambe venue: hall, decorated tables, stage, canopy, food table, band/DJ corner (3 layers) | 3 |
| Couple on stage (the bride must exist for `dont_outshine_bride`) | 1 |
| Photographer figure | 1 |
| Guests: 6 figures × (body, arm) for bob and spray loops. At least 2 in hijab/kaftan and 1 man in babban riga or kaftan | 12 |
| Photo-area backdrops (gold drape, flower wall, adire indigo wall) | 3 |
| Travel vignette (keke through Lagos traffic) | 1 |
| Tailor's nylon bag (closed, open) | 2 |
| **Subtotal** | **38** |

Photo-mode backgrounds = 3 backdrops + room + market + venue = **6**, with no extra art.

### G.6 NPC portraits — 37 files
Bust cut-outs at 1024 × 1024, in the same style as the player character, usable in dialogue and placed in scenes.

| NPC | Expressions | Files |
|---|---|---|
| Amaka | neutral, excited, sceptical, laughing | 4 |
| Mummy | worried, unimpressed, secretly proud | 3 |
| Iya Bisi | welcoming, pleased, annoyed, scandalised, delighted | 5 |
| Baba Tee | neutral, sheepish, proud | 3 |
| Kunle Cuts | neutral, sheepish, proud | 3 |
| Hauwa Stitches | neutral, sheepish, proud | 3 |
| Aunty Sade | approve, neutral, disapprove, shocked | 4 |
| Zara (in hijab) | approve, neutral, disapprove, shocked | 4 |
| Uncle Bayo | approve, neutral, disapprove, shocked | 4 |
| Dami | approve, neutral, disapprove, shocked | 4 |
| **Subtotal** | | **37** |

### G.7 UI and FX — 63 files

| Asset | Files |
|---|---|
| Logo (after-party wordmark) | 1 |
| Aso-oke strip set: panel border strip, tab, progress fill, button label (SVG, 9-slice) | 4 |
| Icons: 12 categories (top, bottom, dress, outerwear, shoes, bag, jewellery, gele, veil, hair, makeup, fabric), 3 currencies (₦, ✨, XP), 16 nav/system (back, close, settings, menu, undo, redo, save, share, camera, lookbook, phone, map, sleep, spotlight/info, sound on, sound off), 2 haggle (deal, walk away) | 33 |
| Gele gesture prompts (fold, pleat, align, wrap, tuck, tighten) | 6 |
| Dance prompts (tap, hold, swipe left, swipe right) | 4 |
| Phone frame (also frames the NaijaGram card) | 1 |
| Spray notes: 3 **fictional** denominations × front/back (stylised, clearly not replicas of CBN notes) | 6 |
| FX textures: sparkle ×2, camera flash, confetti ×3, dust poof, soft glow | 8 |
| **Subtotal** | **63** |

Fonts: 2 open-licence families (one display face from the ART_SPEC shortlist, one humanist sans), self-hosted.

### G.8 Audio — 40 files

| Asset | Count |
|---|---|
| Music loops: room/theme, market, tailors' row (with Hausa-inspired instrumentation, Hauwa's corner), Owambe party, dance track (30 s, fixed BPM, beat map in `audio.json`), photo/results | 6 |
| Stingers: great deal, tailor reveal, level up, disaster | 4 |
| SFX: UI tap, tab, fabric swish, cash register, deal stamp, phone buzz, message pop, call ring, bag zip, garment drop, gele steps ×6 (one per gesture), gele tighten, gele collapse, crowd cheer, crowd gasp, crowd laugh, note flutter, note collect, shutter, heels walk-in, market ambience, venue ambience, talking-drum hit, miss | 30 |
| Voice | 0 (M2) |
| **Subtotal** | **40** |

### G.9 Totals

| Group | Files |
|---|---|
| Character base | 191 |
| Garments + veils | 78 |
| Accessories | 53 |
| Fabrics/materials | 31 |
| Environments | 38 |
| NPC portraits | 37 |
| UI/FX | 63 |
| **Visual total** | **491** |
| Audio | 40 |
| Fonts | 2 families |

**Writing (content, not art):**
- ≈ 25 lines per judge (100)
- ≈ 40 Iya Bisi lines
- ≈ 12 per tailor, ≈ 18 for Hauwa (≈ 42)
- 3 story scenes
- 22 fabric spotlight notes with local names
- ≈ 60 suggested names
- ≈ 20 NaijaGram comments
- ≈ 15 guest barks across Nigerian voices

Every Pidgin/Yoruba/Hausa/Igbo line and every name is `review: true`.

**Art cost levers, if needed:**
- A second body shape later costs +87 files (body 4, arm masks 2, underlayer 3, garments and veils 78).
- 3 face presets instead of 4 saves 39.
- Dropping the 4 freestyle garments saves 15, but loses the best tailor joke.

---

## H. Animation requirements

All animation is code-driven in M1 (tweens, shaders, mesh rig, particles). The art is static. Reduced-motion mode replaces movement with fades and caps particles. Target: **60 fps on a mid-range Android** during dress-up and spray.

| Area | Animation | Technique | Priority |
|---|---|---|---|
| Global | Screen transitions (fabric-swipe wipe), panel slide, button press, count-ups | GSAP / CSS | Must |
| Character | Idle breathing (torso scale ≤ 1%), blink every 3–6 s, expression swaps with a 120 ms ease | Rig + part swap | Must |
| Character | Pose transitions (arm bones), head tilt | Cutout rig (B.6.6) | Must (fallback: body-level) |
| Fabric | Aso-oke/brocade sheen sweep, lace shimmer on movement | Per-frame sheen shader | Must |
| Create/styling | Equip "settle" (garment fades in with a 4 px drop + sparkle), fabric swap ripple | Tween + FX | Must |
| Market | Ambient: hanging fabric sway, passers-by silhouettes, Iya Bisi expression changes, price tag wobble on counter, **deal stamp slam + confetti** on a great deal | Tween, mesh sway, particles | Must |
| Tailor | Message pop-ins on the phone, "typing…" dots, **bag reveal** (shake ×3, unzip, garment drops onto character with a flash) | GSAP timeline | Must |
| Gele | Cloth as a mesh rope/plane textured with the chosen fabric: fold, pleat accordion, wrap around the head, tuck, tighten pulse. Tier reveal. **Disaster:** slow lean, wobble, collapse with a dust poof | Pixi mesh + tweens | Must (signature) |
| Travel | Keke bouncing through traffic, parallax (3 s, skippable) | Tween | Should |
| Venue | Guests bobbing on the beat, light-string twinkle, photographer flashes, couple sway on stage | Loops + FX | Must |
| Arrival | Camera dolly, silhouette-to-colour reveal, flashbulb burst, crowd turn | GSAP + filters | Must |
| Judging | Portrait card slide-in, reaction bounce, text type-on, breakdown bars weaving in | GSAP | Must |
| Money spray | Notes spawn from guest hands, tumble (rotation + scaleX flip for faux 3D), flutter drag, gravity, settle. Tap → fly to counter with a coin-count tick. Finale burst. Cap 300 live notes, pooled | Custom particle pool | Must |
| Dance | Beat-synced prompts, character moves (4 rig move sets: two-step, shoulder bounce, hand wave, spin-fake via scaleX), hit/miss feedback, crowd cheer. Gele collapse on disaster tier | Rig keyframes on audio clock | Must |
| Photo | Shutter flash, filter crossfade, pose snap ease | Tween + filters | Must |
| Results | Count-ups, level-up woven banner unfurl, new-item card flip | GSAP | Must |

---

## I. Biggest technical risks

| # | Risk | Why it matters | Mitigation |
|---|---|---|---|
| T1 | **GPU memory and fill-rate on mobile** | One 1024×2048 RGBA texture is 8 MB. A naive outfit (≈ 30 layer files) could need 240 MB+ and crash mobile Safari or Chrome. | Channel packing, trimming and 0.5× variants (B.6.5). Composite to RTs only on change. Per-scene asset bundles. Measure on a real device in Phase 2. |
| T2 | **Fabric look quality** | Tiled prints can look like wallpaper. Overlay shading can flatten dark fabrics. This is the game's headline feature. | Per-region fabric transforms, a weave-detail tile, a custom shader with fabric-aware shadow tint, and sheen. Phase 3 "any fabric on any garment" screenshot matrix. |
| T3 | **Cutout arm rig seams** | Bad shoulders look cheap. Fixing the A-pose rule after commissioning art is expensive. | Spike in Phase 2 on placeholders. Lock the art rule before commissioning. Fallback to whole-body poses. |
| T4 | **Gele minigame feel** | Gesture recognition, mobile scroll/zoom conflicts, a cloth mesh that reads as cloth. It's the signature feature. | `touch-action: none` on the canvas. Simple gesture vocabulary (drag direction + hold + timing). Paper prototype and a Pixi spike in Phase 7 week 1. Tuning in config. |
| T5 | **Pixi + React lifecycle** | StrictMode double-mounts, HMR and WebGL context loss can leak or blank the canvas. | One Pixi Application outside React. Commands via a bridge. Context-loss handler rebuilds RTs from state. |
| T6 | **Pixi v8 specifics** | Advanced blend modes are filter-based and slow. Mesh/shader APIs differ from v7 tutorials. | Custom shaders from day one. Pin the version. Small render tests. |
| T7 | **Save durability on Safari** | Safari's ITP can delete script-written storage (IndexedDB) after 7 days without a visit. Private mode limits storage. | `navigator.storage.persist()`. "Export save" / "Import save" (JSON file) in settings. Clear messaging. Capacitor and cloud saves fix this in M2. |
| T8 | **Rhythm timing** | Frame-clock timing drifts, and Bluetooth/Android audio latency ruins the dance. | Use the WebAudio context time as the clock. Generous windows. Latency offset calibration in settings. The dance is optional. |
| T9 | **Load time under 3 s on mid Android** | Many PNGs, fonts and audio. | Lazy scene bundles. Preload the next scene during story beats. WebP for colour tiles. Audio streamed. KTX2/Basis only if measurements need it. |
| T10 | **Photo export across browsers** | WebGL readback, Web Share with files (patchy on desktop), iOS download quirks. | `renderer.extract` at a fixed export resolution. Web Share Level 2 where `canShare({files})`, otherwise a download. Tested on iOS Safari and Android Chrome. |
| T11 | **Content and save drift** | Renamed IDs break saves and future shared Looks. | `id-lock.json`, typed migrations with fixtures, `contentVersion` in saves and Looks. |
| T12 | **Procedural pattern quality** | Generated "Ankara" can look like clip-art. | Strong motif art (counted in G.4), curated palettes, layout rules, weave overlay. Every generated fabric is labelled "inspired by". |

---

## J. Biggest product and gameplay risks

| # | Risk | Mitigation |
|---|---|---|
| P1 | **Placeholder art makes it feel like a demo.** Playtesters judge a "premium fashion game" on looks, and BRIEF §29 forbids poor placeholder UI. | Make UI, fabrics, FX and motion final-quality early: they're code-driven. **Commission the ART_SPEC §8 style test during Phase 3**, not after M1 (see M). |
| P2 | **Too long.** The first run estimates ≈ 11 min against a 5–10 target. | Fast paths everywhere. Skippable cinematics on replay. Measure with the timing log. Cut market browsing before cutting humour. |
| P3 | **Haggling gets "solved"** (always lowball, then walk away). | Mood, patience and relationship. Walk-away callbacks are probabilistic and depend on the offer gap. Rudeness raises the price. A great deal needs reading her face. Fully unit-tested. |
| P4 | **Scoring feels opaque or has one best outfit.** That kills "replay with a different strategy". | Evidence-based judge lines name the cause. Judges disagree by design (Zara loves drama, Uncle Bayo hates it). Creativity rewards *not* repeating. The results screen suggests a different strategy. |
| P5 | **Tailor RNG feels unfair** (freestyle ruins a great plan). | Odds follow personality (Baba Tee is clearly a gamble). Freestyle outcomes are context-dependent, often good, and always funny. Late is never a dead end. Following up reduces risk. |
| P6 | **Humour lands as stereotype.** Aunty, Uncle and market-woman archetypes are risky. | Characters have depth (Uncle "secretly soft", Dami's arc). Humour comes from situations, not ethnicity (GDD §11). Every line `review: true`. A cultural reviewer before playtest. |
| P7 | **"Nigerian = Yoruba/Lagos"**, or Muslim/Northern presence as tokenism. The M1 event is Yoruba. | Amaka is Igbo. Zara is a Kaduna-born hijabi influencer and judge. Hauwa's embroidered kaftan is a full tailor style. Hijab, gele-over-hijab, mayafi, abaya, lalle and Kano indigo are all in M1 and score fairly (0.4, D.9). George and akwete are in the market. The names list spans the country. Hausa/Fulani and Muslim reviewers sit alongside Yoruba and Igbo reviewers. |
| P8 | **Gele too hard or too easy across devices.** | Tuning in config, practice mode, and 3 tiers where "good" is easy and "perfect" is mastery. Disaster is funny, not punishing. |
| P9 | **Women-only M1 alienates part of the audience.** | State "men's styles coming" on the create screen. Architecture is ready. Revisit after playtest (decision 2 below). |
| P10 | **Save Look has little value without social.** | Make the exported photo great (watermarked, share-sheet) so sharing happens *outside* the game. That's BRIEF's "I need to send this to my friend". |
| P11 | **Spray notes and money language.** Depicting real CBN notes may raise legal or cultural issues. | Fictional, stylised notes. Copy stays clearly in-game. No real-money link. |
| P12 | **Economy soft-lock** (spend everything at the market). | Safety-net gift. The starter wardrobe always allows completion. A tested invariant: every run is completable. |
| P13 | **Real designer brands** (BRØNZE in GDD). | Not in M1 (BRIEF §29: no payments, no real-people content). Revisit with designer agreements. |

---

## K. What to build first

1. **Phase 1 foundation with a walking skeleton.** Every screen in F exists as a stub with real flow transitions, so the whole loop is clickable end-to-end in under a minute from day one. Each later phase replaces a stub, so the game stays runnable (BRIEF §26).
2. **Content pipeline and integrity checks**, `rng`, `ids`, `formatNaira`, the action reducer skeleton, versioned saves with migrations, and the asset build/placeholder scripts.
3. **The two highest technical risks as spikes inside Phase 2:**
   - one garment through the full fabric shader + RT composite on a real mid-range Android phone (T1, T2, T6),
   - the arm rig on a placeholder body (T3).

   Results decide the A-pose rule before any art spend.

---

## L. What NOT to build yet

- Accounts, login, backend, cloud saves, any network calls, analytics backend.
- Chat, friends, following, clubs, posts, likes, comments, voting, leaderboards, multiplayer events.
- Payments, premium currency, shop/boutique, designer drops (BRØNZE), ads.
- NaijaGram feed (only the single results-screen post card is in), gossip threads, trends, random events, rent, time slots, multiple challenges/chapters, other cities.
- Men's presentation and men's garments. Any body shape beyond `w_mid`. Tribal marks, state of origin.
- Adire studio, the lalle/henna *minigame* (static lalle designs are in), gele shape unlocks, user-saved makeup presets, hair length/accessories, contour.
- Voice acting, licensed music, real celebrities.
- AI stylist / living NPCs, and any Anthropic API call.
- Spine/DragonBones skeletal art pipeline (the cutout rig only).
- Capacitor builds, PWA/offline install, localisation beyond English + data-driven Pidgin/Yoruba lines.
- A walkable wardrobe room, home decoration, upgrades.

---

## M. Recommended development sequence

The ROADMAP phases, with the tweaks marked ★.

| Phase | Build | Key output |
|---|---|---|
| 0 | This document | Approval |
| 1 | Foundation + content pipeline + **★ walking skeleton of all screens** + asset build/placeholder scripts + **★ ESLint import boundaries** | Clickable loop of stubs, validation, saves |
| 2 | Character rendering + skin pipeline + create screen + **★ spikes: fabric shader on device, arm rig** | 12-tone screenshot, A-pose decision |
| 3 | Fabric engine (22 fabrics with local names, procedural, sheen, lace) + styling screen + UI design system (aso-oke strips, typeface) · **★ commission the illustrator style test in parallel** (ART_SPEC §8) | Any fabric on any garment |
| 4 | Beauty: tone-adaptive makeup, hair, static lalle | 3 presets × 4 tones grid |
| 5 | Market: `haggle.ts` (tested) + **★ the minimal Line/condition runner and bark UI** (needed here, not in 11) | Funny haggling |
| 6 | Tailor: `tailor.ts` (tested), sleep/day, phone, reveal, freestyle garments | The gamble and the reveal |
| 7 | Gele minigame (spike in week 1) | Signature minigame |
| 8 | Scoring + judges (`scoring/` fully tested, evidence → lines) | Specific, funny reactions |
| 9 | Owambe venue, arrival, spray, dance, rewards plumbing | The celebration |
| 10 | Photo mode, Save Look, export/share, lookbook | Shareable photo |
| 11 | Story scenes (3), progression (3 levels), borrow box, replay hooks, safety net | Complete, replayable loop |
| 12 | Polish: audio, onboarding, performance on device, accessibility, timing log, feedback link, static deploy | Playtest build |

★ Moving the dialogue runner to Phase 5 and the style test to Phase 3 changes ROADMAP order but not scope.

---

## Approved decisions (Bronze, 2026-10-08)

| # | Decision | Outcome |
|---|---|---|
| 1 | Body shapes in M1 | **One (`w_mid`).** The renderer, data and art rules stay multi-shape, so a second shape costs +87 files later. |
| 2 | Men's presentation in M1 | **No**, revisit after playtest (conflict #1, chosen on merit). |
| 3 | A-pose + arm rig art constraint | **Yes**, proven by the Phase 2 spike before art is commissioned. |
| 4 | Tools | **Approved:** GSAP (runtime). ESLint + Prettier, sharp + @resvg/resvg-js, Playwright (all dev). Added to the CLAUDE.md stack. |
| 5 | Amaka's borrow box | **Yes.** Coral layered necklace, abebe fan or mayafi. |
| 6 | More Northern and Muslim fashion and names | **Yes**, see 0.4: hijab (and gele over hijab), mayafi, embroidered kaftan tailor style, modern abaya, static lalle, Kano Indigo + ivory shadda, local fabric names, `names.json`, Zara as a hijabi influencer, Hausa/Fulani and Muslim reviewers. |
| 7 | Conflicts | **Resolved on merit** (0.2). Changed from the draft: #2 one body shape, #17 a single NaijaGram post card, #18 static lalle. |
| 8 | Fix "Owambe → after-party" text, update CLAUDE.md rules 3–4 and ART_SPEC | **Done** in the approval change. |
| 9 | Split `fabrics.json`, re-key challenge weights and judge focus, add line IDs, remove the Kano Indigo lock | **Phase 1** (data migration with schemas). |
| 10 | Illustrator style test during Phase 3 | **Yes.** |
