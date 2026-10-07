# PROJECT: Nigerian Fashion & Social Game — MVP Vertical Slice

You are my senior game designer, product architect, UI/UX designer, creative director, and lead engineer.

We are building a high-quality Nigerian-themed fashion and social game.

The game should NOT feel like a generic dress-up game with African clothing added to it.

It should feel like a polished, modern game whose identity comes from Nigerian fashion, humour, culture, social life, events, characters, music, and storytelling.

The long-term vision is a Nigerian fashion/social world where players create an identity, dress their characters, attend events, meet NPCs and eventually other real players, build friendships/rivalries, earn money, unlock fashion, travel between Nigerian cities, participate in cultural events, and become influential in the fashion world.

For the FIRST MVP, however, we will build one extremely polished vertical slice.

---

# 1. CORE GAME FANTASY

The player is an aspiring Nigerian fashion stylist / fashion-forward young adult starting their journey in Lagos.

They have limited money, a small wardrobe, and a desire to become known for their fashion.

Their first major opportunity is an Owambe/traditional wedding.

The player must:

1. Visit a Nigerian market.
2. Browse and purchase fabric.
3. Negotiate with a market seller.
4. Choose a tailor.
5. Send fabric to the tailor.
6. Wait for the outfit to be prepared.
7. Style their character.
8. Complete a gele-tying mini-game.
9. Complete makeup/accessory styling.
10. Attend the Owambe.
11. Be judged by memorable Nigerian characters.
12. Receive reactions based on the outfit.
13. Receive money spray if they perform well.
14. Receive a final score/reputation reward.
15. Take a beautiful photograph of their character.
16. Share/save the final look.

The entire experience should take approximately 5–10 minutes for one complete playthrough.

The goal of the MVP is NOT to contain lots of content.

The goal is to make ONE experience feel exceptionally polished, funny, beautiful and addictive.

---

# 2. IMPORTANT PRODUCT PRINCIPLE

Do NOT build a "dress-up website."

Build a GAME.

The player should constantly feel:

- anticipation
- choice
- risk
- humour
- surprise
- reward
- progression

The player should have reasons to replay the same level with different strategies.

---

# 3. LONG-TERM VISION

Do NOT architect the MVP in a way that makes future expansion difficult.

Eventually the game should support:

## Locations

Lagos
Abuja
Kano
Ibadan
Enugu
Benin City
Calabar
Port Harcourt
Ilorin
and eventually diaspora locations such as London, Accra, Toronto, Atlanta and Dubai.

## Events

Traditional weddings
White weddings
Naming ceremonies
Birthday parties
Sunday church
Fashion shows
Lagos Fashion Week
Calabar Carnival
Durbar
Eid celebrations
Detty December
Beach parties
Bridal showers
Engagement ceremonies
Corporate events
Concerts
Nightlife
Fashion competitions

## Social systems

Player profiles
Friends
Following
Private messaging
Group chats
Fashion clubs
Fashion competitions
Voting
Leaderboards
Player-created looks
Photo sharing
Events containing multiple players

Eventually players should be able to encounter and interact with other real players.

DO NOT implement multiplayer/social chat in MVP yet.

However, create the architecture so these systems can be added later.

---

# 4. MVP LOCATION

The first MVP takes place in Lagos.

Do not attempt to build all of Nigeria yet.

Lagos is the entry point into a much larger Nigerian world.

The MVP should contain approximately:

- 1 market
- 1 tailor shop
- 1 player's small room/studio
- 1 Owambe venue
- 1 photo area

The environments should feel Nigerian without becoming caricatures.

Use authentic visual references.

---

# 5. VISUAL DIRECTION

The graphics are extremely important.

The target is:

POLISHED + BEAUTIFUL + MODERN + STYLIZED REALISM.

Do NOT create:

- generic cartoon African characters
- stereotypical "tribal" aesthetics
- low-quality clipart
- flat generic mobile-game graphics
- inconsistent AI-generated character designs

The game should feel like a premium fashion game.

Prioritize:

- beautiful skin rendering
- accurate Nigerian skin tones
- diverse facial features
- high-quality hair
- beautiful fabrics
- realistic fabric texture
- strong lighting
- expressive characters
- elegant UI
- smooth animations
- beautiful photography

The visual identity should feel sophisticated enough that players want to screenshot their characters.

---

# 6. CHARACTER SYSTEM

