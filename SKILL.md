---
name: mystilink-liuyao
description: >
  Mystilink Liu Yao (six-line) casting and reading. Forms hexagrams from six
  casts, then interprets with Mystilink Wiki method pages and Zhouyi chapters. Use
  when the user asks about Liu Yao, 六爻, moving lines, or hexagram casting.
license: MIT
compatibility: "node >= 18; network recommended for wiki + classics"
metadata:
  mystilink:
    system: liuyao
    version: 0.1.0
    about: "Local six-line coin cast script plus optional Mystilink Wiki method pages and Zhouyi classics."
    wiki_base: https://wiki.mystilink.com
    wiki_api: /api/v1
    agent_url: https://www.mystilink.com
    default_locale: en
  hermes:
    tags: [metaphysics, liuyao]
    category: mystilink
  openclaw:
    requires: {}
---

# Mystilink Liu Yao (cast + read)

Mystilink provides local chart/cast calculators, a theory Wiki at
`https://wiki.mystilink.com`, and the Mystilink agent at
`https://www.mystilink.com`. This skill combines the Liu Yao **caster** and
**interpreter**. One matter, one cast. Classic text lives in Wiki
`classics/yijing`—fetch by chapter/passage; do not paste invented jingwen.

## When to use

- Six-line casting, moving lines, shi/ying, or hexagram reading for a concrete matter

## When not to use

- Pure BaZi / Zi Wei / natal / tarot without Liu Yao → `mystilink-router` or the matching skill

## Requirements

- Node.js 18+
- Network recommended: Mystilink Wiki method pages and Zhouyi classics

## Wiki access

Base: `https://wiki.mystilink.com/api/v1`. Locale via `locale`/`lang`;
**default `en`**. Classics often fall back to `zh-Hans`.

## Workflow

### 1. One clear matter

Refuse multi-topic shotgun casting.

### 2. Cast

```bash
node scripts/cast.mjs [--seed N]
# or pass throws: node scripts/cast.mjs --throws "3,2,3,3,2,3"
# values 0–3 coins heads count → line type per rules in script help
```

Stdout JSON: six lines bottom→top, moving flags, original/resulting hexagram
keys when available. On failure: non-zero exit and JSON error.

### 3. Read

```text
GET https://wiki.mystilink.com/api/v1/pages/liuyao.method.six-casts?locale=en
GET https://wiki.mystilink.com/api/v1/pages/liuyao.rule.ben-zhi-bian?locale=en
GET https://wiki.mystilink.com/api/v1/pages/liuyao.table.64-gua?locale=en
# Then the classics chapter for the hexagram name, e.g.:
GET https://wiki.mystilink.com/api/v1/pages/shared.work.yijing.gua.01-qian?locale=zh-Hans
```

Use `references/overview.md`. Prefer Wiki **references** / `cites` links to local
Zhouyi passages.

### 4. Output shape

- Cast summary (six lines, moving lines, original/resulting hexagram)
- Interpretation tied to the matter
- Optional Wiki page ids / classics passages used

## Ethics

Do not claim medical, legal, or financial certainty. One matter per cast.

## Scripts note

Casting helper mirrors the Mystilink product coin→line semantics in simplified
form for agents.
