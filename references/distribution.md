# Skill Distribution

## Option 1: In Repo

```
.claude/skills/           # Project-level
~/.claude/skills/         # User-level
```

## Option 2: ClawHub

1. Test in sandbox
2. Verify real demand
3. Publish to share

## Skill Dependencies

Skills can depend on each other:

```markdown
# In skill-a
To execute X, use skill-b first
```

OpenClaw automatically invokes dependent skills.

---

## Measurement

Track skill usage to find:
- Popular skills
- Undertriggering skills
- Areas for improvement
