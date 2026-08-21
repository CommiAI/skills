# My Skills

Custom agent skills for [OpenCode](https://opencode.ai), [Claude Code](https://claude.ai), and other coding agents.

## Installation

```bash
npx skills add CommiAI/skills
```

## Available Skills

| Skill | Description |
|-------|-------------|
| `humanlayer-orchestrator` | Orchestrates durable tasks and coding sessions through the HumanLayer CLI |

## Usage

The orchestrator is user-invoked so it only takes control when explicitly requested:

```text
$humanlayer-orchestrator implement these changes in parallel and return one consolidated result
```

Authenticate against either HumanLayer environment before the first run:

```bash
humanlayer login
# or
humanlayer --beta login
```

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
