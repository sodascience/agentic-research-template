# Agentic research project starter

A reusable starting point for researcher-led work with an AI agent. Use it to develop a project brief, agree a study design, plan manageable tasks, and implement and verify an analysis. No dataset, programming language, or research method is prescribed.

## Start a research project

1. On GitHub, choose **Use this template → Create a new repository**, then open your new repository locally. You can also copy these files into a new local Git repository.
2. Review `AGENTS.md` and configure actual file, network, and execution permissions in your AI tool. Written instructions do not enforce access restrictions. Check what information may be shared before supplying data or documentation.
3. Make permitted data documentation available. Add datasets only when needed; decide what may be tracked or shared before staging files. Use suitable synthetic data first when available. Do not assume real data may be accessed because the scripts worked on synthetic data.
4. Start the project-brief discussion using the prompt below. Adapt `AGENTS.md` after agreeing the brief, then develop the study design. Keep substantive choices with the researcher.

## Using different agents

The research documents and skill instructions are shared across tools. This starter keeps one set of skill files in `.agents/skills/`. The folder link `.claude/skills` points to that same location so Claude Code can discover them too.

- **Codex:** discovers skills in `.agents/skills/`. Use `$develop-research-plan` or `$implement-and-verify` in the prompts below. If they do not appear, check skill discovery or start a new chat. See the [Codex skills documentation](https://learn.chatgpt.com/docs/build-skills).
- **Claude Code:** `CLAUDE.md` imports the shared working instructions from `AGENTS.md`. The `.claude/skills` folder link makes the same skills available for automatic discovery. Use `/develop-research-plan` or `/implement-and-verify` instead of the Codex `$` forms in the prompts below. If discovery fails, use the explicit file-reading examples below. See [Claude Code skills](https://code.claude.com/docs/en/skills) and [project instructions](https://code.claude.com/docs/en/memory).
- **Other file-capable agents:** explicitly ask the agent to read `AGENTS.md` and the relevant skill file. Check the tool's permissions and instruction-loading behaviour. In a chat without local file access, supply the relevant files and templates yourself and run code locally.

Folder links work naturally on macOS and Linux. On Windows, Git may check out the link as a text file unless symbolic-link support is enabled. If `.claude/skills` does not open as a folder, use the explicit-reading fallback; do not maintain duplicate skill copies.

For the fallback in Claude Code or another file-capable agent, replace `Use $develop-research-plan` in a prompt with:

```text
Read AGENTS.md and .agents/skills/develop-research-plan/SKILL.md and follow
that guidance
```

Replace `Use $implement-and-verify` with:

```text
Read AGENTS.md and .agents/skills/implement-and-verify/SKILL.md and follow
that guidance
```

Keep the rest of the task request. These explicit file-reading requests do not require skill installation. Use them again when starting a new chat as needed.

## Where things belong

| File or folder | Purpose |
|---|---|
| `.claude/skills` | Folder link to the shared skills for Claude Code discovery. |
| [CLAUDE.md](CLAUDE.md) | Imports the shared working instructions for Claude Code. |
| [AGENTS.md](AGENTS.md) | Default working rules, permissions to clarify, verification, records, and commit policy. Adapt for your project. |
| [Research prompt templates](templates/research_prompts.md) | Ready-to-copy requests for each stage, with agent-specific invocation guidance. |
| [Planning skill](.agents/skills/develop-research-plan/SKILL.md) | Interactive guidance for the brief, design, and plan. |
| [Bundled templates](.agents/skills/develop-research-plan/assets/templates/) | Authoritative blank document structures; no duplicate copies are needed. |
| [Implementation skill](.agents/skills/implement-and-verify/SKILL.md) | Guidance for implementation, verification, bug fixes, and final review. |

Save completed `project_brief.md`, `study_design.md`, and `implementation_plan.md` in the project root as each stage is agreed. Leave unknowns explicit. Add analysis folders and software dependencies when the plan needs them. Replace this README's starter guidance with project-specific setup, input versions, run instructions, and AI-use records as the project develops.

## Recommended chats

| Chat | Work |
|---|---|
| 1 | Develop the brief, adapt `AGENTS.md`, and co-create the study design. Start a separate design chat if the discussion becomes lengthy. |
| 2 | Build the implementation plan from the saved, agreed design. |
| 3 | Implement and verify related units; diagnose bugs in the same chat while context remains useful. |
| 4 | Perform a fresh final rerun and review. |

This is a default, not a requirement. Start fresh sooner if abandoned approaches or conflicting decisions make a chat confusing. Before switching, update the existing documents with agreed choices, evidence, and open issues. A new chat does not itself make verification independent; meaningful checks still matter.

## Start the discussion

Use the opening prompt below, replacing bracketed fields. For Claude Code, use `/develop-research-plan`; for other agents, see the explicit-reading fallback in the [research prompt templates](templates/research_prompts.md).

```text
Use $develop-research-plan to help me develop project_brief.md.
My initial idea is [idea], intended output is [output or undecided], and
available time is [time]. Documentation is at [location or not yet available].
Start with focused questions; do not inspect record-level data or write
analysis code yet. Propose a brief for review and save it after I agree.
Stop after the brief.
```

Continue with the [research prompt templates](templates/research_prompts.md) for working instructions, study design, implementation planning, implementation, verification, bug fixes, resuming work, revisions, commits, and final review. The skills hold the detailed process; the prompts specify what to do now.

## For template maintainers

To make this repository a GitHub template, enable **Template repository** under **Settings → General** after publishing it. Projects created from it are independent copies; improvements do not automatically propagate. Keep data and completed research decisions out of this starter. Choose a licence before offering the materials for general reuse; this starter does not assign one on your behalf.

The workflow is informed by the [SoDa AI-assisted research programming workshop](https://github.com/sodascience/workshop-ai-assisted-research-programming). The starter text and skills were written for this workflow; external skill frameworks are not bundled. AI-use recording guidance in `AGENTS.md` draws on [Feuerriegel et al. (2026), GUIDE-LLM](https://doi.org/10.1038/s41562-026-02492-7). Test the skills on a real project before treating them as established teaching materials.