For MVP create ONE primary player character system with the ability to support future customization.

The architecture should support:

- skin tone
- face
- body type
- hair
- hairstyle
- makeup
- clothing
- shoes
- bags
- jewellery
- headwear
- accessories

The player should be able to see clothing layered correctly.

Do not hard-code outfits as single images if this prevents future customization.

Use a modular clothing architecture wherever technically practical.

The system must be designed so more clothing items can be added later without rewriting the entire character system.

---

# 7. MVP FASHION INVENTORY

Create a small but high-quality initial wardrobe.

Prioritize quality over quantity.

Include Nigerian-inspired:

- dresses
- skirts
- blouses
- traditional pieces
- wrappers
- lace
- aso-oke-inspired pieces
- gele
- coral/beaded jewellery
- handbags
- heels
- sandals

Also include a few modern fashion pieces.

The clothing system should support:

- item name
- category
- rarity
- price
- colour
- fabric
- cultural/style tags
- event suitability
- score modifiers where appropriate

Avoid reducing culture to simplistic numerical stereotypes.

Tags should primarily help the game understand whether an item fits an event brief.

---

# 8. THE MARKET

The market is one of the signature MVP features.

The player enters a Nigerian fabric market.

The market should feel alive.

There should be a market seller NPC with a distinct personality.

The player can:

- browse fabrics
- inspect fabric
- compare prices
- negotiate
- accept the first price
- bargain
- walk away
- return
- choose another fabric

Create a simple but fun haggling mechanic.

The player should feel like:

"I can pay this price, but maybe I can get it cheaper."

Do not make this overly complicated.

Make it intuitive and funny.

Example interaction:

SELLER:
"₦35,000."

PLAYER OPTIONS:

"That's too expensive."

"Final price?"

"I'll give you ₦25,000."

"Okay, I'll take it."

"Let me look around."

The seller should have personality and reactions.

If the player bargains badly, the seller can say something humorous.

If the player gets an excellent deal, reward them with a satisfying moment.

---

# 9. FABRIC SYSTEM

For MVP create approximately 15–25 fabrics.

Each fabric should have:

- name
- texture
- colour/pattern
- price
- rarity
- style tags

Include Nigerian-inspired textiles such as:

- Ankara
- Adire-inspired patterns
- Aso-oke-inspired patterns
- Lace
- Brocade
- George-inspired fabric

Do not falsely claim historical/cultural authenticity for generated patterns.

Where cultural terminology is used, use it accurately.

Build the system so procedural patterns can be introduced later.

---

# 10. TAILOR SYSTEM

The tailor is a major Nigerian personality mechanic.

Create 3 fictional tailors.

Each should have a personality and tradeoffs.

Example:

TAILOR 1:
Cheap
Good quality
Slow

TAILOR 2:
Expensive
Excellent quality
Fast

TAILOR 3:
Cheap
Very creative
Unpredictable

The player chooses one.

The tailor receives the selected fabric and selected outfit style.

The game should create anticipation.

The player should eventually receive the finished outfit.

Include small humorous uncertainty.

Example:

"Your tailor says your outfit is almost ready."

Then:

"Your tailor is on his way."

Then:

"Your tailor has sent a message."

The experience should be funny rather than frustrating.

Do NOT make the MVP dependent on real-time waiting.

Use simulated time.

The player should never be forced to wait hours for the game to continue.

---

# 11. OUTFIT CREATION

The player selects:

- outfit
- fabric
- colour
- shoes
- bag
- jewellery
- gele
- hairstyle
- makeup

The game calculates compatibility with the event brief.

Do NOT make the scoring purely numerical.

Create an understandable fashion scoring system.

For example:

STYLE
Cultural Fit
Colour Harmony
Accessories
Event Appropriateness
Creativity

The player should receive understandable feedback.

---

# 12. GELE MINI-GAME

THIS IS ONE OF THE SIGNATURE FEATURES.

The gele mini-game should be fun enough that players want to replay it.

The player must perform simple actions such as:

- fold
- pleat
- align
- wrap
- tuck
- tighten

The MVP can use mouse/touch gestures or simple timing mechanics depending on platform.

Create 3 outcomes:

PERFECT GELE
Beautiful, symmetrical, impressive.

GOOD GELE
Looks good with minor imperfections.

DISASTER GELE
Funny, lopsided, collapsed or badly positioned.

