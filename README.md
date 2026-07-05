# shipping-log

An agent skill that turns your week's **actual work** - commits, merged PRs, docs,
decisions, wins - into an honest build-in-public post. No more "what did I even do
this week".

Based on the **Proof of Work** framing from the Solana/Superteam ecosystem:
reputation = verifiable contributions x consistency x visibility. The skill's core
rule: every claim in the post needs a receipt in your real activity. No receipt,
no claim.

## What you get

Ask your agent "shipping log for this week" and it produces:

1. a private summary of everything you did (including private/client work), and
2. a public post draft like this:

```
week 3 of building <project>:

- shipped X (live)
- fixed a bug that silently broke Y
- new Z ready, waiting on store review

decided: dropping A to focus on B - the data said so

hard part rn: getting people from "cool" to a first deposit

next: user interviews. more next week
```

## Install

**Claude Code / Codex / Cursor and friends (via [skills](https://skills.sh)):**

```bash
npx skills add 4oko4ow/shipping-log
```

**Manual (Claude Code):**

```bash
git clone https://github.com/4oko4ow/shipping-log
cp -r shipping-log/shipping-log ~/.claude/skills/
```

**Any other agent:** it is just markdown - paste `shipping-log/SKILL.md` into your
agent's context (or its skills/instructions folder) and ask for a weekly log.

## Usage

Once a week, same day:

> shipping log for this week

The agent scans your repos (read-only), asks about non-code wins and decisions,
and drafts the post. You review, you post.

## Security

Worth checking for any skill you install - this one is a single markdown file,
read it before installing. What it does:

- reads local git history and doc files (read-only)
- optionally reads merged PRs via the `gh` CLI
- asks you questions

What it never does: no network calls, no uploads, no auto-posting. Every draft is
reviewed and posted by you.

## Credits

Inspired by the "Proof of Work on Solana" framework popularized by Superteam.
Built by [@4oko4ow](https://x.com/4oko4ow) while building [portfi](https://portfi.fun).

## License

MIT
