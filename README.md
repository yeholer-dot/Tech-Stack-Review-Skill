# tech-stack-review

A Claude Code skill that produces a deep, structured tech stack analysis of any app, SaaS product, or digital tool — researched entirely from the outside, without source code access.

Built for founders and developers doing **pre-development competitive research**: understand how your competitors are built, what trade-offs they accepted, and what that means for how you should build your own app.

## What it produces

A 7-section report covering:

1. **Product Snapshot** — platforms, maturity, scale
2. **Build Approach** — native vs. cross-platform, evidence, trade-offs
3. **Data & Sync Architecture** — where data lives, offline support, sync strategy, user pain points
4. **AI & Advanced Features** — on-device vs. cloud, which services, how central
5. **Competitive Advantages & Liabilities** — what their stack enables and what it locks them out of
6. **Team & Build Signal** — estimated team size, hiring stack signals, v1 scope, engineering culture
7. **Summary: What This Means for Your Build** — one core architectural bet, 2–3 irreversible decisions to make before coding, what to replicate, and an MVP scope reality check

Every section includes an explicit **confidence level** (high confidence / inferred / unknown) so you know what's established fact vs. reasoned inference.

## Example output

> *"The highest-leverage direction is to own your sync layer and build for portability from day one. This is not just a sync decision — it's a constellation of connected choices: owning sync enables real-time collaboration, cross-platform access, and user transparency. A portable data model enables AI tools to read the full writing corpus. These aren't three separate features. They're one architectural commitment."*
>
> — From the Ulysses analysis

## Install

```bash
npx skills add yeholer-dot/tech-stack-review@tech-stack-review
```

Or manually: copy `SKILL.md` into your `~/.claude/skills/tech-stack-review/` directory.

## Usage

Just name a product in Claude Code:

- `analyze the tech stack of Notion`
- `how is Linear built?`
- `competitive tech research on Bear`
- `what infrastructure does Craft use?`

The skill triggers automatically on competitive research prompts.

## How it researches

No source code access needed. The skill draws on:

- Training knowledge about the product
- App Store / Play Store listings, release notes, permissions
- Job postings and LinkedIn (reveal stack and team composition)
- Engineering blogs and conference talks
- User reviews and community forums (surface tech-rooted pain points)
- Public API docs and third-party SDK signals
- BuiltWith, Stackshare, and similar public sources

## What it doesn't cover

Intentionally excluded: monetization infrastructure, analytics/telemetry SDKs, and authentication implementation details — these don't inform how *you* should build your app.
