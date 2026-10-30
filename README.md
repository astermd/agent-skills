# AsterMD Agent Skills

Reusable [Agent Skills](https://agentskills.io) for working with the [AsterMD](https://www.astermd.com/) EMR platform. Each skill is a folder with a `SKILL.md` (instructions + frontmatter), so it works with any agent that supports the format — Claude Code, Codex, Cursor, Gemini CLI, and others.

## Skills

| Skill | What it does |
| --- | --- |
| [`astermd-teleform-builder`](skills/astermd-teleform-builder/SKILL.md) | Turns a list of intake/telemedicine questions (markdown, text, doc, or chat) into teleform builder JSON that imports via **Teleforms → Import JSON**. Also fixes/updates existing teleform JSON. |

## Install

### Option 1: `npx skills` (any agent)

```bash
# list skills in this repo
npx skills add astermd/agent-skills --list

# install one skill
npx skills add astermd/agent-skills --skill astermd-teleform-builder

# install all skills
npx skills add astermd/agent-skills --all
```

The CLI asks which agents (Claude Code, Codex, Cursor, …) to install for, and whether to install per-project or globally.

> No npm package is needed — skills are pulled straight from GitHub.

### Option 2: Manual copy

Clone the repo, then copy the skill folder(s) into your agent's skills directory:

```bash
git clone https://github.com/astermd/agent-skills.git
cd agent-skills

# Claude Code (global)
cp -R skills/astermd-teleform-builder ~/.claude/skills/
# Claude Code (single project)
cp -R skills/astermd-teleform-builder <project>/.claude/skills/

# Codex / other agents following the open standard
cp -R skills/astermd-teleform-builder ~/.agents/skills/
```

Check your agent's docs for its exact skills path. For agents with no skill support, paste the contents of `SKILL.md` into the system prompt or project instructions file (e.g. `AGENTS.md`).

### Updating

Skills are copies, so they do not update themselves. Pull new versions when you want them:

```bash
npx skills check    # see if installed skills have updates
npx skills update   # update installed skills
```

Manual installs: `git pull` in your clone and copy the folder again.

## Usage

Skills trigger automatically when your request matches their description, or you can call one by name (e.g. `/astermd-teleform-builder` in Claude Code).

### astermd-teleform-builder

Give it your questions and it writes an importable JSON file:

```
Create a teleform JSON for an NAD+ intake from questions.md
```

Then in AsterMD: **Teleforms → New Form → Import JSON**, choose the form type, paste the JSON (or *Choose JSON File*), and click **Import Template**. The skill reports page/field/condition counts and flags anything it couldn't express.

## Repo layout

```
skills/
  <skill-name>/
    SKILL.md        # required: frontmatter (name, description) + instructions
    ...             # optional: references, scripts, assets
```

## Contributing a skill

1. Create `skills/<kebab-case-name>/SKILL.md` with `name` (matching the folder) and `description` frontmatter. The description decides when agents load the skill, so say what it does and when to use it.
2. Keep instructions agent-neutral — avoid tool names specific to one agent.
3. Keep it public-safe — describe behavior users can see in AsterMD; no internal source paths, file names, function names, or other private implementation details.
4. Add a row to the **Skills** table above.

## License

[MIT](LICENSE) © CodeClouds™ DBA [AsterMD](https://www.astermd.com/)
