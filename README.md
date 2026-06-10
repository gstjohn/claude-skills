# Skills

A collection of installable skills for Claude. Each skill lives in its own folder under `skills/` and installs independently.

## Skills

| Skill | What it does | Rationale |
|---|---|---|
| [decode](skills/decode/) | Faithfully re-encodes dense inbound content (email, transcript, message, document) to fit how you read, preserving meaning and adding nothing the sender did not say. | [docs/decode/README.md](docs/decode/README.md) |

## Installing a skill

A skill is a folder under `skills/` (for example `skills/decode/`). Install only that folder. The `docs/` tree is design rationale for humans and is not part of the skill.

Custom skills do not sync across surfaces, so add the skill on each surface where you want it.

### Claude Code (filesystem, no zip)

Copy the skill folder into your Claude Code skills directory. Claude Code discovers it automatically; there is no upload step.

- Personal (all projects): `~/.claude/skills/decode/`
- Project only: `.claude/skills/decode/` in the project root

```bash
rm -rf ~/.claude/skills/decode && cp -R skills/decode ~/.claude/skills/decode
```

### Claude.ai and Claude Cowork (zip upload)

Cowork runs inside the Claude desktop app and uses the same custom skills you add to your Claude account.

1. Zip the skill folder:
   ```bash
   cd skills && zip -r decode.zip decode && cd ..
   ```
2. In the Claude app, open Customize > Skills, choose Create skill, then Upload a skill, and select `decode.zip`.

Free, Pro, and Max plans can upload custom skills directly in Customize > Skills. Team and Enterprise plans require an org Owner to enable Skills and code execution in Organization settings first. Custom skills uploaded this way are per-user, not org-wide.

## Repo layout

```
skills/<name>/          the installable unit (SKILL.md + references/)
docs/<name>/            design docs for that skill (README, CONTEXT, ADRs, research)
```

## Adding a skill

1. Create `skills/<name>/` with a `SKILL.md` and any `references/`. Do not put a `README.md` inside a skill folder; skill documentation goes in `SKILL.md` or `references/`.
2. Create `docs/<name>/` for that skill's design docs and human-facing rationale.
3. Add a row to the Skills table above.

## License

[MIT](LICENSE), Copyright (c) 2026 Garrett St. John.
