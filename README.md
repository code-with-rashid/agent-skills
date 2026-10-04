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

### Cursor

Customize → Rules → Add Rule → **Remote Rule (GitHub)** → paste the skill's repo URL,
e.g. `https://github.com/code-with-rashid/mental-model`.

### Codex CLI

Drop the skill folder into `$HOME/.agents/skills` (all repos) or
`$REPO_ROOT/.agents/skills` (this repo only):

```
git clone https://github.com/code-with-rashid/mental-model ~/.agents/skills/mental-model
```

Codex also supports installing directly via its skill installer — see the
[Codex skills docs](https://developers.openai.com/codex/skills) for the current syntax.

### Any other Agent-Skills-compatible tool

Every skill is a plain `SKILL.md` folder with no Claude-Code-only dependencies — clone
the individual skill's repo and point your tool at its `skills/<name>` directory. Check
your tool's own docs, or the [full client list](https://agentskills.io/clients) for
tool-specific install steps.

## Adding a new skill to the catalog

1. Ship the skill in its own repo, as a standard `skills/<name>/SKILL.md` package.
2. Add an entry to [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json)
   pointing at it via a `git-subdir` source.
3. Add a row to the table above.
