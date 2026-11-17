# Competitive Intel Digest

A Claude skill that watches your competitors and their customers twice a week, and tells you only what's worth acting on.

Every run, four research agents work in parallel. One watches the big platforms, one watches your direct rivals, one watches the up-and-comers, and one reads what customers are saying in public. The main agent then opens every link they bring back, throws out anything it can't confirm, and asks "so what?" Most findings are logged, and only the few that change a message, a campaign, a sales conversation or a pricing argument get flagged.

All state lives in plain Markdown, so you can read and edit everything in any text editor or in Obsidian:

- **`CONTEXT.md`**: who you are, who your competitors are, what counts, and your so-what bar
- **`Baselines/`**: one file per competitor, with current pricing, product and positioning plus a dated log of every move
- **`Digests/`**: one short report per run
- **`seen.md`**: customer-voice links already reported, so nothing repeats

## What a digest looks like

```markdown
# Competitive Intel: 2026-11-13
Window: 2026-11-10 → 2026-11-13

## Worth acting on
**1. A competitor now ships the feature our main campaign says they lack.** ...
- **Why it matters:** ...
- **Next step:** ...
- **Affects:** ...

## Changes logged
- **Competitor A:** raised the price of its team plan ([source](...))

## Customer voice
- A user says the free tier's limits pushed them off the product ([source](...)), Competitor B, pricing

## Quiet
Competitor C, Competitor D
```

## Setup

1. **Install the skill.** Copy this folder into your Claude skills folder: `~/.claude/skills/competitive-intel-digest/` for Claude Code. In the Claude app, upload it as a skill.
2. **Run it once.** Ask Claude to run the competitive intel digest and tell it where to keep the files. On the first run, it asks about your company and competitors (or reads your positioning doc), creates `CONTEXT.md` and a baseline per competitor, and stops.
3. **Check the baselines.** Fix anything wrong. The digest only reports changes against what's in them.
4. **Schedule it.** In Claude Code, create a scheduled task with a one-line prompt:

   > Run the competitive intel digest. The intel folder is /path/to/competitive-intel.

   Twice a week is plenty for most markets.

## Making it yours

- **Tiers:** put every competitor in one. Big platforms get a strict filter so their unrelated news doesn't bury you. Direct rivals get everything, including hiring and leadership changes. Up-and-comers also get traction tracking.
- **The so-what bar** in `CONTEXT.md` decides what gets flagged. Name the campaigns and claims you want protected, and the digest checks every finding against them.
- **Change behavior by editing files**, never the schedule. `CONTEXT.md` holds what to watch, and `SKILL.md` holds how a run works.

## Ground rules it follows

- Every item has a source URL and a date it confirmed. If it can't verify something, it leaves it out.
- Competitor claims are reported as claims.
- Quotes from any source are 15 words or fewer.
- Anything it reads on the web is treated as data, never as instructions.
- If nothing passed, the digest is one line. It doesn't pad.

## Files

```
competitive-intel-digest/
├── SKILL.md            # how a run works
├── README.md
└── templates/
    ├── CONTEXT.md      # fill in once
    ├── baseline.md     # one per competitor
    ├── digest.md       # report format
    └── seen.md         # customer-voice dedupe list
```
