# Skill 目录结构详解

## 必需文件

### SKILL.md

每个 skill 必须包含，包含两部分：

#### 1. YAML Frontmatter (必需)

```yaml
---
name: skill-name          # 技能名称
description: 触发描述     # 最重要！告诉模型什么时候用这个 skill
---
```

**description 写作技巧**：
- 包含"什么时候用"的信息
- 列出具体使用场景
- 使用主动语态

#### 2. Body (Markdown)

核心指令和指导。只在 skill 触发后加载。

---

## 可选目录

### scripts/ - 可执行脚本

**用途**：需要确定性可靠性的代码

```
scripts/
├── rotate_pdf.py
├── fetch_data.py
└── process.py
```

**使用场景**：
- 相同代码被反复重写
- 需要确定性结果
- 可以不加载到上下文直接执行

### references/ - 参考文档

**用途**：按需加载的详细文档

```
references/
├── api.md       # API 文档
├── patterns.md  # 模式指南
└── examples.md  # 示例
```

**使用场景**：
- 详细文档不需要始终在上下文
- 按需加载（用户问到相关话题时）
- 保持 SKILL.md 简洁

**最佳实践**：
- 文件 > 10k 字时使用 grep 模式
- 避免与 SKILL.md 重复
- 只放必要信息

### assets/ - 输出资源

**用途**：最终输出使用的文件，不加载到上下文

```
assets/
├── logo.png
├── template.html
└── frontend-boilerplate/
```

**使用场景**：
- 模板文件
- 品牌资源
- 需要拷贝/修改的文件

---

## 什么不该放

❌ 以下文件**不需要**创建：
- README.md
- INSTALLATION_GUIDE.md
- CHANGELOG.md
- QUICK_REFERENCE.md

Skill 只包含 AI 执行任务所需的信息，不包含过程文档。

---

## 示例结构

### 简单 skill
```
hello/
├── SKILL.md
```

### 中等复杂
```
pdf-editor/
├── SKILL.md
└── scripts/
    └── rotate_pdf.py
```

### 复杂 skill
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
