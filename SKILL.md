---
name: effective-skills
description: 设计高质量 Agent Skills 的最佳实践。当需要创建新 skill、优化现有 skill、或遇到 skill 效果不佳时使用。包括：Gotchas 常见失败点、设计原则、描述撰写技巧、渐进式披露策略。注意：技术实现细节请参考 skill-creator。
---

# Effective Skills Design

## ⚠️ Gotchas (最重要！)

这是从真实失败中总结的最高价值信息。

### 1. Description 是给模型用的，不是给人看的

```yaml
# ❌ 错误：太笼统
description: "帮助编写 Python 代码"

# ✅ 正确：具体说明触发时机
description: "Python 代码编写、调试和重构。当需要：写新功能、debug、代码审查、重构时触发。"
```

**关键**：把"什么时候用"的信息放在 description，而不是 body。

### 2. 别写显而易见的东西

Claude 已经很聪明了。你需要提供的是：
- 你的特定领域知识
- 常见失败点和解决方案
- 独特的工作流

```markdown
# ❌ 冗余
- 使用 Python 的 def 关键字定义函数
- 函数可以有参数和返回值

# ✅ 有价值
- 这个项目的函数命名规范：snake_case
- 常用函数在 utils.py 中，避免重复定义
```

### 3. 验证！验证！验证！

代码开发类 skill 必须在最后添加验证步骤：
```markdown
- [ ] Step 3: 编写功能代码
- [ ] Step 4: 运行语法检查 ← 必须
- [ ] Step 5: 执行测试 ← 必须
```

### 4. 避免过度限定 (Avoid Railroading)

给 Claude 足够的信息，但保持灵活性：

```markdown
# ❌ 太死板
必须先读 A，再读 B，最后写 C

# ✅ 有弹性
建议顺序：A → B → C，但根据实际情况调整
```

---

## 🎯 Design Principles

### Concise is Key

上下文窗口是公共资源。默认假设 Claude 已经很聪明，只添加它不具备的上下文。

**检验标准**：这段信息是否值得占用 token？

### Set Appropriate Degrees of Freedom

根据任务类型决定自由度：

| 任务类型 | 自由度 | 示例 |
|---------|--------|------|
| 文本创作 | 高 | "用活泼的语气写..." |
| 有固定模式 | 中 | "用这个模板，参数可调" |
| 脆弱操作 | 低 | "必须按顺序执行这 5 步" |

### Progressive Disclosure

三层加载：
1. **Metadata** (name + description) - 始终在上下文
2. **SKILL.md body** - skill 触发时加载
3. **references/** - 按需加载

---

## 📁 Directory Structure

```
skill-name/
├── SKILL.md           # 必需：元数据 + 核心指令
├── scripts/           # 可选：可执行脚本
├── references/        # 可选：按需加载的文档
└── assets/           # 可选：输出用的资源文件
```

详细结构说明见 [references/structure.md](references/structure.md)

---

## 🔄 Common Patterns

### Pattern 1: 带参考文档的主文件

```markdown
# SKILL.md
## 快速开始
[核心指令]

## 详细指南
- 高级用法 → [references/advanced.md](references/advanced.md)
- 常见问题 → [references/faq.md](references/faq.md)
```

### Pattern 2: 按领域组织

```
big-query/
├── SKILL.md
└── references/
    ├── finance.md
    ├── sales.md
    └── product.md
```

### Pattern 3: 带配置的 Setup

首次使用时询问或读取 config.json：

```markdown
如果 config.json 不存在，请询问用户：
- API 密钥
- 偏好设置
```

---

## 📦 Distribution

### 方式 1: 放入 repo
```
./claude/skills/  # 项目级 skill
```

### 方式 2: 发布到 Marketplace
- 先在 sandbox 测试
- 验证有实际需求后再提交
- 做好 curation（质量把控）

详见 [references/distribution.md](references/distribution.md)

---

## 🔗 Related Skills

- **skill-creator** - 技术实现：如何创建、初始化、打包 skill
- **auto-todo** - 多步骤任务执行框架

需要技术实现细节时使用 skill-creator，需要设计指导时使用本 skill。
