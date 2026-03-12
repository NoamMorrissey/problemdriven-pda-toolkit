# ❓ FAQ

Common questions about the PDA Toolkit.

---

**Do I need Spec Kit installed?**
No. The `/pda-ai-build` agent handles the spec generation pipeline internally. You don't need to install any additional CLI tools.

---

**Does it work without Claude Code?**
Yes. The toolkit includes agents for GitHub Copilot (`.github/prompts/`) and Cursor (`.cursor/rules/`). All three platforms encode the same behavior. Claude Code agents are the canonical source.

---

**Can I use this on an existing project?**
Yes. Clone the toolkit into your project directory, add your research evidence, and run `/pda-problem`. The agents read from and write to `docs/` — they won't touch your existing code until Phase 4, and even then, they write to `src/` and ask for your approval first.

---

**What if my problem changes mid-project?**
Go back to Phase 1. Update your research, re-run `/pda-problem`, and then cascade the changes forward: `/pda-solution`, `/pda-context`, `/pda-ai-build`. Traceability flows in one direction — always fix upstream.

---

**Is this only for web apps?**
No. The methodology is technology-agnostic. The Problem Statement, Solution Brief, and Context Specification work for any software project. The Context Specification is where you define the stack — it could be a web app, a CLI tool, a mobile app, an API, or anything else.

---

**What's the difference between Solution Brief and Context Specification?**
The Solution Brief contains **business decisions**: what to build and why. Components, success criteria, constraints, actor map. No technology mentioned. The Context Specification contains **technical decisions**: how to build it. Stack, architecture, data model, interaction patterns. In small teams one person writes both. In large teams different people write them. The separation ensures product decisions happen before technical decisions.

---

**How long does the full process take?**
It depends on how much research you have. If your evidence is ready, you can run all 4 phases in under an hour. The real investment is the research itself — talking to users, collecting evidence, understanding the problem. That happens before you open the toolkit.

---

**Can I skip phases?**
No. Each phase depends on the output of the previous one. `/pda-solution` needs an approved Problem Statement. `/pda-context` needs an approved PS and SB. `/pda-ai-build` needs all three. Skipping phases means building without validated decisions.

---

**What happens if a verification fails?**
The agent stops and tells you what failed. Read the verification report, fix the source document that caused the issue, and re-run. Don't patch downstream — always fix upstream.

---

**Where can I learn the full methodology?**
Visit [problemdriven.ai](https://problemdriven.ai) for the complete Problem-Driven AI methodology, including the 5 phases, 10 principles, anti-patterns, and detailed guidance. See [docs/METHODOLOGY.md](METHODOLOGY.md) for a summary with links.
