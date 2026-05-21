# Planning Slices Skill

[![skills.sh](https://skills.sh/b/kodi/planning-slices)](https://skills.sh/kodi/planning-slices)

An agent skill for writing engineering plans as recoverable implementation slices instead of static proposals. It helps agents create and maintain `docs/plans` handoff documents with explicit decisions, ordered slice boundaries, verification steps, and progress notes.

## Install

```bash
npx skills add kodi/planning-slices
```

To install non-interactively for Codex or another supported agent:

```bash
npx skills add kodi/planning-slices -g -y
```

## Skill

The installable skill lives at [`skills/planning-slices`](./skills/planning-slices).

It should trigger when an agent needs to:

- draft a plan under `docs/plans`
- split a migration or multi-module feature into ordered slices
- record decisions, scope, verification, and open questions
- update slice status and working notes after implementation progress

## Structure

```text
skills/
  planning-slices/
    SKILL.md
    agents/
      openai.yaml
```

## License

MIT
