# Skill Directory Structure

## Required Files

### SKILL.md

Every skill must have this:

#### YAML Frontmatter (Required)

```yaml
---
name: skill-name
description: Trigger description - when to use this skill
---
```

**Critical**: Description is what OpenClaw scans to decide "should I use this skill?" Put "when to use" info here.

#### Body

Core instructions. Only loaded after skill triggers. Keep under 500 lines.

---

## Optional Directories

### scripts/

Executable code (Python/Bash/etc.) - not just instructions.

```
scripts/
├── rotate_pdf.py
├── fetch_data.py
└── process.py
```

**Why**: OpenClaw executes scripts directly instead of rewriting the same code.

### references/

Detailed docs loaded on demand:

```
references/
├── api.md
├── patterns.md
└── examples.md
```

Keep SKILL.md concise - move detailed content here.

### assets/

Files for final output (templates, icons, etc.):

```
assets/
├── logo.png
├── template.html
└── frontend-boilerplate/
```

---

## What NOT to Include

- README.md
- INSTALLATION_GUIDE.md
- CHANGELOG.md
- QUICK_REFERENCE.md

Skills contain only what AI needs to execute - not process docs.

---

## Example Structures

### Simple
```
hello/
├── SKILL.md
```

### Medium
```
pdf-editor/
├── SKILL.md
└── scripts/
    └── rotate_pdf.py
```

### Complex
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
