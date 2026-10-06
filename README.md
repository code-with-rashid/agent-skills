# Agent Skills

Portable coding-agent skills, built on the open [Agent Skills standard](https://agentskills.io) —
the same `SKILL.md` format read natively by Claude Code, Cursor, Codex CLI, Gemini CLI,
and 30+ other agent tools. Write once, use anywhere the standard is supported.

Each skill also lives in its own repo (own history, own issues, own stars) — this repo
is just the catalog that ties them together and makes them installable with a single
command in Claude Code.

## Skills

| Skill | What it does |
|---|---|
| [mental-model](https://github.com/code-with-rashid/mental-model) | Builds a correct, source-grounded mental model of how code actually works — instead of a confident-sounding guess. |
| [adversarial-qa](https://github.com/code-with-rashid/claude-adversarial-qa-skill) | Drives a repo to measured, resumable test-hardening convergence: coverage, mutation testing, fuzzing, and load/soak, until objective thresholds are met. |
| [test-fix-repeat](https://github.com/code-with-rashid/test-fix-repeat) | Tests a running app end to end, fixes real bugs with regression tests, and repeats until three clean rounds in a row. |
| [understory](https://github.com/code-with-rashid/understory) | Turns a codebase into an interactive HTML course the reader can actually defend — territory-mapped, self-verifying, with fieldwork in the real repo and spaced recall. |

More skills get added here as they ship — no need to re-add anything, they'll show up
in this catalog automatically.

## Install

### Claude Code

```
/plugin marketplace add code-with-rashid/agent-skills
/plugin install mental-model@codewithrashid-skills
/plugin install adversarial-qa@codewithrashid-skills
/plugin install test-fix-repeat@codewithrashid-skills
/plugin install understory@codewithrashid-skills
```

### Every other tool: copy the skill folder

Each skill is a plain `skills/<name>/` folder with a `SKILL.md` and no
Claude-Code-only dependencies. Copy that folder (not the whole repo) into the
skills directory your tool reads:

| Tool | Personal (all projects) | Project only |
|---|---|---|
| Codex CLI | `~/.agents/skills/` | `.agents/skills/` |
| Cursor | `~/.cursor/skills/` or `~/.agents/skills/` | `.cursor/skills/` or `.agents/skills/` |
| Gemini CLI | `~/.gemini/skills/` or `~/.agents/skills/` | `.gemini/skills/` or `.agents/skills/` |
| GitHub Copilot | `~/.copilot/skills/` or `~/.agents/skills/` | `.github/skills/` or `.agents/skills/` |
| Claude Code (without the plugin) | `~/.claude/skills/` | `.claude/skills/` |

`~/.agents/skills/` is read by Codex, Cursor, Gemini CLI, and Copilot, so one copy
there covers all four. For example, with `mental-model`:

```bash
git clone https://github.com/code-with-rashid/mental-model /tmp/mental-model
mkdir -p ~/.agents/skills
cp -r /tmp/mental-model/skills/mental-model ~/.agents/skills/
```

```powershell
git clone https://github.com/code-with-rashid/mental-model $env:TEMP\mental-model
New-Item -ItemType Directory -Force "$HOME\.agents\skills" | Out-Null
Copy-Item -Recurse "$env:TEMP\mental-model\skills\mental-model" "$HOME\.agents\skills\"
```

Some tools can also install straight from the repo:

- Gemini CLI: `gemini skills install https://github.com/code-with-rashid/mental-model.git --path skills/mental-model`
- Codex CLI: ask the built-in `$skill-installer` to install from the repo URL.

Per-tool docs: [Codex](https://developers.openai.com/codex/skills) ·
[Cursor](https://cursor.com/docs/skills) ·
[Gemini CLI](https://geminicli.com/docs/cli/skills/) ·
[Copilot](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/create-skills) ·
[all Agent Skills clients](https://agentskills.io/clients).

## Adding a new skill to the catalog

1. Ship the skill in its own repo, as a standard `skills/<name>/SKILL.md` package.
2. Add an entry to [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json)
   pointing at it via a `git-subdir` source.
3. Add a row to the table above.
