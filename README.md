# after-party — Starter Kit (read this first)

Working title: **after-party: Lagos Style Stories** (rename any time; the name lives in one place, `src/config/game.ts`, once scaffolded).

This folder is everything Claude Code needs to build the game with you, system by system. You don't paste the whole vision in one prompt; you give Claude Code a single source of truth (these docs) and walk it through phases.

## What's in here

| File | What it's for |
|---|---|
| `CLAUDE.md` | Claude Code reads this automatically every session. Stack, architecture rules, conventions. Keep it updated. |
| `docs/GDD.md` | The Game Design Document: the merged vision (story, systems, characters, economy, scoring, locations). |
| `docs/ART_SPEC.md` | Art direction plus the exact asset spec artists (and placeholder art) must follow. |
| `docs/ROADMAP.md` | The build plan: 14 phases, each with a copy-paste prompt and a "done when" checklist. |
| `data/fabrics.json` | Seed content: Nigerian textiles with cultural notes. |
| `data/npcs.json` | Seed content: the character cast. |
| `data/challenges.json` | Seed content: the first fashion challenges. |

## Setup (about 15 minutes)

1. **Install Node.js LTS** (v20 or newer) from nodejs.org. Check with `node -v`.
2. **Install Git** and create a GitHub repo (private) called `after-party`.
3. **Create the project folder**, copy this whole starter kit into it, and open it in Cursor.
4. **Install Claude Code.** The current official instructions are at https://docs.claude.com/en/docs/claude-code/overview. The npm route is `npm install -g @anthropic-ai/claude-code`. Then, in Cursor's terminal, run `claude` from the project folder and log in.
5. Initialise git and make your first commit:
   ```bash
   git init && git add . && git commit -m "chore: starter kit docs"
   ```
6. Open `docs/ROADMAP.md`, copy the **Phase 0** prompt, paste it into Claude Code. Go.

## How to work with Claude Code on this project

- **One phase per session.** Run `/clear` between phases so context stays clean; `CLAUDE.md` and the docs carry the memory.
- **Ask for a plan first on big phases.** Start the prompt with "Plan first, don't write code yet." Review the plan, push back, then say "go".
- **Commit after every phase** that passes its "done when" checklist. If a phase goes sideways, `git reset --hard` is your undo button.
- **Run the game constantly.** `npm run dev`, open the browser, actually play it. Tell Claude Code exactly what looks or feels wrong ("the gele snaps too fast", "the judge comment repeats") rather than "make it better".
- **Keep the docs alive.** When you change a design decision, have Claude Code update `GDD.md` in the same commit. The docs are the brain; the code follows them.
- **Content is data.** New outfits, challenges, NPC lines and fabrics go in `data/*.json`, never hardcoded. This is what lets the game grow to hundreds of items without code changes.

## The art reality (read before you spend money)

Claude Code builds the engine, systems, minigames, UI, scoring, story logic and procedural fabrics. It cannot produce the final illustrated characters and garments at the quality you want. The plan in `ROADMAP.md` handles this deliberately: you build every system on **placeholder art that follows the real asset spec**, prove the game is fun, then commission illustrators (ideally Nigerian) to deliver final art to `docs/ART_SPEC.md`. Because placeholders and final art share one spec, real art drops straight in.

## Cultural accuracy

Everything cultural in these docs (fabric notes, ceremony details, Pidgin and Hausa/Yoruba/Igbo lines) is a starting draft. Before launch, get each region's content reviewed by someone from that culture. Lines needing review are marked `"review": true` in the data files.
