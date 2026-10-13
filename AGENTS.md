# AGENTS.md

The KIRHA agent skill. It teaches an agent to call the KIRHA CLI for live, sourced data from specialized providers instead of answering from memory.

## Installing it

```bash
npx skills add kirha-ai/kirha-skill
```

The skill needs the `kirha` CLI and an API key from https://app.kirha.com/api-keys. The CLI can install the skill itself with `kirha skills install`.

## Working on this repo

- The skill is one file: `skills/kirha/SKILL.md`. There is no build and no test.
- The `description` in the frontmatter must stay under 1024 characters. It is what agents read to decide when to use the skill.
- Bump `metadata.version` in the frontmatter on every change.
- Every `kirha` command or flag in the skill must exist in the current CLI (https://github.com/kirha-ai/kirha-cli). Check its `llms.txt` before adding one.
- Keep the workflow order: search without a vertical first, discovery and `--focus` only when results are thin.
