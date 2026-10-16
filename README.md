# My Skills

Custom agent skills for [OpenCode](https://opencode.ai), [Claude Code](https://claude.ai), and other coding agents.

## Installation

```bash
npx skills add CommiAI/skills
```

## Available Skills

| Skill | Description |
|-------|-------------|
| `frontend-skill` | Guides visually strong interfaces with restrained composition, imagery, and motion |
| `opinionated-code-structure` | Organizes functions in top-down reading order with useful one-sentence comments |
| `writing-for-agents` | Guides writing skills, agent instructions, and other documents agents consume |

## Usage

Ask your agent to use a skill for the relevant task:

```text
Use frontend-skill to design this app's interface.
```

## Upstream attribution

`writing-for-agents` is copied unchanged from [Matt Pocock's skills](https://github.com/mattpocock/skills/tree/main/skills/productivity/writing-for-agents), including its companion reference, agent metadata, and MIT license. Source commit: `f3fc5632f401156837ee3872f14fe33ccf1024ea`. It is also maintained locally.

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
