# after-party — Art Direction & Asset Spec

This file is the contract between code, placeholder art, and the illustrators. If an asset follows this spec, it drops into the game with no code changes.

## 1. Art direction

**Style:** high-end 2D illustrated fashion editorial — think fashion-week sketchbook brought to life, with painterly skin, crisp lineart, and rich textiles. Not chibi, not hyper-real 3D. 2D is a deliberate choice: it delivers premium quality at a scale a small team can produce, and it makes fabric swapping on every garment possible.

**Animation:** characters are rigged with skeletal 2D animation (Spine or DragonBones) from Phase 2 of art onwards: idle breathing, fabric sway, gele shimmer, walk-in, dance loops, money-spray reactions. MVP placeholders are static.

**The signature UI element:** *aso-oke strips.* Panel borders, tabs and progress bars use woven-strip motifs (the narrow-loom strips aso-oke is sewn from). Swatches are the main UI metaphor: categories are fabric tabs, buttons feel like woven labels. Spend the boldness there; keep the rest of the UI quiet.

**Palette (UI)**
| Name | Hex | Use |
|---|---|---|
| Adire Indigo | `#1F2A5C` | primary, headers, night scenes |
| Coral Bead | `#D2452F` | key actions, alerts, spray highlights |
| Gold Thread | `#E2B13C` | rewards, Influence, premium |
| Sanyan | `#E9DCC3` | panels, backgrounds |
| Palm Green | `#2E6B4F` | success, positive scores |
| Kola | `#5A2E1E` | text on light |

**Type:** a characterful display face for titles and event cards (candidates: *Gloock*, *Clash Display*, *Bricolage Grotesque*; pick one in Phase 4 after seeing it on screen) and one clean humanist sans for UI body text. Sentence case everywhere.

## 2. Canvas and anchors
- Character canvas: **1024 × 2048 px** (1:2), transparent PNG, character standing front-facing, feet baseline at y = 1940.
- Every asset for a given body shape uses the same canvas and origin, so layers align by simply stacking.
- Export at 1x; the game downsamples. Keep source files layered (PSD/Procreate) at 2x.
- Anchor points (per body shape, stored in `data/bodies.json`): head-top, neck, shoulders L/R, elbows L/R, waist, hips, wrists L/R, hands L/R, ankles L/R. Accessories snap to anchors.
- **Milestone 1 ships one body shape, `w_mid`.** Art must still follow the multi-shape rules below so more shapes can be added later.
- **Head canvas:** face parts, makeup masks, hair, gele and earrings are authored on a **1024 × 1024** canvas at the same pixel scale as the body, registered to the `neck` anchor. **All body shapes share the same head size and neck point**, and **feet are identical across body shapes**, so head-region assets and shoes are shared. Bodies are delivered neck-down; heads come per face preset.
- **Base pose: relaxed A-pose.** Arms ~15–20° away from the torso with a visible gap at the waist, and nothing hidden behind the arms except a small shoulder overlap. Each body also ships `arm_l` / `arm_r` region masks. The engine's cutout rig poses the arms, so garments are drawn once, in this pose only.

## 3. Skin system
- 12 base tones, from deepest (`skin_01`) to light brown (`skin_12`). Each tone has: base colour, **shadow colour** and **highlight colour**.
- **Never shade dark skin by multiplying with grey or black.** Shadows hue-shift warmer/redder (toward burnt umber, plum or red-brown); highlights shift slightly cool/golden with a soft sheen. This is the single biggest quality difference.
- Body art is delivered as: `body_base` (greyscale value map), `body_lineart`, `body_shadow_mask`, `body_highlight_mask`. The engine tints them with the tone's three colours.
- Faces: features as separate layers (brows, eyes, nose, lips) for expression swaps.

## 4. Garment layers (the fabric contract)
Each garment, per body shape, is delivered as:

| File | Content |
|---|---|
| `{id}_{body}_mask_{region}.png` | Solid white where fabric shows, one file per fabric region: `body` (always), and `trim` / `sleeve` if the garment has them. |
| `{id}_{body}_shading.png` | Greyscale folds/shadows, mid-grey (#808080) = neutral. Applied with an overlay/soft-light blend over the fabric. |
| `{id}_{body}_lineart.png` | Seams, edges, folds in a dark warm line colour. |
| `{id}_{body}_fixed.png` *(optional)* | Non-fabric parts: buttons, embroidery, beading, metal. Not tinted. |
| `{id}_{body}_back_mask_{region}.png`, `_back_shading.png`, `_back_lineart.png` *(optional)* | Fabric-bearing parts that render behind the body (back of a gele or hijab, ipele or mayafi drape). They follow the same contract as the front. A non-fabric back can be a single `_back.png`. |
| `{id}_{body}_fixed_embellished.png` *(optional)* | Embroidery/beading overlay used for the tailor "masterpiece" outcome and Hauwa Stitches' embroidery. |

The engine renders: tiled fabric → clipped by mask → shading blend → fixed details → lineart. The build script trims and channel-packs these files for the GPU; artists always deliver them as separate files. Anchored items (gele, shoes, bags, earrings) use the head canvas or anchor and drop `{body}` from the name.

Fabric textures: seamless tiles, 512 × 512 px. Aso-oke, Kano indigo and brocade include a separate `_sheen` map for animated light catch. Lace is a single greyscale RGBA tile: its own alpha channel carries transparency, and it is tinted per colourway.

## 5. Layer order (first is furthest back)
1. Background
2. Back hair
3. Headwear back (gele back)
4. Garment `_back` parts (ipele, mayafi, hijab drape)
5. Body, then body art (lalle)
6. Head (skin), face makeup base (blush, highlight, eyeshadow), face features (eyes, brows, mouth, lashes, liner, lip colour)
7. Underlayer (base)
8. Bottoms / wrappers
9. Tops / dresses / kaftans / abayas
10. Outerwear (ipele; later agbada)
11. Shoes
12. Jewellery (neck, wrist)
13. Front hair (hidden under hijab or mayafi)
14. Earrings
15. Veil (hijab, mayafi)
16. Headwear front (gele, which can sit over a hijab)
17. Held items (bag, fan)
18. FX (sparkle, sheen)

Source of truth in code: `src/render/layers.ts` (see ARCHITECTURE B.6.4).

## 6. Naming
`{category}_{shortname}_{variant}` e.g. `top_buba_classic`, `head_gele_fan`, `shoe_bronze_stiletto`. Lowercase, underscores, no spaces.

## 7. Placeholder art (what Claude Code generates in Phases 2–3)
- Generated SVG → PNG at the real canvas size, using the real anchors.
- Body: simple silhouette with correct proportions per shape.
- Garments: flat silhouette masks with simple shading gradients and lineart, so the full fabric pipeline is exercised.
- Clearly marked with a small "PH" tag in a corner so nothing ships by accident.

## 8. Briefing illustrators (later)
Send this file, `data/bodies.json`, three garment examples rendered in-engine, the skin tone sheet, and a mood board. Commission a **style test first**, during build Phase 3: one body shape (`w_mid`, A-pose), one skin tone, one outfit (iro & buba + gele), delivered to spec. Only scale up after it drops into the engine cleanly. The full Milestone 1 asset list with counts is in ARCHITECTURE section G.
