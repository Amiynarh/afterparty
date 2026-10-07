# after-party — Build Roadmap (Claude Code)

How to use: one phase per Claude Code session. Copy the prompt, paste it, review the plan Claude Code proposes, then let it build. Check every "done when" box by actually playing before you commit. Run `/clear` before the next phase. The game must stay runnable at the end of every phase.

**Milestone 1 (Phases 0–12) = The after-party Loop** from `docs/BRIEF.md`: one polished 5–10 minute playthrough.
**Milestone 2 = Chapter 1** (see bottom).

---

## Phase 0 — Architecture kickoff (no code)

**Prompt:**
> Read CLAUDE.md, docs/BRIEF.md, docs/GDD.md, docs/ART_SPEC.md and everything in data/. Do NOT write any code. Answer BRIEF section 30, items A–M, in full. Rules for your answer: (1) The stack in CLAUDE.md is my current decision. Evaluate it against the brief and recommend changes only if you have a strong reason, stated plainly. (2) Use the fabric/garment layer contract in ART_SPEC section 4 as the clothing-layer design unless you can show a better one. (3) BRIEF wins on Milestone 1 scope; GDD fills in design detail. List every place where they conflict and say which you followed. (4) Data models must satisfy the multiplayer-ready rule in CLAUDE.md, with stable IDs and PlayerProfile separate from CharacterAppearance and Look, but propose no backend. (5) For G (art assets), give an exact asset list for Milestone 1 with counts. Save the whole answer as docs/ARCHITECTURE.md, then summarise it for me and stop and wait for my approval.

**Done when:** you've read ARCHITECTURE.md, pushed back on anything you don't like, and told Claude Code "approved" (it should then mark the doc as approved).

---

## Phase 1 — Foundation + content pipeline

