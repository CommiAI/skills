# My Skills Repository

This repository contains custom agent skills for AI coding assistants.

## Structure

Skills are organized under `skills/`:

```
skills/
├── skill-name/
│   └── SKILL.md
└── another-skill/
    └── SKILL.md
```

## Adding a New Skill

1. Run `npx skills init my-skill-name` to create a template
2. Edit `skills/my-skill-name/SKILL.md` with your instructions
3. Update `.claude-plugin/plugin.json` to include the new skill
4. Update `README.md` to list the new skill

## Skill File Format

Each `SKILL.md` must have YAML frontmatter:

```yaml
---
name: skill-name
description: What this skill does and when to use it
---
```

Then provide clear instructions for the agent to follow.

## Maintenance

- Run `scripts/link-skills.sh` to symlink skills into local agent directories
- Run `scripts/list-skills.sh` to see all skills in the repo
- Use `npx changeset` to record changes for the changelog

## Invocation Types

Skills can be:

- **User-invoked**: Only triggered when the user explicitly requests them
- **Model-invoked**: Can be triggered by the agent when the task fits

Set `disable-model-invocation: true` in frontmatter for user-invoked skills.
