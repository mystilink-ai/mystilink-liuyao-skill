# Changelog

Version is tracked in `SKILL.md` under `metadata.mystilink.version` and in this file.

## 0.1.0

- Agent Skill for Liu Yao (six-line) casting and reading
- `scripts/cast.mjs` forms a hexagram from six casts and marks moving lines
- `references/overview.md` maps hexagram fields to Mystilink Wiki method pages and Zhouyi chapters (`wiki.mystilink.com`)
- `examples/cast-request.json` gives a runnable cast request
- Runtime: `node >= 18`; the Wiki and classics lookup is used when network access is available
- Install by copying this directory into a host skills path that reads `SKILL.md`