**Prompt:**
> Read CLAUDE.md and docs/ARCHITECTURE.md. Scaffold the project per the approved architecture and the CLAUDE.md folder layout; pin exact versions. Implement: src/config/game.ts, src/lib/rng.ts (seeded, tested), Zod schemas for every data model in ARCHITECTURE.md, a content loader that validates all data/*.json at boot and shows a clear error screen if anything is invalid, `npm run validate:content`, versioned save/load (IndexedDB, 3 slots, migration hook), and a simple scene/flow manager matching the screen flow in ARCHITECTURE.md. Add data/items.json (about 25 placeholder items), data/bodies.json and data/skins.json per ART_SPEC. Title screen "after-party" with New game / Continue. Fill in the Commands section of CLAUDE.md.

**Done when:** title screen works on a phone viewport · validation passes, and breaking a JSON field shows a readable error · save, reload, continue works · tests green.

---

## Phase 2 — Character rendering

**Prompt:**
> Read ART_SPEC 2, 3, 5, 7 and the character sections of ARCHITECTURE.md. Build the Pixi character stage: a CharacterRenderer that stacks layers per src/render/layers.ts, placeholder art generated to the real spec (clearly tagged PH) for the body shapes, and the skin pipeline (base, shadow, highlight maps tinted per tone with hue-shifted shadows, never grey multiply). Build character select/create: skin tone, body shape, face preset, hairstyle. Rendering must read only CharacterAppearance, never PlayerProfile.

**Done when:** put all skin tones side by side in a screenshot; every one looks warm and rich · switching is instant · appearance saves.

---

## Phase 3 — Fabric engine + wardrobe

**Prompt:**
> Read GDD 5.2–5.3, BRIEF sections 7 and 9, ART_SPEC 4. Build the fabric engine: tiled fabric clipped by garment mask, shading blend, fixed details, lineart; multiple fabric regions per garment; aso-oke sheen and lace transparency. Create data/fabrics for 15–25 fabrics (extend data/fabrics.json; generated patterns must be labelled "inspired by", never claimed as historical originals). Make patterns procedural-ready ({ motifId, paletteId, layout, seed }). Then build the wardrobe/dress-up screen: character on top, category tabs styled as fabric swatches, item drawer, fabric picker, undo, Save Look. Propose the UI design plan (palette from ART_SPEC, display typeface, how the aso-oke strip motif is used) before building it.

**Done when:** any fabric looks right on any garment · a full look takes under 2 minutes on a phone · it feels like a fashion game, not a form.

---

## Phase 4 — Beauty (hair + makeup)

**Prompt:**
> Read BRIEF section 13 and GDD 5.5. Build a lightweight makeup system (skin finish, blush, eyes, lashes, lips, highlight) and hairstyle selection with colour. Every shade must be tested on the deepest and lightest skin tones; blush and highlight must stay visible and flattering on dark skin. Presets must not make faces look the same. Integrate into the dress-up screen.

**Done when:** a screenshot grid of 3 presets × 4 skin tones all look good.

---

## Phase 5 — The market

**Prompt:**
> Read BRIEF section 8, GDD 5.4 and Iya Bisi in data/npcs.json. Implement systems/haggle.ts as a pure, unit-tested state machine (firmness, mood, relationship; moves: accept, "too expensive", "final price?", counter-offer, walk away, return). Build the Balogun market scene: lively stalls, fabric bolts to browse and inspect (zoom on texture), price comparison, Iya Bisi with portrait, reactions and humour from data. A great deal triggers a satisfying celebration moment; a bad bargain gets a funny line. Bought fabric goes to inventory.

**Done when:** walking away at the right moment actually saves money · rudeness costs you · someone watching you play laughs.

---

## Phase 6 — The tailor

**Prompt:**
> Read BRIEF section 10, GDD 5.4 and the three tailors in data/npcs.json. Implement systems/tailor.ts (pure, tested, seeded RNG): order = fabric + style + tailor; outcomes perfect / late / freestyle / masterpiece driven by skill, reliability, speed, creativity. Simulated time only: a "sleep / next day" action and phone messages ("almost ready", "I'm on my way", "your tailor has sent a message"). Build the tailor shop (choose tailor, pick a style, see quote and promised date) and a dramatic delivery reveal. A late or freestyle result must be funny and still playable, never a dead end.

**Done when:** choosing a tailor feels like a real gamble · the reveal makes you hold your breath.

---

## Phase 7 — Gele minigame (signature)

**Prompt:**
> Read BRIEF section 12 and GDD 5.5. Build src/minigames/gele as a self-contained Pixi minigame: fold, pleat, align, wrap, tuck, tighten via touch/mouse gestures and timing. Three outcome tiers (perfect, good, disaster) with matching visual results using the chosen gele fabric. Disaster is lopsided or collapsing and funny, with the character reacting using original lines. The result feeds the score. Include a practice/retry option.

**Done when:** you want to replay it to get a perfect gele · a disaster makes you laugh, not quit.

---

## Phase 8 — Scoring + judges

**Prompt:**
> Read BRIEF sections 11 and 15, GDD 5.6, and the judges in data/npcs.json (Aunty Sade, Uncle Bayo, Zara, Dami). Implement systems/scoring.ts (pure, thoroughly tested): sub-scores for Style, Cultural Fit, Colour Harmony, Accessories, Event Appropriateness, Creativity, plus gele quality and special rules (dont_outshine_bride). Map sub-scores to judge reactions that reference what the player actually wore (item names, colours, gele result). No repeated lines per playthrough. Build a judge reaction sequence UI with portraits and a short readable breakdown, never bare stars.

**Done when:** two very different outfits get clearly different, specific, funny reactions · outshining the bride gets roasted.

---

## Phase 9 — The after-party: event, money spray, dance

**Prompt:**
> Read BRIEF sections 14, 16, 17 and GDD 5.7. Build the after-party venue (decorated tables, guests, stage, photographer, food; ambient animation so it feels alive) with an entrance reveal, then the judging from Phase 8, then the money spray: naira notes flying and raining with an amount based on outfit + gele + judges, tap to collect, satisfying sound. Then an optional 20–30 second rhythm dance game on an original placeholder beat; a good performance boosts the spray, a bad one is funny. Then rewards.

**Done when:** a high score feels like a celebration you want to see again · the whole event takes about 3 minutes.

---

## Phase 10 — Photo mode + Save Look

**Prompt:**
> Read BRIEF section 18 and GDD 5.10. Build photo mode: pose presets, expression, camera angle, zoom, background sets, lighting/filter presets, PNG export with a subtle watermark, Web Share API where available. Save Look stores a serialisable Look (stable item IDs, fabrics, appearance, photo settings) in a lookbook, designed so it could later be posted publicly.

**Done when:** you want to send the photo to a friend.

---

## Phase 11 — Story scenes + progression

**Prompt:**
> Read BRIEF sections 19–21 and GDD 5.11. Build a small data-driven dialogue system (node graph, conditions, effects). Write 2–3 short, fast, funny scenes as data: Mummy's sceptical call, Amaka's encouragement and the after-party invitation, and a post-event closing beat. Implement XP and levels (New Stylist, Known Around Town, Rising Fashion Name), reputation and a new-item reward. Mark every Pidgin/Yoruba line "review": true. Add replay hooks: the end screen suggests a different strategy (other tailor, other fabric, aim for perfect gele).

**Done when:** a new player completes the loop in 5–10 minutes with no instructions and wants to go again.

---

## Phase 12 — Polish + playtest build

**Prompt:**
> Polish pass against BRIEF sections 28–29: audio (original placeholder tracks and UI sounds), transitions, loading states, an onboarding woven into the first scenes, performance on a mid-range Android (60fps dress-up, under 3s load), accessibility (text size, reduced motion, contrast), a feedback button. Remove any CRUD-feeling screens. Produce a deployable build and deploy steps for Vercel or Netlify.

**Done when:** you send the link to 10 playtesters and watch at least 3 play live.

---

## Milestone 2 — Chapter 1 and beyond
1. Fix what playtesting revealed.
2. Art style test with an illustrator (ART_SPEC 8); swap in real art.
3. Calendar, rent and the full Chapter 1 challenges (`data/challenges.json`), Dami's arc, Mrs. Okafor finale.
4. NaijaGram and random events (GDD 5.9, 5.12).
5. Spine animation.
6. Capacitor iOS/Android.
7. Backend (accounts, cloud saves, profiles) — the first multiplayer step.
8. Later: competitions, AI stylist, new cities, designer drops (BRØNZE first).
