# Skill Directory Structure

## Required Files

### SKILL.md

Every skill must have this, containing two parts:

#### 1. YAML Frontmatter (Required)

```yaml
---
name: skill-name          # Skill name
description: Trigger description  # Most important! Tells model when to use
---
```

**Description Writing Tips**:
- Include "when to use" information
- List specific use cases
- Use active voice

#### 2. Body (Markdown)

Core instructions and guidance. Only loaded after skill triggers.

---

## Optional Directories

### scripts/ - Executable Scripts

**Purpose**: Code requiring deterministic reliability

```
scripts/
├── rotate_pdf.py
├── fetch_data.py
└── process.py
```

**Use when**:
- Same code being rewritten repeatedly
- Deterministic results needed
- Can execute without loading into context

### references/ - Reference Docs

**Purpose**: Detailed docs loaded on demand

```
references/
├── api.md       # API docs
├── patterns.md  # Pattern guides
└── examples.md  # Examples
```

**Use when**:
- Detailed docs don't need to always be in context
- Load on demand (when user asks about related topic)
- Keep SKILL.md concise

**Best practices**:
- Use grep patterns for files > 10k words
- Avoid duplication with SKILL.md
- Only include essential info

### assets/ - Output Resources

**Purpose**: Files for final output, not loaded into context

```
assets/
├── logo.png
├── template.html
└── frontend-boilerplate/
```

**Use when**:
- Template files
- Brand assets
- Files to copy/modify

---

## What NOT to Include

❌ Don't create:
- README.md
- INSTALLATION_GUIDE.md
- CHANGELOG.md
- QUICK_REFERENCE.md

Skills should only contain info needed for AI to do the task—not process documentation.

---

## Example Structures

### Simple Skill
```
hello/
├── SKILL.md
```

### Medium Complexity
```
pdf-editor/
├── SKILL.md
└── scripts/
    └── rotate_pdf.py
```

### Complex Skill
```
data-science/
├── SKILL.md
├── scripts/
│   ├── fetch_bq.py
│   └── visualize.py
├── references/
│   ├── schemas.md
│   └── metrics.md
└── assets/
    └── report-template.html
```
