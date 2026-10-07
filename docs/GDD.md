# after-party: Lagos Style Stories — Game Design Document

Version 0.1 · Owner: Bronze · Status: pre-production

## 1. Vision

after-party is not "a Nigerian skin on a dress-up game." It is a fashion life-sim where the outfit is the engine of the story. Nigerian fashion is social, dramatic and funny: the aso-ebi group chat, the tailor who is "on his way", the aunty who inspects you at the gate, the money raining down on the dance floor. The game captures that feeling, and every look the player builds causes something to happen.

**Pitch:** *You just moved to Lagos with ₦50,000 and a dream. Can you become the city's next fashion icon?*

**Inspirations:** Covet Fashion (styling challenges), Episode/Choices (story and choices), The Sims (life, home, relationships), Nigerian pop culture (after-party, Nollywood energy, Afrobeats, social media banter).

**Platforms:** Web first (mobile browser, portrait), then iOS/Android via Capacitor.

**Audience:** Nigerian players at home, the diaspora (UK, US, Canada), and fashion-game players worldwide who want something fresh. Primary: 16–35.

## 2. What makes it stand out

1. **Outfits cause consequences.** Overdress for brunch and your friend says you're doing too much; outshine the bride and the aunties will talk; nail the aso-ebi and you meet an influencer.
2. **Real Nigerian textiles, swappable on any garment.** Any fabric on any style: Ankara, aso-oke, adire, george, lace, akwete, brocade. Plus a procedural pattern engine so the fabric library is effectively infinite, and players design their own.
3. **Dark skin rendered beautifully.** A first-class skin system with warm, accurate shading across a wide range of Nigerian complexions. Most fashion games get this wrong; we make it a headline.
4. **Men's fashion treated seriously.** Agbada, babban riga, kaftan, senator, atiku, plus streetwear.
5. **Systems only Nigerians would invent:** the unreliable tailor, market haggling, the gele minigame, money spray, the aunty panel.
6. **Humour with heart.** Recurring characters players love (and love to hate), voiced in Pidgin and local languages.
7. **Built to be shared.** Photo mode and NaijaGram turn every look into a screenshot.
8. **Real designer drops.** Nigerian designers release collections as in-game items. BRØNZE heels are the launch brand.

## 3. Core gameplay loop

```
Explore / get invited  →  Receive challenge (brief, budget, deadline)
        ↓
Source: wardrobe · market (haggle) · shop · tailor (sew fabric into a style)
        ↓
Style: outfit · gele/headwear · hair · makeup · accessories
        ↓
Photo mode (optional)  →  Attend event
        ↓
Judged by the panel  →  Money spray + dance  →  Dialogue choices
        ↓
Earn Naira + Influence · relationships shift · story advances
        ↓
Unlock clothes, locations, designers, NPCs  →  repeat
```

**Session target:** one event in 5–10 minutes. **Daily hook:** NaijaGram trend, a random event, a tailor delivery.

## 4. Time and calendar

The game runs in **days**, each with Morning / Afternoon / Evening slots. Actions cost slots (market trip = 1 slot, event = 1 evening). Events are scheduled on the calendar with deadlines, which is what makes the tailor system bite: order your outfit too late and you're wearing something from your wardrobe. Real-time is not used for core progression (no "wait 8 hours" walls).

## 5. Systems