A bad result should be funny rather than punishing.

Show the character reacting.

Potential reactions:

"Oh no."

"Please."

"Not today."

"Who tied this thing?"

Do not use copyrighted or real celebrity voices.

Use original dialogue.

---

# 13. MAKEUP / BEAUTY

Create a lightweight MVP beauty system.

Allow:

- foundation/skin finish
- blush
- eye makeup
- lashes
- lipstick
- highlight

The system must render beautifully across dark Nigerian skin tones.

Avoid using generic beauty presets that make all characters look the same.

---

# 14. OMWAMBE EVENT

This is the payoff.

The player arrives at the event.

Create a beautiful Nigerian event environment.

There should be:

- guests
- music
- dancing
- decorated tables
- photographer
- fashion-conscious guests
- food/drinks
- stage/celebration area

The environment should feel alive.

---

# 15. JUDGING SYSTEM

Create 4 judging characters.

Example archetypes:

THE AUNTY

Very observant.
Opinionated.
Funny.

THE FASHION BLOGGER

Cares about style and originality.

THE UNCLE

Cares about decency and appropriateness.

THE RIVAL STYLIST

Always has something negative to say.

Each judge should have:

- personality
- scoring preferences
- dialogue
- reactions

Do NOT simply show:

⭐⭐⭐⭐⭐

Instead show character reactions.

For example:

AUNTY:

"Hmm."

"Okay ooo."

"Who styled you?"

FASHION BLOGGER:

"Now THIS is a look."

RIVAL:

"Interesting choice."

UNCLE:

"At least she dressed properly."

The reactions should depend on what the player actually wore.

---

# 16. MONEY SPRAY

This is the major reward animation.

When the player performs well:

Guests begin spraying money.

Money should visually rain/fly around the character.

Create a satisfying animation.

The player earns in-game currency.

Better fashion + better gele + better event performance + better dance performance = larger reward.

Do NOT use real-world financial value.

This is purely in-game currency.

---

# 17. DANCE MOMENT

After judging, create a short optional dance mini-game.

The player responds to rhythm/timing prompts.

A good performance increases the final reward.

A bad performance should be funny.

This should be quick.

Approximately 20–30 seconds.

---

# 18. PHOTO MODE

After the event, allow the player to create a fashion photograph.

Allow:

- pose
- camera angle
- zoom
- background
- simple lighting/filter
- character expression

The result should look beautiful.

This is important because the game should naturally encourage players to share their looks.

Create a "Save Look" function.

Architect the system so social sharing can be added later.

---

# 19. PROGRESSION

For the MVP create a simple progression system.

Player starts with:

- small amount of money
- basic wardrobe
- low reputation

Completing the event rewards:

- money
- reputation
- new item
- XP

Create approximately 3 progression milestones.

Example:

LEVEL 1
New Stylist

LEVEL 2
Known Around Town

LEVEL 3
Rising Fashion Name

Do not overbuild progression yet.

---

# 20. STORY

Create a short introduction.

The player is trying to prove that fashion can become a real career.

A family member is skeptical.

A friend encourages the player.

The first Owambe becomes the player's first opportunity.

Create approximately 2–3 short story scenes.

Keep them funny and fast.

Avoid long dialogue dumps.

---

# 21. HUMOUR

Humour is a core feature.

Use Nigerian conversational energy.

The game can use English, light Pidgin, and occasional culturally appropriate expressions.

Do not overuse slang.

Do not turn characters into stereotypes.

Humour should come from:

- personalities
- situations
- fashion disasters
- tailoring experiences
- market bargaining
- social observations

---

# 22. CULTURAL AUTHENTICITY

Cultural accuracy is extremely important.

Do not invent cultural rules and present them as fact.

Where specific cultural ceremonies, clothing, terminology or regional traditions are represented, structure the content so it can be reviewed by Nigerian cultural consultants later.

The game should eventually represent multiple Nigerian cultures respectfully.

The MVP can focus on a Lagos/Yoruba-influenced Owambe setting while clearly treating it as ONE part of Nigeria rather than "Nigerian culture = Yoruba/Lagos."

---

# 23. SOCIAL / MULTIPLAYER FUTURE

DO NOT implement multiplayer in MVP.

But architect the code/data model so future versions can support:

- user accounts
- profiles
- avatars
- friends
- following
- private chat
- group chat
- fashion clubs
- public fashion posts
- likes
- comments
- competitions
- player voting
- multiplayer events

