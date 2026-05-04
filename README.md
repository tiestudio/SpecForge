# SpecForge
*Spec-Driven Development for non-developer builders*

SpecForge helps you write production-quality specification files for AI coding agents — without knowing how to write specs or what to include.

You fill in a structured form. SpecForge turns your answers into the markdown files your AI agent needs to build your product correctly, consistently, and without guessing.

It works with Claude Code, Cursor, Kiro, Windsurf, and any other agent that reads a spec file on session boot.

---

## What's in this repo

| File | What it does |
|---|---|
| `specforge-interview-form.html` | A standalone interview form — open in any browser, no account needed. Guides you through your product in plain language and generates a ready-to-paste Claude prompt. |
| `specforge-skill.md` | A Claude skill that reads your form answers, fills in the gaps, and generates your full spec bundle as production-quality markdown files. |

They are designed to be used together, in that order.

---

## How it works

SpecForge operates in two phases that happen at different points in your build lifecycle.

### Phase 1 — Constitution (once per project)

The Constitution is three files that become the permanent memory of your project. Your AI coding agent reads them on every session boot — so it always knows your product, your stack, and your decisions, without you re-explaining anything.

| File | What it contains |
|---|---|
| `mission.md` | Product vision, target audience, problem being solved, v1 scope, explicit out-of-scope |
| `tech-stack.md` | Framework, database, auth, hosting, integrations, design direction, full database schema |
| `roadmap.md` | Sequenced feature phases with goals and checkable items — a living document updated after every feature |

You generate these once using the form and the skill. Then you upload them to a Claude Project and they're available for every future session automatically.

### Phase 2 — Feature specs (once per feature, throughout the build)

Before building each feature, you open a new chat in your Claude Project and say *"next feature"*. Claude reads your Constitution, identifies what's next on the roadmap, and runs a focused 10-minute interview. It generates three files for that feature:

| File | What it contains |
|---|---|
| `plan.md` | User flow, UI states, edge cases, task groups |
| `requirements.md` | Technical constraints, data schema, API endpoints |
| `validation.md` | Success criteria, test steps, definition of done |

You take those files into your coding agent and build. When the feature is done, you come back and say *"next feature"* again. Claude gives you an updated `roadmap.md` — replace the one in your project, and your agent's memory stays current.

**The full lifecycle:**
```
Form → Constitution → Build Phase 1
→ Spec Phase 2 → Build Phase 2
→ Spec Phase 3 → Build Phase 3 → ...
```

---

## Getting started

### Step 1 — Fill in the form

Download `specforge-interview-form.html` and open it in any browser. No internet connection required.

The form has three modes — choose the one that fits:

- **New project** — you have an idea and want to build it from scratch
- **Existing project** — you've already built something and want to add SDD discipline
- **Single feature** — you already have a Constitution and just need to spec the next feature

Work through the phases. Every question has a plain-language explanation and a concrete example. When you reach the Export screen, click **Copy prompt**.

### Step 2 — Set up a Claude Project

Go to [claude.ai/projects](https://claude.ai/projects) and click **New Project**. Name it after your product.

Upload `specforge-skill.md` to the project. This file stays there permanently — it teaches Claude how to run the interview, generate spec files, and manage the feature spec workflow across the full build lifecycle.

### Step 3 — Generate your Constitution

Open a new chat inside your Claude Project. Paste the prompt you copied from the form. Claude will:

1. Read all your answers silently
2. Identify any gaps or inconsistencies
3. Ask only the follow-up questions that are genuinely needed
4. Generate `mission.md`, `tech-stack.md`, and `roadmap.md` as drafts for your review
5. Ask which AI coding tool you use and convert the files to the right format

Review each file. Claude applies your corrections before finalising.

### Step 4 — Upload the Constitution to your Claude Project

Once all three files are approved, upload them to your Claude Project:

- `mission.md`
- `tech-stack.md`
- `roadmap.md`

These three files — alongside the skill — are now your project's permanent memory. Every new chat in this project has access to them automatically.

### Step 5 — Drop the spec into your coding agent

Place the spec file(s) in your project root based on your tool:

| Tool | File | Location |
|---|---|---|
| Claude Code | `CLAUDE.md` | Project root |
| Cursor | `project.mdc` | `.cursor/rules/` |
| Kiro | `mission.md`, `tech-stack.md`, `roadmap.md` | `.kiro/steering/` |
| Windsurf / OpenCode | `AGENTS.md` | Project root |
| Universal | `CONSTITUTION.md` | Project root |

Open your coding agent. It reads the spec on the next session boot and is immediately anchored to your product — no re-explaining, no guessing.

### Step 6 — Spec each feature before building it

When you're ready to build the next feature:

1. Open a **new chat** inside your Claude Project
2. Say: *"next feature"*
3. Claude reads your Constitution, identifies what's next on the roadmap, and runs a 10-minute spec interview
4. You get `plan.md`, `requirements.md`, `validation.md`, and an updated `roadmap.md`
5. Drop the feature files into your project and build

Repeat from Step 6 for every feature on your roadmap.

---

## Why this works

**The spec is the memory.** AI coding agents are stateless — every new session starts blank. Without a spec, the agent has no record of your database schema, your auth approach, or the decisions you made last week. It guesses, contradicts itself, and drifts from earlier work. A Constitution loaded on session boot anchors the agent immediately — without consuming your context window with conversation history.

**Fewer rebuild cycles.** The most expensive part of vibe coding isn't the tokens. It's the 10–15 rounds of misaligned output that happen because the spec was vague. A precise spec front-loads all clarification so the agent executes correctly from the first or second pass.

**Built for non-developers.** SpecForge asks questions in plain language with concrete examples. Claude makes all technical decisions — framework, database, hosting, schema — and explains each one clearly. You make the product decisions. The spec writes itself.

---

## Supported tools

| Tool | Export format |
|---|---|
| Claude Code | `CLAUDE.md` |
| Cursor | `.cursor/rules/project.mdc` + per-feature `.mdc` files |
| Kiro (AWS) | `.kiro/steering/` + `.kiro/specs/[feature]/` |
| Windsurf | `AGENTS.md` |
| OpenCode | `AGENTS.md` |
| Universal | `CONSTITUTION.md` + `SPEC.md` |

---

## Keeping your project memory current

After each feature is built and merged:

1. Open a new chat in your Claude Project
2. Say *"next feature"*
3. Claude outputs an updated `roadmap.md` at the end of the session
4. Replace the `roadmap.md` in your Claude Project with the new version

One file to replace. Your agent always knows what's been built and what comes next.

---

## What the skill does

`specforge-skill.md` is a Claude skill following the Agent Skills open standard. Loaded into a Claude Project, it handles three situations automatically:

**Form output detected** — Claude reads your compiled form answers, identifies gaps, and goes straight to spec generation without re-asking what's already answered.

**"Next feature" said** — Claude reads the Constitution, identifies the next roadmap item, runs the feature spec interview, and outputs the three spec files plus an updated roadmap.

**Cold start** — if neither a form output nor a Constitution is present, Claude runs the full interview from scratch.

---

## Follow the build

SpecForge is early. A visual web platform is coming — template library, design direction visuals, and Claude Projects integration so you never have to manage files manually.

**[Follow the build →](https://specforge.io)**

---

## Tried it? Tell me what's broken.

Feedback on a real project is the most useful thing right now — which questions were confusing, what was missing, whether the spec files actually improved your agent's output.

**[Leave feedback →](https://specforge.io#feedback)**

---

## Licence

MIT — free to use, modify, and share.

---

*Built by [@tiestudio](https://github.com/tiestudio)*