### 5.1 Character creation
- Presentation: woman / man (more later).
- **Skin:** 12 tones from deepest to light brown with proper undertones (see ART_SPEC 3).
- **Body shapes:** MVP women: slim, mid, curvy; men: slim, broad. More in later updates.
- Face presets plus adjustable features; tribal marks as an optional, respectfully handled cosmetic choice (pending cultural review).
- Name, home state of origin (affects some dialogue and a few unlockables; never locks the player out of any culture's clothing).

### 5.2 Wardrobe and items
Every item has tags used by scoring:

| Tag | Values |
|---|---|
| `category` | top, bottom, dress, wrapper, outerwear, agbada, kaftan, shoes, bag, headwear, jewellery, hair accessory, eyewear, fan |
| `formality` | 1 casual → 5 ceremonial |
| `occasions` | wedding_trad, wedding_white, church, brunch, party, club, corporate, interview, festival, casual, date |
| `cultures` | yoruba, igbo, hausa_fulani, edo, efik_ibibio, ijaw, pan_nigerian, diaspora, global |
| `modesty` | 1–5 |
| `drama` | 1–5 (how much it "does too much") |
| `price`, `rarity`, `designerId?` | |
| `fabricSlot` | whether a fabric can be applied, and which regions (body, trim, sleeves) |

Categories at launch: traditional (iro & buba, gele, aso-oke sets, george wrappers, agbada, babban riga, kaftans, senator, atiku, Ankara styles), modern Nigerian (Lagos streetwear, corporate chic, brunch, party, clubwear, resortwear, airport looks, Afrobeats style), accessories (gele, coral beads, gold, bags, fans, watches, chains, shoes, sneakers, heels).

The wardrobe is a **room**, not a grid: clothes on rails, shoes on shelves (grid view available as a toggle for speed).

### 5.3 Fabric engine (signature)
- Garments are fabric-agnostic: any compatible fabric fills any garment.
- Fabric types (see `data/fabrics.json`) carry texture behaviour: sheen (aso-oke catches light), weave texture, lace transparency, print scale.
- **Procedural pattern generator:** motif library (circles, cowries, fans, birds, geometric, adire-style resist motifs) × palette × layout × seed. A fabric is saved as `{ motifId, paletteId, layout, seed }`.
- **Adire studio minigame:** fold/tie/apply starch-resist, dip in indigo, reveal. The result is a fabric you own, can sew, and can sell or gift.

### 5.4 Sourcing: market, shops, tailor
**Market haggling (Balogun in Lagos; Kantin Kwari in Kano later).** Traders have personalities (`firmness`, `mood`, `likes`). The player picks moves: *Greet properly*, *Compliment*, *Counter-offer*, *Walk away*, *"Last price?"*, *Buy now*. Good manners and timing lower the price; rudeness raises it. A relationship meter with each trader gives regular-customer discounts. Logic is a pure function in `systems/haggle.ts`.

**Boutiques** sell ready-to-wear and designer pieces at fixed prices.

**Tailors** turn fabric + style into a garment. Each tailor has `skill`, `reliability`, `speed`, `price`, `specialties`. Outcomes on delivery:
- **Perfect** — as ordered.
- **Late** — "I dey come!" Arrives after the deadline unless the player pays a rush fee or visits the shop to "follow up".
- **Freestyle** — the tailor "improved" the style. Sometimes better, sometimes a disaster.
- **Masterpiece** — rare; bonus score and a NaijaGram moment.
Reveal is dramatic: the bag opens, a beat, the garment drops. Players will recognise this pain and laugh.

### 5.5 Styling minigames
- **Gele tying (signature):** a gesture/timing sequence of fold, wrap, pleat, tuck, set. Precision shapes the final silhouette (fan, rose, double-layer). A bad gele collapses comically mid-event if the player rushes. Styles unlock with practice.
- **Makeup:** full layered system (base, contour, highlight, brows, eyes, lashes, lips) tuned for dark skin, with savable presets ("Lagos Soft Glam"). Bridal, soft glam, editorial, natural, party glam.
- **Hair:** knotless braids, Fulani braids, cornrows, locs, afro, Bantu knots, wigs, bobs, pixie, ponytails, puffs, with length, colour, highlights and cuffs/beads.
- **Lalle/henna** (Northern chapters): tracing minigame on hands and feet.

### 5.6 Challenges and scoring
A challenge defines: occasion, theme text, budget, deadline, required/forbidden tags, target ranges (formality, modesty, drama), culture context, special rules, and judges. See `data/challenges.json`.

**Player-facing categories** (what the player sees, as judge reactions plus a short breakdown): **Style · Cultural Fit · Colour Harmony · Accessories · Event Appropriateness · Creativity**. Never a bare star rating.

**Under the hood, score (0–100)** = weighted sum of:
- **Occasion fit** — formality and occasion tags vs target.
- **Theme fit** — tag matches to the theme keywords.
- **Coordination** — colour harmony across items (fabric palette vs accessories), gele/fabric match.
- **Cultural appropriateness** — e.g. aso-oke and gele at a Yoruba trad, coral at an Edo/Igbo trad; respectful modesty at Northern events.
- **Budget** — penalty for overspend; bonus for "rich look, small money".
- **Special rules** — e.g. `dont_outshine_bride`: drama above a threshold *loses* points; `aso_ebi_match`: must use the group fabric but style it uniquely.
Weights per challenge live in data. Logic in `systems/scoring.ts`, fully unit-tested.

**The judge panel** turns the score breakdown into personality. Each judge reacts to specific sub-scores with lines from data:
- **Aunty Sade** (tradition, modesty, "who is your father?")
- **Zara** (influencer: trendiness, drama, photo-worthiness)
- **Uncle Bayo** (decency and event appropriateness: "At least you dressed properly.")
- **Dami** (rival: always finds a flaw, grudging respect on high scores)

Judge focus: Aunty Sade → Cultural Fit, Accessories, gele quality · Uncle Bayo → Event Appropriateness, modesty · Zara → Style, Creativity · Dami → Colour Harmony (and whatever is weakest).
Comments never repeat within a session.

### 5.7 The event scene
Arrival walk-in (the reveal), judges' reactions, **money spray** (naira notes rain proportional to score; tap to collect), optional **dance rhythm game** (higher score = more spray and Influence), then a dialogue moment with choices that affect relationships and story.

### 5.8 Economy
- **Naira (₦)** — earned from styling jobs, events, sprays, selling clothes/fabrics. Spent on fabric, tailors, items, rent, upgrades.
- **Influence (✨)** — earned from scores, NaijaGram, competitions, networking. Unlocks events, celebrities, designers, locations. Never purchasable.
- **Premium currency** — post-launch only, cosmetic only. Rules: no loot boxes, no energy walls, no pay-to-win scoring. Designer drops are direct purchase with clear prices.
- **XP and levels** — Level 1 *New Stylist*, Level 2 *Known Around Town*, Level 3 *Rising Fashion Name* (more later). Levels unlock items, tailors and events.
- **Rent** is due every 7 in-game days (Milestone 2+); a gentle sink that pushes the player to take styling jobs.

### 5.9 NaijaGram (in-game social)
A phone app with a feed. NPCs post (scripted and systemic), react to the player's looks, and start trends ("this week: emerald and gold"). Players post photo-mode shots; follower count feeds Influence. Gossip threads appear ("Did you see what Amaka wore?") with choices: defend, ignore, comment, investigate. Gossip is always about fictional characters.

### 5.10 Photo mode
Pose, expression, camera angle, background (location sets), lighting, filter. Export a PNG with a subtle after-party watermark, plus share to device.

### 5.11 Relationships and story
Each key NPC has `friendship` and `rivalry` meters plus flags. Dialogue is data-driven (node graph with conditions on state and effects on meters/flags). NPCs **remember**: lines can reference what you wore last time (stored outfit history), e.g. Amaka: *"Gold again? Chai, you and gold ehn."*

### 5.12 Random events
Triggered by calendar and conditions: *"Your friend's trad is TOMORROW"* (rush challenge, 10-minute timer); *"Dami says you copied her style"* (choice event); *"Tailor has your outfit — but he cut it short"*.

### 5.13 Home (post-MVP)
Start in a self-contained in Yaba; upgrade to a Lekki flat, then an Ikoyi penthouse. Decorate rooms; the wardrobe room grows physically.

### 5.14 Competitions (post-MVP, online)
Weekly themes (Best Trad Look, Best Budget Outfit, Detty December), player voting, leaderboards, cosmetic rewards and titles.

### 5.15 AI features (post-MVP, server-side)
- **AI Stylist:** describe the vibe ("expensive but not trying too hard") and it assembles a look from the player's wardrobe and explains it.
- **Living NPCs:** major NPCs get generated reactions grounded in their personality card and the player's history, constrained by the game's tone rules.
Both run through a backend proxy; scripted fallbacks always exist.

## 6. Characters
See `data/npcs.json` for full cards. Core cast:
- **Amaka** — the bestie. Igbo, fashion-obsessed, loyal, loud.
- **Tolu** — aspiring Afrobeats artist; future celebrity client.
- **Zara** — influencer and judge; trends live and die by her.
- **Chinedu** — knows everybody, gets you into places, comic relief.
- **Aunty Sade** — neighbourhood gossip and tradition judge.
- **Uncle Bayo** — family friend at every party; judges decency and appropriateness.
- **Mrs. Okafor** — wealthy event organiser; the big-money client.
- **Dami** — the rival stylist.
- **Iya Bisi** — Balogun fabric trader and haggling boss.
- **Tailors:** Baba Tee (cheap, "on his way"), Kunle Cuts (pricey, perfect, punctual), Hauwa Stitches (Kano-trained embroidery genius, busy).
- **Mummy** — the player's mother, by phone: *"Fashion will not pay your rent."*
- **Fictional celebrities:** Kiki Blaze (Afrobeats star), Maya Banks (actress), DJ Lush, Tunde Gold (footballer). Never real people.

## 7. World and chapters

| Chapter | Place | Signature events | Status |
|---|---|---|---|
| 1. Welcome to Lagos | Yaba, Balogun, event hall | Amaka's cousin's Yoruba trad (aso-ebi), brunch, first client | **MVP** |
| 2. Island Life | Lekki, Victoria Island | Rooftop party, Lagos Fashion Week, celebrity birthday | v1.1 |
| 3. Igba Nkwu | Enugu / Anambra | Igbo traditional wedding, chief's title | v1.2 |
| 4. Kano Gold | Kano | Hausa wedding (kamu, sadaki), Kantin Kwari market, Kofar Mata dye pits, the Durbar | v1.3 |
| 5. Capital Moves | Abuja | Corporate gala, embassy party | v1.4 |
| 6. Detty December | Lagos | Seasonal live event every December | Annual |
| 7. London Calling | Peckham, London | Diaspora wedding, UK fashion week | v2 |
| Also | Calabar Carnival, Eyo Festival, Ibadan | Festival specials | Events |

## 8. Audio
Original music inspired by Nigerian sounds (no licensed hits at launch): Afrobeats/Afropop at parties, talking drum and percussion at trad weddings, Afro-R&B in restaurants, Afro-house on the runway, fuji/highlife touches, Hausa instrumentation in the North. Voiced barks for judges and key NPCs.

## 9. Monetisation (post-launch)
Premium (one-time unlock of all chapters) or free-to-play with cosmetic designer drops and chapter passes. Decision deferred until the vertical slice is playtested. Ethics rules in 5.8 are non-negotiable.

## 10. MVP scope (two milestones)

**Milestone 1 — The after-party Loop (follow `docs/BRIEF.md`).** One polished 5–10 minute playthrough, replayable with different strategies: short intro (Mummy sceptical, Amaka encouraging) → character select/create → Balogun market (browse, inspect, haggle) → choose one of 3 tailors (simulated time, funny uncertainty) → style outfit, accessories, hair, makeup → gele minigame → the after-party (alive venue) → 4 judges react → money spray → 20–30s dance → photo mode and Save Look → rewards (money, reputation, XP, a new item) toward 3 levels. Content: 15–25 fabrics, a small high-quality wardrobe, 5 locations. Success = BRIEF section 28.

**Milestone 2 — Chapter 1.** Calendar and rent, more challenges from `data/challenges.json`, NaijaGram, random events, rival arc, Mrs. Okafor finale.

## 11. Tone rules
Warm, witty, affectionate. Laugh *with* Nigerian culture, never *at* it. No ethnic stereotypes as jokes. No real people. Every culture's clothing is presented with its name, region and a short "Culture Spotlight" note when first unlocked.
