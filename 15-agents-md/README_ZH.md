# 第十五课：AGENTS.md——给 AI 编码智能体的项目上下文

## 简介

新成员加入团队，你需要告诉他：怎么跑测试、代码风格、提交规范、项目结构——所有这些他才知道怎么干活。

`AGENTS.md` 就是给 AI 编码智能体的"入职文档"。它告诉智能体项目规则、命令、风格和边界。

本课介绍什么是 AGENTS.md、为什么重要、如何编写以及与类似标准的对比。

---

## ELI5：新员工入职资料包

新人第一天，你给他一个文件夹：

- 公司网络怎么连
- 代码在哪、怎么跑
- 测试怎么跑
- 提交代码的规范
- 不能碰的东西

没有这个文件夹，新人要到处问。有了，他能快速上手。

`AGENTS.md` 就是 AI 编码智能体的入职资料包。它告诉智能体"这里的事怎么干"。

---

## 什么是 AGENTS.md

`AGENTS.md` 是一个纯 Markdown 文件，放在项目根目录（或子目录）。它不是特殊格式、不是 JSON Schema——就是普通 Markdown，但 AI 编码智能体会自动检测并读取它。

### 历史

- **2025 年 8 月**：OpenAI、Amp、Google、Cursor、Factory 协作创建
- **2025 年 12 月**：贡献给 AAIF（Linux Foundation）
- **2026 年初**：60,000+ 仓库已采用

### 核心原则

- **纯 Markdown**：没有特殊格式，人类也能直接读
- **自动检测**：AI 编码智能体自动发现并读取
- **非侵入式**：不影响现有开发流程

---

## AGENTS.md 覆盖的六个核心领域

### 1. 命令（Commands）

告诉智能体怎么跑项目：

```markdown
## 命令
- 安装依赖：`poetry install`
- 运行测试：`poetry run pytest tests/`
- 运行服务：`poetry run uvicorn app:app --reload`
- 代码检查：`poetry run ruff check .`
- 格式化：`poetry run ruff format .`
```

**关键：** 包含完整命令行参数。不要说"跑测试"——说"跑 `poetry run pytest tests/`"。

### 2. 测试（Testing）

```markdown
## 测试
- 框架：pytest
- 位置：`tests/` 目录
- 命名：`test_<模块名>.py`
- 运行：`poetry run pytest tests/ -v`
- 覆盖率：`poetry run pytest --cov=app tests/`
```

### 3. 项目结构（Project Structure）

```markdown
## 项目结构
app/
  ├── api/        # REST API 端点
  ├── models/     # 数据模型
  ├── services/   # 业务逻辑
  └── config.py   # 配置
tests/
  ├── unit/       # 单元测试
  └── integration/ # 集成测试
```

### 4. 代码风格（Code Style）

```markdown
## 代码风格
- Python 3.11+
- 使用类型注解
- 遵循 PEP 8
- 工具：ruff（lint + format）
- 命名：snake_case（函数/变量），CamelCase（类）
```

### 5. Git 工作流（Git Workflow）

```markdown
## Git 工作流
- 分支策略：功能分支（`feature/描述`）
- 提交信息：Conventional Commits（`feat:`, `fix:`, `docs:`）
- PR 要求：至少 1 个审批，所有测试通过
```

### 6. 边界（Boundaries）

```markdown
## 边界
- 不要修改 `generated/` 目录——自动生成
- 不要提交 `.env` 文件
- 数据库迁移必须用 `alembic revision`
- 不要在代码中硬编码密钥
```

---

## Monorepo 中的分层 AGENTS.md

在 monorepo 中，可以有多个 AGENTS.md：

```
AGENTS.md                    # 根级别——全局规则
services/api/AGENTS.md       # API 服务专用规则
services/frontend/AGENTS.md  # 前端专用规则
services/ml-pipeline/AGENTS.md # ML 管道专用规则
```

