---
name: effective-skills
description: Best practices for designing high-quality Agent Skills. Use when creating new skills, optimizing existing ones, or when skills aren't working well. Includes: Gotchas (common failure points), design principles, description writing tips, progressive disclosure strategy. For technical implementation details, refer to skill-creator.
---

# Effective Skills Design

## ⚠️ Gotchas (Most Important!)

Highest-value information from real failures.

### 1. Description is for the Model, Not Humans

```yaml
# ❌ Wrong: Too vague
description: "Helps write Python code"

# ✅ Correct: Specific triggering conditions
description: "Python code writing, debugging, and refactoring. Use when: writing new features, debugging, code review, or refactoring."
```

**Key**: Put "when to use" info in description, NOT in body.

### 2. Don't State the Obvious

OpenClaw is already smart. Provide:
- Your domain-specific knowledge
- Common failure points and solutions
- Unique workflows

```markdown
# ❌ Redundant
- Use Python's def keyword to define functions
- Functions can have parameters and return values

# ✅ Valuable
- This project's function naming: snake_case
- Common functions are in utils.py, avoid duplicates
```

### 3. Verify! Verify! Verify!

Code development skills MUST include verification steps:

```markdown
- [ ] Step 3: Write functional code
- [ ] Step 4: Run syntax check ← Required
- [ ] Step 5: Execute tests ← Required
```

### 4. Avoid Railroading

Give OpenClaw enough information, but keep flexibility:

```markdown
# ❌ Too rigid
Must read A first, then B, then write C

# ✅ Flexible
Recommended order: A → B → C, but adjust based on实际情况
```

---

## 🎯 Design Principles

### Concise is Key

Context window is a shared resource. Assume OpenClaw is already smart—only add context it doesn't have.

**Test**: Is this information worth the token cost?

### Set Appropriate Degrees of Freedom

Choose freedom level based on task type:

| Task Type | Freedom | Example |
|-----------|---------|---------|
| Text creation | High | "Write in a lively tone..." |
| Fixed patterns | Medium | "Use this template, parameters adjustable" |
| Fragile operations | Low | "Must execute these 5 steps in order" |

### Progressive Disclosure

Three-layer loading:
1. **Metadata** (name + description) - Always in context
2. **SKILL.md body** - Loaded when skill triggers
3. **references/** - Loaded on demand

---

## 📁 Directory Structure

```
skill-name/
├── SKILL.md           # Required: metadata + core instructions
├── scripts/           # Optional: executable scripts
├── references/        # Optional: docs loaded on demand
└── assets/           # Optional: output resources
```

See [references/structure.md](references/structure.md) for details.

---

## 📦 Distribution

### Option 1: In Repo

```
./claude/skills/           # Project-level skill
~/.claude/skills/           # User-level skill
```

### Option 2: Publish

- Test in sandbox first
- Verify actual demand before publishing
- Maintain quality control

See [references/distribution.md](references/distribution.md).

---

## 🔗 Related Skills

- **skill-creator** - Technical implementation: creating, initializing, packaging skills
- **auto-todo** - Multi-step task execution framework

Use skill-creator for technical details, this skill for design guidance.
