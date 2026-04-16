# SpecForge
*Spec-Driven Development for non-developer builders*
 
SpecForge helps you write production-quality specification files for AI coding agents like Claude Code, Cursor, Kiro, and Windsurf — without knowing how to code or what to write.
 
You fill in a structured form. SpecForge turns your answers into the markdown files your AI agent needs to build your product correctly, consistently, and without guessing.
 
---
 
## What's in this repo
 
| File | What it is |
|---|---|
| `specforge-skill.md` | A Claude Skill that interviews you and generates your spec files |
| `specforge-interview-ui.html` | A visual form to organise your answers before running the skill |
 
They are designed to be used together, in that order.
 
---
 
## How to use it
 
### Step 1 — Fill in the form
 
Download `specforge-interview-ui.html` and open it in any browser. No internet connection required.
 
Work through the six phases:
- **Setup** — choose your project mode and target AI tool
- **Mission** — describe your product, audience, and scope
- **Tech stack** — pick your database, auth, and technical constraints
- **Roadmap** — list your v1 features and sequence them
- **Feature spec** — plan your first feature in detail
- **Export** — get your ready-to-paste first prompt
When you reach the Export screen, click **Copy first prompt**.
 
---
 
### Step 2 — Load the skill into Claude
 
You have two options:
 
**Option A — Claude Project (recommended)**
If you use [Claude Projects](https://claude.ai), add `specforge-skill.md` to your project's files. Every new chat in that project will have the skill available automatically.
 
**Option B — Paste into chat**
In a new Claude chat, paste the full contents of `specforge-skill.md` as your first message, followed by your copied prompt from the form.
 
---
 
### Step 3 — Paste your prompt and let Claude work
 
Paste the prompt you copied from the Export screen. Claude will:
 
1. Read all your form answers
2. Identify any gaps, ambiguities, or inconsistencies
3. Ask only the follow-up questions that are actually needed
4. Generate your full spec bundle as markdown files
---
 
### Step 4 — Drop the files into your project
 
Claude produces ready-to-use files formatted for your chosen AI tool:
 
| Tool | Files generated |
|---|---|
| Claude Code | `CLAUDE.md` |
| Cursor | `.cursor/rules/project.mdc` + one file per feature |
| Kiro | `.kiro/steering/mission.md`, `tech-stack.md`, `roadmap.md` + feature folders |
| Windsurf / OpenCode | `AGENTS.md` |
| Universal | `CONSTITUTION.md` + `SPEC.md` |
 
Copy the files into your project root and open your AI coding agent. It will read the spec on the next session boot.
 
---
 
## Why this works
 
AI coding agents are stateless — every new session starts with no memory of prior decisions. Without a spec, the agent guesses at your architecture, contradicts earlier choices, and requires constant re-explanation.
 
A well-structured spec loaded on session boot anchors the agent immediately. It knows your product, your stack, your constraints, and the exact feature it's implementing. The result is fewer misaligned outputs, fewer rebuild cycles, and a codebase that stays coherent across weeks of development.
 
SpecForge makes writing that spec something any builder can do — not just developers.
 
---
 
## The two-step workflow explained
 
**Why use the form first, then the skill?**
 
The form is fast — chips and text fields, no open-ended thinking required. It gets your core decisions down in one sitting and organises your thinking before the conversation starts.
 
The skill is smarter — it reads your form answers, spots what's missing, and asks targeted follow-up questions. It produces richer, more consistent spec files than the form output alone.
 
Using both together gets you the speed of the form and the quality of the skill.
 
---
 
## Supported AI tools
 
| Agent | Supported |
|---|---|
| Claude Code | Yes |
| Cursor | Yes |
| Kiro (AWS) | Yes |
| Windsurf | Yes |
| OpenCode | Yes |
| GitHub Copilot (via AGENTS.md) | Yes |
| Codex (OpenAI) | Yes |
 
---
 
## License
 
MIT — free to use, modify, and share.
 
---
 
*Built with SpecForge by T-is-enough Studio
