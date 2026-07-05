---
name: shipping-log
description: Use when the user wants to summarize their week's real work, draft a build-in-public update or weekly shipping log, or turn actual progress (commits, PRs, docs, decisions, wins) into a post backed by verifiable receipts
---

# Shipping log

## Overview

Turn a week of real work into an honest build-in-public update. Based on the
"Proof of Work" framing used in the Solana/Superteam ecosystem:

> Reputation = verifiable contributions x consistency x visibility.

The core rule: **every claim in the output needs a receipt in the collected
evidence.** No receipt - no claim. The goal is a track record, not marketing.

## Step 1 - collect receipts (last 7 days)

**Code layer** (run read-only commands; adapt paths to the user's machine):

```bash
# commits across active repos (ask the user for their projects root on first run)
for g in <projects-root>/*/.git; do r=${g%/.git}; n=$(git -C "$r" log --oneline --since='7 days ago' --all 2>/dev/null | wc -l | tr -d ' '); [ "$n" -gt 0 ] && echo "== $(basename $r) ($n commits)" && git -C "$r" log --since='7 days ago' --format='%h %s' --all | head -20; done

# merged PRs, if the gh CLI is available
gh pr list --repo <owner>/<repo> --state merged --limit 15 --json number,title,mergedAt

# docs, decision records, plans changed this week
find <projects-root>/*/docs -name "*.md" -mtime -7 2>/dev/null
```

**Founder layer** - git does not capture this, so ALWAYS ask the user:

- **wins**: programs or communities joined, grants applied/received, features and
  mentions by others, partnerships, launches, notable intros
- **decided**: bets started or dropped this week - the decision plus one line of why
- **learned**: one insight from users, research, or competitors worth quoting

On first run also ask: which projects are public-facing, and which are private or
client work. Remember the answer if the agent has persistent memory.

## Step 2 - filter

- Private/client work never appears in the public draft
- Security fixes: describe user impact, never the mechanics of the hole
- "shipped" means merged AND live; anything else is labeled honestly
  ("built, waiting on review")
- Numbers come only from collected evidence - never from memory, never invented
- Strategy stays private: share decisions and lessons, not roadmaps

## Thin week fallback - blitz interview

If collected activity is thin (few commits, nothing merged), do NOT pad or
inflate. Run a quick interview instead, one question at a time:

1. what did you actually spend the week on? (client work, thinking, life - all valid)
2. any conversation, decision, or dead end worth sharing?
3. what did you try that did not work?
4. what is blocking you right now?
5. what are you going into next week with?

An honest "slow week, here is what i am wrestling with" post builds more trust
than a padded changelog.

## Step 3 - output (always both parts, in English)

1. **Private summary** for the user: everything, including private work and
   pending reminders.
2. **Public post draft**: shipped work, wins if any, a decided/learned line,
   one honest "hard part" line, one "next" line. Note what was left out and why.

## Voice defaults (user's own style always wins)

- on first run, ask the user for 1-2 of their own past posts and match THAT
  voice - the goal is the user sounding like themselves, not like this skill
- plain words, short paragraphs - a message to a peer, not a landing page
- small honest numbers beat pathos; the hard part makes the wins credible
- no buzzwords, no "game-changer", no unexplained "building in public"
- suggest posting links in the first reply and attaching one clean screenshot

## Write like a person, not like a model

AI-drafted posts share tells that make every author sound identical. Avoid:

- contrast constructions: "X, not Y", "it's not about X, it's about Y"
- the rule of three ("fast, honest, and simple")
- every bullet opening with the same part of speech
- the same closing line every week
- em dashes and stacked semicolons

Vary the post's shape week to week: a plain two-paragraph story, a short list,
a single number with context. If two consecutive weeks look structurally
identical, redraft one of them.

## Cadence

Weekly, same day each week. Consistency is the multiplier in the reputation
equation - a modest log that ships every week beats a brilliant one that stops.

## Security

This skill only reads local git history and files, and asks the user questions.
It makes no network calls except optional `gh` reads, uploads nothing, and never
posts anywhere - the user reviews every draft and posts it themselves.
