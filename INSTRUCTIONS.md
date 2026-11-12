# INSTRUCTIONS.md — NVIDIA SkillSpector (Rainer-Silva fork)

This file was added to the fork for Rainer Andrade Silva on 12 November 2026 (Europe/Stockholm). It is not part of the upstream project.

- **Upstream:** https://github.com/NVIDIA/SkillSpector (verified NVIDIA Corporation GitHub organisation)
- **This fork:** https://github.com/Rainer-Silva/SkillSpector
- **Docs:** https://docs.nvidia.com/skills/scanning-agent-skills
- **License:** Apache-2.0
- **Reviewed snapshot:** 25,529 stars, 2,255 forks, last upstream commit 11 Nov 2026, 22:07 CET (Europe/Stockholm), latest release v2.13.4. The Instagram reel claimed about 24k stars; the live count is in the same range.

## What it is

SkillSpector is NVIDIA’s open-source security scanner for AI agent skills (Claude Code, Codex, Gemini CLI, MCP skills, and similar). It looks for prompt injection, data exfiltration, dangerous code, supply-chain issues, and related patterns *before* you install a skill. It can scan a local folder, a `SKILL.md` file, a Git URL, or a zip, and can emit terminal, JSON, Markdown, or SARIF reports.

This is the most trustworthy of the five reel repos: it lives under the verified NVIDIA org, has an official docs.nvidia.com guide, and reports security issues to NVIDIA PSIRT (`psirt@nvidia.com`), not a public GitHub issue.

## Can it cut token usage / cost?

| Question | Honest answer |
|---|---|
| Cut Grok Bot / this assistant’s usage? | **No.** |
| Cut LLM token count? | **No.** Static scans (`--no-llm`) use no model tokens. Optional LLM “semantic” analysis *adds* tokens and may need a paid API key. |
| Why keep it anyway? | It reduces *risk* when you install skills such as Ponytail, Lemo-Opuscar, or Agent Reach. That is a safety tool, not a cost tool. |

## Setup (do not run until you have decided to try it)

Python 3.12+ (or Docker). From upstream’s README:

```bash
# CLI-only, static scans need no API key
uv tool install git+https://github.com/NVIDIA/skillspector.git

# Scan a skill folder without calling an LLM
skillspector scan ./path-to-skill/ --no-llm
```

From source: `git clone` this fork or upstream, create a venv, then `make install`. Docker: `make docker-build` (or `docker build -t skillspector .`) and mount the folder you want to scan.

Prefer `--no-llm` unless you have an approved paid key and a reason to run the slower semantic stage. Do not put API keys in chat or in a committed `.env`.

## Risks and caveats

- Low security concern relative to the other four repos. Still review what you install, and pin a release if you use it regularly.
- An LLM-backed scan can send skill text to the provider you configure. Use `--no-llm` for a local-only first pass.
- The scanner is a helper, not a guarantee that a skill is safe.
- **Cost:** optional LLM analysis may bill a provider. Static mode should be free.

## Cost note

Running anything that needs paid APIs or servers requires Rainer’s spend approval first. Forking, installing the CLI, and running `--no-llm` scans is free.

## Recommendation

Best of the five to actually use, but not for token savings. Install it in static mode and scan any third-party agent skill before enabling it. Track upstream for updates rather than relying only on this fork.