The wardrobe/item system should have stable IDs.

Player profiles should be separable from the character rendering system.

Avoid creating architecture that assumes only one player will ever exist.

---

# 24. FUTURE SOCIAL WORLD

The long-term vision is a persistent social fashion world.

Players could eventually:

- meet other players
- attend virtual Owambe events
- chat
- form friend groups
- compete in fashion battles
- visit each other's spaces
- exchange/sell player-created fabrics
- create fashion clubs
- participate in seasonal events
- build reputations

This should influence architecture, but MUST NOT cause MVP scope creep.

---

# 25. TECHNICAL APPROACH

Before writing substantial code:

1. Analyze the requirements.
2. Recommend the best technical stack for this MVP.
3. Explain why.
4. Define the project architecture.
5. Define the data model.
6. Define the component structure.
7. Define how clothing layers will work.
8. Define how future multiplayer/social systems could be introduced.
9. Define how assets will be organized.
10. Define how content can be added without rewriting core systems.

Prefer a web-based MVP unless there is a strong technical reason not to.

Prioritize:

- excellent performance
- responsive design
- desktop support
- mobile-friendly architecture
- clean component structure
- maintainability

---

# 26. DEVELOPMENT PHILOSOPHY

Do not try to build everything at once.

Build in vertical slices.

PHASE 1
Project foundation.

PHASE 2
Character rendering.

PHASE 3
Wardrobe system.

PHASE 4
Market.

PHASE 5
Tailor.

PHASE 6
Gele mini-game.

PHASE 7
Owambe event.

PHASE 8
Judging.

PHASE 9
Money spray.

PHASE 10
Photo mode.

PHASE 11
Progression.

PHASE 12
Polish.

At the end of each phase, the game should remain runnable.

Do not destroy working systems while adding new features.

---

# 27. IMPORTANT ART ASSET PRINCIPLE

Do not solve difficult art problems by repeatedly generating random AI images that have inconsistent characters.

We need a consistent visual system.

If temporary placeholder assets are necessary, clearly label them.

Design the asset pipeline so professionally illustrated/generated assets can replace placeholders later without changing game logic.

Keep:

GAME LOGIC

separate from

VISUAL ASSETS.

---

# 28. MVP SUCCESS CRITERIA

The MVP is successful if a new player can:

1. Start the game.
2. Create/select their character.
3. Enter the market.
4. Buy fabric.
5. Negotiate.
6. Choose a tailor.
7. Create an outfit.
8. Complete the gele mini-game.
9. Attend the Owambe.
10. Receive funny character reactions.
11. Earn money spray.
12. Complete a dance moment.
13. Take a beautiful photo.
14. Want to play again with a different outfit.

The MVP should feel like a REAL GAME, not a technical demo.

---

# 29. WHAT I DO NOT WANT

Do NOT:

- build dozens of unfinished systems
- create generic African stereotypes
- use poor-quality placeholder UI everywhere
- make the game feel like a CRUD application
- create a boring inventory screen and call it a game
- overcomplicate the first version
- implement multiplayer prematurely
- implement payments prematurely
- use real celebrities
- use copyrighted music
- copy existing games
- copy The Sims
- copy Covet Fashion
- copy existing Nigerian games

Take inspiration from successful games, but develop an original identity.

---

# 30. YOUR FIRST RESPONSE

DO NOT START CODING YET.

First give me:

A. Your recommended technical stack.

B. A proposed project architecture.

C. A proposed folder structure.

D. The data model for:
   - player
   - character
   - clothing
   - fabric
   - tailor
   - event
   - judge
   - currency
   - progression

E. The proposed game state flow.

F. The proposed MVP screen/page flow.

G. The art asset requirements.

H. The animation requirements.

I. The biggest technical risks.

J. The biggest product/gameplay risks.

K. What should be built first.

L. What should explicitly NOT be built yet.

M. A recommended development sequence.

Then wait for my approval before implementing.

Remember:

WE ARE NOT BUILDING A GENERIC DRESS-UP APP.

WE ARE BUILDING THE FIRST VERTICAL SLICE OF A POTENTIAL NIGERIAN FASHION + SOCIAL WORLD.

The first experience needs to make someone say:

"Wait... this is actually a GAME."

And ideally:

"😂 I need to send this to my friend."