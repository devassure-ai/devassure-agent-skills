# devassure-agent-skills

This repository holds **Claude Skills** for [DevAssure](https://app.devassure.io): packaged instructions and references so Claude can help you install, configure, and use the **DevAssure CLI** (`@devassure/cli`) for natural-language, browser-based end-to-end tests.

## What are Claude Skills?

**Skills** are directories built around a `SKILL.md` file. They extend what Claude can do by giving it a focused playbook (workflows, conventions, and pointers to extra files). Skills follow the [Agent Skills](https://agentskills.io/) open standard; in **Claude Code**, they also support supporting assets (e.g. reference markdown), optional frontmatter, and automatic loading when a task matches the skill’s description.

- **Automatic use:** Claude can load a skill when your request matches its `description` in the skill frontmatter.
- **Explicit use:** You can invoke a skill by typing **`/`** plus the skill **`name`** from that frontmatter (same idea as other slash commands in Claude Code).

Official overview: [Extend Claude with skills](https://docs.anthropic.com/en/docs/claude-code/skills).

## What’s in this repo

| Path | Purpose |
| --- | --- |
| `skills/devassure/SKILL.md` | Main skill: CLI install, auth, `init`, YAML tests, `run-tests`, CI, troubleshooting pointers |
| `skills/devassure/references/` | Deeper docs the skill points to (`cli-reference.md`, `cli-troubleshooting.md`) |

The skill’s frontmatter declares `name: devassure`, which defines the slash command (see below).

## Using `/devassure` in Claude

After the skill is installed where Claude Code looks for skills (see below), you can use it in two ways:

1. **Explicit invocation** — Type **`/devassure`** in the composer or prompt. You can add context on the same line, for example:
   - `/devassure` — open-ended help on DevAssure CLI setup and usage  
   - `/devassure help me add a smoke test for login in .devassure/tests/` — task-specific assistance  

2. **Implicit (automatic) invocation** — Ask in natural language about DevAssure, the CLI, YAML/CSV tests, `.devassure` layout, CI tokens, etc. Claude can apply this skill when your message matches its description (without typing `/devassure`).

## Installing this skill

### From the Claude console

1. In the **Claude** console, run a prompt such as: **Install the DevAssure skill from https://github.com/test-plus-plus/devassure-cli-skills**
2. **Restart** your Claude session so the skill loads and you can use it.
3. Invoke **`/devassure`** or ask about DevAssure in natural language.

### Manual install (clone or copy)

Skills are a folder whose entrypoint is `SKILL.md`. Copy or symlink this repo’s **`skills/devassure`** directory into a Claude skills location (for example `~/.claude/skills/devassure` for a personal install).

**Personal (all projects):**

```bash
mkdir -p ~/.claude/skills
ln -s /path/to/devassure-cli-skills/skills/devassure ~/.claude/skills/devassure
# or: cp -r .../devassure ~/.claude/skills/devassure
```

**Single project only:**

```bash
mkdir -p .claude/skills
ln -s /path/to/devassure-cli-skills/skills/devassure .claude/skills/devassure
```

See [Where skills live](https://docs.anthropic.com/en/docs/claude-code/skills#where-skills-live) for enterprise, plugin, and monorepo paths.

## Project context with `CLAUDE.md`

Adding a **`CLAUDE.md`** file (sometimes `claude.md`, depending on OS) at the root of your **application** repository (the repo where you build and test your product) gives Claude durable, project-specific guidance so it can reuse the same conventions and remember what matters for that codebase across sessions.

Use it to tell Claude where the DevAssure skill lives in your tree and to prefer it for test work—for example:

```markdown
# End to End Testing

Read `skills/devassure/SKILL.md` at the start of every session and follow its instructions for all test-related tasks.
```

If you keep a copy of the skill under another path, update the path—for example `src/skills/devassure/SKILL.md` when the skill lives under `src/skills/`.

---

*DevAssure CLI: global install `npm install -g @devassure/cli`, then `devassure login`, `devassure init`, and `devassure run-tests` — full detail is inside the skill and its `references/` files.*
