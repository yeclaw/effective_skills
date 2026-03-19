---
name: effective-skills
description: Best practices for designing high-quality Agent Skills. Trigger: ("写个skill", "写个脚本", "创建skill", "创建一个skill", "创建自动化流程", "优化这个skill", "how to write a skill", "create a skill", "design a skill", "skill optimization"). Use when creating new skills, optimizing existing ones, or when skills aren't working well. For technical implementation (init, package, validate), refer to skill-creator.
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

# ✅ Valuable
- This project's function naming: snake_case
- Common functions are in utils.py
```

### 3. Verify! Verify! Verify!

Code development skills MUST include verification steps:

```markdown
- [ ] Step 3: Write functional code
- [ ] Step 4: Run syntax check ← Required
- [ ] Step 5: Execute tests ← Required
```

### 4. Avoid Railroading

Give OpenClaw flexibility to adapt:

```markdown
# ❌ Too rigid
Must read A first, then B, then write C

# ✅ Flexible
Recommended order: A → B → C, adjust based on实际情况
```

### 5. Store Scripts, Not Just Instructions

Rather than describing steps in text, provide executable scripts:

```markdown
# ❌ Text-heavy
To process data: read the file, parse JSON, filter, output

# ✅ Script-based
scripts/
├── process_data.py  # Reusable, deterministic
```

This lets OpenClaw focus on composition, not reconstructing boilerplate.

---

## ✅ Skill Design Checklist

Before finishing a skill, verify:

- [ ] **English Only**: SKILL.md and all resources written in English
- [ ] **Trigger phrases**: description covers all likely trigger words/phrases
- [ ] **Concise SKILL.md**: body under 500 lines, core workflow only
- [ ] **Progressive disclosure**: detailed content in references/, not SKILL.md
- [ ] **Code verification**: syntax check + test execution steps included
- [ ] **Scripts vs text**: reusable code in scripts/, not prose
- [ ] **Cross-reference**: references skill-creator or auto-todo where relevant

---

## 🎯 Design Principles

### Concise is Key

Context window is a shared resource. Only add what OpenClaw doesn't know.

### Progressive Disclosure

Three-layer loading:
1. **Metadata** - Always in context (~100 words)
2. **SKILL.md body** - When skill triggers (<5k words)
3. **references/** - On demand (unlimited)

### Skill Composition

Skills can depend on each other:

```markdown
# In skill-a
To execute X, first use skill-b
```

OpenClaw will automatically invoke installed dependent skills.

---

## 📁 Directory Structure

```
skill-name/
├── SKILL.md           # Required: metadata + core
├── scripts/           # Executable code (Python/Bash)
├── references/        # Docs loaded on demand
└── assets/           # Output resources (templates, etc.)
```

**scripts/**: Store reusable code instead of rewriting.
**references/**: Keep detailed docs here, not in SKILL.md.
**assets/**: Templates and files for output.

---

## 🔗 Related Skills

- **skill-creator** - Technical implementation: init, package, validate (use AFTER planning with effective-skills)
- **auto-todo** - Multi-step task framework for complex skill development
