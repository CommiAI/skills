# My Skills

Custom agent skills for [OpenCode](https://opencode.ai), [Claude Code](https://claude.ai), and other coding agents.

## Installation

```bash
npx skills add CommiAI/skills
```

## Available Skills

| Skill | Description |
|-------|-------------|
| `create-verification-skill` | Creates a repo-specific skill, driving tools, and feature map for verifying real app behavior |
| `maintain-verification-skill` | Audits the verification skill and feature map against source and live app behavior |
| `frontend-skill` | Guides visually strong interfaces with restrained composition, imagery, and motion |
| `opinionated-code-structure` | Organizes functions in top-down reading order with useful one-sentence comments |

## Usage

In the application repo, ask your agent to run `create-verification-skill`:

```text
Use create-verification-skill to build a verification skill for this app.
```

The creator lives here; the generated verification skill and any helpers live in the application repo. Run the creator initially, then use and maintain the generated skill to verify changes.

Generated skills live in `.agents/skills/verify-<app>/` in the application repo. Use `maintain-verification-skill` to keep them current.

## Upstream attribution

`create-verification-skill` and `maintain-verification-skill` are copied from [pstack](https://github.com/cursor/plugins/tree/main/pstack), by Lauren Tan (poteto), including its feature-map examples and MIT license. Source commit: `ccb5507cec1546dc88135c1139c811e6c59115ba`.

These are locally maintained copies, not automatically updated dependencies. The only changes to the upstream skill instructions are `.cursor/skills/` → `.agents/skills/`.

## Creating New Skills

```bash
npx skills init my-new-skill
```

This creates a `skills/my-new-skill/SKILL.md` template.

## Structure

```
skills/
├── skill-name/
│   └── SKILL.md
└── another-skill/
    └── SKILL.md
```

Each `SKILL.md` needs YAML frontmatter with `name` and `description`.

## Development

### Link skills locally

Symlink skills into your agent directories for development:

```bash
npm run link
# or
bash scripts/link-skills.sh
```

This creates symlinks in `~/.claude/skills/` and `~/.agents/skills/` pointing to your local skills. Run `git pull` to update.

### List all skills

```bash
npm run list
# or
bash scripts/list-skills.sh
```

### Record changes

```bash
npx changeset
```

Follow the prompts to record changes for the changelog.

## License

MIT
