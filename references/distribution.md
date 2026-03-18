# Skill Distribution Guide

## Option 1: In Repo (Small Teams)

```
./claude/skills/           # Project-level
~/.claude/skills/           # User-level
```

**Pros**:
- Simple and direct
- Version controlled
- Team sharing

**Cons**:
- Adds context to every repo
- Hard to distribute across many repos

---

## Option 2: Marketplace (Scale)

### Upload Process

1. **Development**: Test locally or in sandbox
2. **Validation**: Ensure real usage demand
3. **Submit**: Move to marketplace directory

### Curation Principles

**Pre-publish Checklist**:
- [ ] Clear description?
- [ ] Gotchas included?
- [ ] Avoided obvious content?
- [ ] Validated with real use cases?

**Quality Standards**:
- Unique domain knowledge > generic knowledge
- Real failure experience > theory
- Concise > verbose

---

## Dependency Management

Skills can depend on other skills:

```
skill-a/           # Uploaded skill
skill-b/           # Dependency
```

Usage:
```markdown
# In skill-a
To execute X, first use skill-b
```

Model will automatically invoke installed dependent skills.

---

## Measurement & Iteration

### Track Usage

Use PreToolUse hook to log skill usage:

```python
# Pseudocode
def pre_tool_use(tool_name, tool_input):
    if tool_name == "SkillLoader":
        log_skill_usage(tool_input["skill_name"])
```

### Metrics

- Usage frequency
- Trigger accuracy (correct scenario)
- User feedback

### Iteration Loop

1. Use in real tasks
2. Find inefficiencies or failures
3. Update SKILL.md or resources
4. Retest

---

## FAQ

**Q: When should I create a new skill?**
A: When a domain's knowledge or workflow repeats frequently and existing skills can't cover it.

**Q: Skill too long?**
A: Split into references/, use progressive disclosure.

**Q: How to handle sensitive info?**
A: Use config.json, add to .gitignore for sensitive configs.