智能体首先读取根级 AGENTS.md，然后根据修改的目录读取子级规则。

---

## AGENTS.md vs. 其他标准

| 标准 | 来源 | 用途 |
|------|------|------|
| **AGENTS.md** | 开放标准（AAIF/Linux Foundation） | 通用的 AI 编码智能体上下文 |
| **CLAUDE.md** | Anthropic（Claude Code） | Claude 编码智能体的项目指令 |
| **.cursorrules** | Cursor | Cursor AI 的规则 |
| **.github/copilot-instructions.md** | GitHub Copilot | Copilot 的自定义指令 |
| **GEMINI.md** | Google（Gemini CLI） | Gemini 编码智能体的指令 |

**关键区别：** AGENTS.md 是开放标准，所有 AI 编码智能体都能读取。其他是特定工具专有的。

---

## 最佳实践

### 1. 不超过 150 行

AGENTS.md 应该是精简的。太长浪费上下文窗口，智能体也不一定能读完。

### 2. 具体可执行

```
差："测试很重要"
好："运行 `poetry run pytest tests/ -v --tb=short`"
```

### 3. 用示例说话

```
差："使用 Conventional Commits"
好：提交信息格式：`<type>: <描述>`
    示例：`feat: add user authentication`
          `fix: resolve null pointer in API handler`
          `docs: update README with setup instructions`
```

### 4. 迭代改进

像代码一样对待 AGENTS.md。根据智能体的实际表现持续改进。

### 5. 包含"为什么"

```
"使用 `--strict` 模式运行 mypy，因为我们在生产中发现
未类型注解的代码经常引发 Bug。"
```

### 6. 视为代码

- 版本管理
- 通过 PR 修改
- 和其他代码一样审查

---

## 完整示例

```markdown
# Agent Engineer - Python Web App

## 命令
- 安装：`poetry install`
- 测试：`poetry run pytest tests/ -v`
- 运行：`poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000`
- Lint：`poetry run ruff check .`
- 格式化：`poetry run ruff format .`

## 测试
- 框架：pytest
- 位置：`tests/`
- 命名：`test_<模块>.py`
- 单元测试放 `tests/unit/`，集成测试放 `tests/integration/`

## 代码风格
- Python 3.11+，类型注解必填
- 遵循 PEP 8
- ruff 做 lint 和格式化
- snake_case（函数/变量），CamelCase（类）
- 函数不超过 50 行

## Git 工作流
- 功能分支：`feature/描述`
- 提交信息：Conventional Commits
- PR 需 1 个审批 + 所有测试通过

## 边界
- 不要修改 `generated/` 目录
- 不要提交 `.env`
- 数据库迁移用 `alembic revision --autogenerate`
- 不在代码中硬编码密钥
```

---

## AGENTS.md 不够用时

| 需求 | 更好的方案 |
|------|-----------|
| 动态工具调用 | 使用 MCP |
| 可复用工作流 | 使用 Skills（SKILL.md） |
| 跨智能体协调 | 使用编排系统 |

AGENTS.md 是项目上下文，不是工具定义、不是技能模块、不是编排逻辑。

---

## 核心要点

1. **AGENTS.md 是 AI 编码智能体的入职文档。** 告诉智能体项目规则、命令和边界。

2. **纯 Markdown，自动检测。** 所有主流 AI 编码智能体都能读取。

3. **六个核心领域：** 命令、测试、项目结构、代码风格、Git 工作流、边界。

4. **150 行以内。** 精简、具体、可执行。

5. **开放标准。** 不同于 CLAUDE.md、.cursorrules 等专有格式。

6. **视为代码。** 版本管理、PR 审查、持续迭代。

---

## 下一步是什么？

AGENTS.md 告诉智能体项目上下文。但 MCP 作为工具协议，还有什么值得深入了解的？下一课深入 MCP 底层机制。

[下一课：第十六课 - MCP 深度解析 -->](../16-mcp-deep-dive/README_ZH.md)
