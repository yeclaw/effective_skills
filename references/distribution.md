# Skill 分发指南

## 方式 1: 放入 Repo (小型团队)

```
./.claude/skills/           # 项目级
~/.claude/skills/           # 用户级
```

**优点**：
- 简单直接
- 版本控制
- 团队共享

**缺点**：
- 每个 repo 都添加上下文
- 难以为大量 repo 分发

---

## 方式 2: Marketplace (规模化)

### 上传流程

1. **开发阶段**：在本地或 sandbox 测试
2. **初步验证**：确保有实际使用需求
3. **提交 PR**：移动到 marketplace 目录

### Curation 原则

**发布前检查**：
- [ ] 是否有清晰的 description？
- [ ] 是否有 Gotchas（常见失败点）？
- [ ] 是否避免显而易见的内容？
- [ ] 是否有实际用例验证？

**质量标准**：
- 独特的领域知识 > 通用知识
- 真实失败经验 > 理论推导
- 简洁 > 冗长

---

## 依赖管理

Skill 可以依赖其他 skill：

```
skill-a/           # 上传 skill
skill-b/           # 被依赖的 skill
```

使用时：
```markdown
# 在 skill-a 中
要执行 X，请先使用 skill-b
```

模型会自动调用已安装的依赖 skill。

---

## 测量与迭代

### 追踪使用

可以用 PreToolUse hook 记录 skill 使用情况：

```python
# 伪代码
def pre_tool_use(tool_name, tool_input):
    if tool_name == "SkillLoader":
        log_skill_usage(tool_input["skill_name"])
```

### 指标

- 使用频率
- 触发准确度（是否在正确场景触发）
- 用户反馈

### 迭代循环

1. 真实任务中使用
2. 发现低效或失败
3. 更新 SKILL.md 或 resources
4. 重新测试

---

## 常见问题

**Q: 什么时候该创建新 skill？**
A: 当某个领域的知识或工作流经常重复，且现有 skills 无法覆盖。

**Q: skill 太长怎么办？**
A: 拆分到 references/，用渐进式披露。

**Q: 如何处理敏感信息？**
A: 使用 config.json，添加 .gitignore 忽略敏感配置。
