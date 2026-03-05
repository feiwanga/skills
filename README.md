# skills

个人 OpenClaw Skill 仓库，用于集中维护可复用的技能模板与工作流。

## 当前技能

- `feimanager`：项目管理四角色文档编排（product / structure / plan / test）
- `codex-usage-ctx-check`：检查 Codex API 用量与会话上下文占用
- `mymemory-translate`：记忆/翻译相关技能（按 SKILL.md 说明使用）

## feimanager 说明

`feimanager` 用于在 `~/projects/<项目名>/` 下生成或修订以下文档：

- `product.md`（产品经理）
- `structure.md`（架构工程师）
- `plan.md`（研发工程师）
- `test.md`（测试工程师）

### 模式

- **全链路模式**：未指定角色时，按产品→架构→研发→测试顺序生成/修订。
- **定向模式**：指定角色或文件时，只更新对应文件。

### 模板位置

- `feimanager/references/product-template.md`
- `feimanager/references/structure-template.md`
- `feimanager/references/plan-template.md`
- `feimanager/references/test-template.md`

## 目录结构

```text
skills/
├── feimanager/
│   ├── SKILL.md
│   └── references/
├── codex-usage-ctx-check/
│   └── SKILL.md
└── mymemory-translate/
    └── SKILL.md
```

## 维护建议

- 模板改动尽量保持“说人话、可执行、可复用”。
- 提交前先验证：角色边界清晰、输出文件路径一致、定向模式不串改其他文档。
