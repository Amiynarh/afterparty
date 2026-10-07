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
- Anchor points (per body shape, stored in `data/bodies.json`): head-top, neck, shoulders L/R, waist, hips, wrists L/R, ankles L/R. Accessories snap to anchors.

## 3. Skin system
- 12 base tones, from deepest (`skin_01`) to light brown (`skin_12`). Each tone has: base colour, **shadow colour** and **highlight colour**.
- **Never shade dark skin by multiplying with grey or black.** Shadows hue-shift warmer/redder (toward burnt umber, plum or red-brown); highlights shift slightly cool/golden with a soft sheen. This is the single biggest quality difference.
- Body art is delivered as: `body_base` (greyscale value map), `body_lineart`, `body_shadow_mask`, `body_highlight_mask`. The engine tints them with the tone's three colours.
- Faces: features as separate layers (brows, eyes, nose, lips) for expression swaps.

## 4. Garment layers (the fabric contract)
Each garment, per body shape, is delivered as:

| File | Content |
|---|---|
| `{id}_{body}_mask.png` | Solid white where fabric shows. Separate masks per fabric region if the garment has `body`, `trim`, `sleeve` regions. |
| `{id}_{body}_shading.png` | Greyscale folds/shadows, mid-grey (#808080) = neutral. Applied with an overlay/soft-light blend over the fabric. |
| `{id}_{body}_lineart.png` | Seams, edges, folds in a dark warm line colour. |
| `{id}_{body}_fixed.png` *(optional)* | Non-fabric parts: buttons, embroidery, beading, metal. Not tinted. |
| `{id}_{body}_back.png` *(optional)* | Parts that render behind the body (back of a gele, agbada drape). |

The engine renders: tiled fabric → clipped by mask → shading blend → fixed details → lineart.

Fabric textures: seamless tiles, 512 × 512 px. Aso-oke and brocade include a separate `_sheen` map for animated light catch. Lace includes an alpha map for transparency.

## 5. Layer order (front to back reversed: first is furthest back)
1. Background
2. Back hair · garment `_back` parts · gele back
3. Body
4. Underwear-level / base layer
5. Bottoms / wrappers
6. Tops / dresses
7. Outerwear / agbada / kaftan
8. Shoes
9. Jewellery (neck, wrist)
10. Front hair
11. Headwear / gele front
12. Held items (bag, fan)
13. FX (sparkle, sheen)
Source of truth in code: `src/render/layers.ts`.

## 6. Naming
`{category}_{shortname}_{variant}` e.g. `top_buba_classic`, `head_gele_fan`, `shoe_bronze_stiletto`. Lowercase, underscores, no spaces.

## 7. Placeholder art (what Claude Code generates in Phases 2–3)
- Generated SVG → PNG at the real canvas size, using the real anchors.
- Body: simple silhouette with correct proportions per shape.
- Garments: flat silhouette masks with simple shading gradients and lineart, so the full fabric pipeline is exercised.
- Clearly marked with a small "PH" tag in a corner so nothing ships by accident.

## 8. Briefing illustrators (later)
Send this file, `data/bodies.json`, three garment examples rendered in-engine, the skin tone sheet, and a mood board. Commission a **style test first**: one body shape, one skin tone, one outfit (iro & buba + gele), delivered to spec. Only scale up after it drops into the engine cleanly.
