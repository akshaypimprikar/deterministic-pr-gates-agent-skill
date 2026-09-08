# Deterministic PR Gates

A Claude Code agent skill that runs pre-PR verification as real, scriptable checks: an exit code, a grep match, a coverage percentage. Not a model judging whether a diff looks ready.

## Why deterministic, not LLM-judged

Most "quality gate" agent skills work by asking an LLM to read a diff and judge it: is this good code, does it follow our conventions, is anything missing. That's a real capability, but it's non-deterministic. The same diff can pass on one run and get flagged on the next, and a confident-sounding judgment is not the same as a verified fact.

This skill does the opposite. Every gate is a real command with a checkable outcome. Nothing here asks a model to opine. Use an LLM-judgment skill *in addition* to this one for things that are genuinely subjective, like whether a variable name communicates intent. Use this skill for everything that has a yes/no answer.

## What it checks

Ten gates, most conditional on what actually changed on the branch: build, full test suite, TODO/FIXME/HACK scan, branch naming convention, changelog presence, coverage threshold on new files, a security-file touch check, an abstraction-bloat/duplication heuristic, and a slot for your project's own architecture and layer rules, instantiated as greps from whatever your `CLAUDE.md`/`AGENTS.md` already documents.

Works standalone in any project — no other skill or pipeline required. See [`skills/deterministic-pr-gates/SKILL.md`](skills/deterministic-pr-gates/SKILL.md) for the full gate list and instantiation instructions.

## Origin

Extracted from [pragma](https://github.com/akshaypimprikar/pragma), a Claude Code plugin implementing a full `spec → plan → feature → gates → review → test → bugfix → release` pipeline for iOS projects. This is the `/gates` stage's underlying skill, generalized to run standalone in any language or project. If you want the full pipeline it sits inside, see pragma.

## License

MIT — see [LICENSE](LICENSE).
