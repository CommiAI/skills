# My Skills

Custom agent skills for [OpenCode](https://opencode.ai), [Claude Code](https://claude.ai), and other coding agents.

## Installation

```bash
npx skills add CommiAI/skills
```

## Available Skills

| Skill | Description |
|-------|-------------|
| `example-skill` | A template for creating new skills |

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
