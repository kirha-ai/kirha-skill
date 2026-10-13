# AGENTS.md

The KIRHA agent skill. It teaches an agent to call the KIRHA CLI for live, sourced data from specialized providers instead of answering from memory.

- Get an API key: https://app.kirha.com/api-keys
- Skill docs: https://docs.kirha.com/skills.mdx

```bash
npx skills add kirha-ai/kirha-skill
```

The skill needs the `kirha` CLI (https://docs.kirha.com/cli.mdx), logged in with the API key. The CLI can also install the skill with `kirha skills install`.
