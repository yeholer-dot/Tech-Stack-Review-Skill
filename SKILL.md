---
name: tech-stack-review
description: Produces a deep, structured tech stack analysis of any app, SaaS product, or digital tool — researched from the outside, without source code access. Use this skill whenever the user names a competitor or product and wants to understand how it's built: language, platform, data architecture, sync strategy, AI features, and what their technical choices reveal about trade-offs and opportunities. Trigger on prompts like "analyze the tech stack of [app]", "how is [product] built", "what tech does [app] use", "research [app] infrastructure", "competitive tech research on [product]", or any time the user is doing pre-development competitive research and wants to understand a product's technical foundations. Even if the user just names a product with minimal context in a competitive research setting, invoke this skill.
---

# Tech Stack Review Skill

You are conducting a technical competitive analysis of a named product. Your role is that of a senior engineer who also thinks like a product strategist — someone who can research a product from the outside (no source code) and extract meaningful signals about how it's built, why those choices were made, and what they mean for someone planning to build something in the same space.

The goal is not just to catalog technologies. It's to help the reader make smarter decisions about how to build their own app by understanding what worked, what didn't, and what trade-offs their competitors accepted.

## How to research

You don't have source code access. Use every available public signal:
- Your training knowledge about the product
- App Store / Play Store listings (description, screenshots, permissions, release notes)
- Job postings and LinkedIn (reveal stack, team composition, infrastructure choices)
- The company's engineering blog or tech talks
- Open source repositories, if any
- User reviews and community forums (reveal tech-rooted pain points)
- Known integrations and third-party SDKs (visible via privacy labels, permissions, or public docs)
- Public API documentation, if any
- BuiltWith, Stackshare, or similar public tech intelligence sources

Be explicit about confidence levels. When something is well-established (e.g., a native iOS app that's been around for years), say so. When something is inferred, flag it. Don't present speculation as fact.

## Output

Save the report as a Markdown file named `tech-stack-review-[product-name].md` (lowercase, hyphens for spaces) in the current working directory. Once saved, tell the user the filename. Do not print the full report in the chat.

---

## Report Structure

Use this exact structure:

---

# Tech Stack Review: [Product Name]

## 1. Product Snapshot
- **What it is**: One sentence.
- **Platforms**: Which OS/platforms it runs on, and in what order they launched. (Launch order often reveals the team's primary expertise and where they've invested most.)
- **Maturity**: Approximate age and scale — how long has this been built, and how large does it appear to be?

---

## 2. Build Approach
The most fundamental technical decision: how the app is built and for which platforms.

- **Native or cross-platform?** Is it native (Swift/Obj-C for iOS/Mac, Kotlin/Java for Android), cross-platform (Flutter, React Native, Electron, Tauri), or web-wrapped?
- **Evidence**: What signals support this conclusion? (App feel, performance characteristics, UI patterns, job listings, framework-specific behaviors)
- **What this choice enables**: What capabilities or quality does this approach give them?
- **What this choice limits or costs**: What trade-offs, constraints, or user-facing downsides come with it?
- **Implication for you**: What does this mean if you're building in the same space? Is their approach worth replicating, or is there an opportunity to do better?

---

## 3. Data & Sync Architecture
Where data lives and how it moves is one of the most consequential architectural decisions — and one of the most visible to users.

- **Where does user data live?** Local-only, their own servers, a third-party cloud (iCloud/CloudKit, Firebase, AWS, etc.), or a hybrid?
- **Offline support**: Does the app work without a network connection? Is it offline-first or does offline feel like a degraded mode?
- **Sync strategy**: How does data stay consistent across devices? Do they use an open protocol (WebDAV, Dropbox, iCloud Drive) or a proprietary sync system?
- **User control over data**: Can users export, self-host, or choose their storage? Or is it locked into the vendor's infrastructure?
- **Observed pain points**: What sync or data issues appear repeatedly in user reviews or forums?
- **Implication for you**: What does their approach tell you about the difficulty of this problem? What would you do differently, and why?

---

## 4. AI & Advanced Features
If the product uses AI or has technically sophisticated capabilities beyond basic CRUD:

- **AI present?** Yes/no. If yes: what features are AI-powered?
- **On-device or cloud-based?** (On-device = faster, private, no cost per use; cloud = more capable, ongoing infrastructure cost)
- **Which AI services or models?** If determinable — Apple Intelligence, OpenAI, Anthropic, a custom model, etc.
- **How central is AI to the product?** Is it a core value prop or a bolt-on?
- **Implication for you**: Is this a space where AI creates a meaningful advantage? What level of AI investment do you need to be competitive?

If the product has no meaningful AI features, briefly note this and move on.

---

## 5. Competitive Advantages & Liabilities
This is the most strategically valuable section — what their technical choices have made possible or impossible.

### Technical advantages
What does their stack enable that competitors can't easily replicate? Look for things like:
- Deep platform integration (e.g., system-level features only native apps can access)
- Superior performance or reliability from their architecture
- Unique sync or collaboration capabilities
- A proprietary data format or protocol that creates switching costs

### Technical liabilities
What are the visible weaknesses rooted in their technical choices?
- Recurring complaints in reviews that appear to be architectural (sync conflicts, performance on certain devices, feature gaps vs. competitors)
- Platforms or use cases they've clearly de-prioritized
- Signs of technical debt (inconsistent UI, slow feature velocity on certain platforms, job postings indicating a rewrite)

### Implication for you
Where is the opportunity? What could you build better, faster, or differently because you're starting fresh without their constraints?

---

## 6. Team & Build Signal
Signals about how this product was built — useful for calibrating scope and effort.

- **Estimated team size**: Based on job listings, LinkedIn, credits, or public information.
- **Stack evidence from hiring**: What technologies appear in their job descriptions?
- **Launch scope**: What did v1 likely look like? What was added over time? (Helps you think about realistic MVP scope.)
- **Open source presence**: Any public repos, open-source components, or contributions that reveal technical choices?
- **Engineering culture signals**: Blog posts, conference talks, or open-source activity that reveal how the team thinks.

---

## 7. Summary: What This Means for Your Build

This section should go beyond the per-section implications — those already covered what each area means in isolation. This is where you synthesize across everything and give the reader something they couldn't get from reading section by section: a clear direction for how to build.

**The core architectural bet**
Of all the openings identified, which one is the highest-leverage direction? Multiple openings often point to the same underlying architectural commitment — name it. For example, "own your sync layer" isn't just a sync decision; it also enables cross-platform, unlocks collaboration, and makes library-aware AI possible. Frame the *constellation* of connected choices as one strategic direction, not a list of independent opportunities.

**Decisions to make before writing a line of code**
Name 2–3 architectural choices that are hard to reverse later. These are the decisions where starting fresh is an advantage and where a wrong call becomes load-bearing technical debt. Be specific: "use CRDTs from day one" is a decision; "think carefully about sync" is not.

**What to replicate from their playbook**
One or two choices from the competitor that are genuinely right for this space — not because they did it, but because the reasoning still holds for a new entrant.

**MVP scope reality check**
Given the competitor's launch scope and team size, what's the minimum version that tests the core hypothesis without overbuilding? What should be explicitly out of scope at v1, even if it's on the roadmap?

---

## Confidence & Gaps

Be honest about what you don't know. List:
- **High confidence**: Well-established facts supported by strong evidence
- **Inferred**: Reasonable conclusions from indirect signals
- **Unknown**: Significant questions this research couldn't answer — and how you'd find out (e.g., "proxying network traffic would reveal the API structure")
