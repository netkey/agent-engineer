# Agent Engineer —— 面向软件工程师的 AI 智能体课程

学习 AI 智能体的核心基础，以及如何借助 Google Cloud AI 构建智能体。

## 适合哪些人？

适合想了解 AI 智能体是什么、如何运作以及如何构建的软件工程师。无需 AI/ML 背景——只需好奇心和一定的 Python 知识。

## 课程概览

本课程分为三个部分：

**第一部分：基础（101）** —— 理解 AI 智能体的核心概念。这些课程与平台无关，专注于建立你的思维模型。

**第二部分：构建与上线（201）** —— 使用 Google Cloud AI、Vertex AI 以及 Agent Development Kit（ADK）将基础知识付诸实践。

**第三部分：深度专题（301）** —— 深入探讨真实世界智能体开发中的重要话题。

## 课程目录

### 第一部分：基础知识

| 序号 | 课程 | 你将学到 |
|---|--------|-------------------|
| 01 | [什么是 AI 智能体？](./01-what-are-ai-agents/README_ZH.md) | 宏观视角——智能体是什么、为何重要、何时使用 |
| 02 | [智能体如何思考](./02-how-agents-think/README_ZH.md) | LLM 作为推理引擎——模型如何规划、决策和生成 |
| 03 | [工具——给智能体一双手](./03-tools-giving-agents-hands/README_ZH.md) | 函数调用、工具设计，以及将智能体连接到现实世界 |
| 04 | [智能体设计模式](./04-agentic-design-patterns/README_ZH.md) | ReAct、反思、规划及其他核心模式 |
| 05 | [记忆与上下文](./05-memory-and-context/README_ZH.md) | 智能体如何记忆——会话、上下文窗口与长期记忆 |
| 06 | [规划与推理](./06-planning-and-reasoning/README_ZH.md) | 智能体如何分解复杂任务并做出决策 |
| 07 | [多智能体系统](./07-multi-agent-systems/README_ZH.md) | 当单个智能体不够用时——协调、委派与团队协作 |
| 08 | [智能体 RAG](./08-agentic-rag/README_ZH.md) | 超越基础检索——会搜索、评估和精化的智能体 |
| 09 | [评估与测试智能体](./09-evaluating-and-testing-agents/README_ZH.md) | 如何判断智能体是否真正有效——指标、评估与可观测性 |
| 10 | [护栏与安全](./10-guardrails-and-safety/README_ZH.md) | 保持智能体可信赖——安全、对齐与负责任 AI |

### 第二部分：构建与上线

| 序号 | 课程 | 你将学到 |
|---|--------|-------------------|
| 11 | [从原型到生产](./11-from-prototype-to-production/README_ZH.md) | 从演示到部署的旅程——CI/CD、上线流程与运维 |
| 12 | [Vertex AI 与 ADK 入门](./12-getting-started-with-vertex-and-adk/README_ZH.md) | 面向智能体的 Google Cloud AI 技术栈——现有能力与整体结构 |
| 13 | [构建你的第一个智能体](./13-building-your-first-agent/README_ZH.md) | 动手实践——用 ADK 逐步构建可运行的智能体 |
| 14 | [智能体协议——MCP 与 A2A](./14-agent-protocols-mcp-and-a2a/README_ZH.md) | 智能体如何通过开放标准与工具及彼此通信 |

### 第三部分：深度专题

| 序号 | 课程 | 你将学到 |
|---|--------|-------------------|
| 15 | [AGENTS.md](./15-agents-md/README_ZH.md) | 用标准配置文件为 AI 编码智能体提供项目上下文 |
| 16 | [MCP 深度解析](./16-mcp-deep-dive/README_ZH.md) | MCP 的底层运作机制、MCP 与 CLI 工具的对比，以及安全注意事项 |
| 17 | [智能体技能](./17-agent-skills/README_ZH.md) | 将可复用的领域专业知识打包为便携的技能模块 |
| 18 | [编排器](./18-orchestrators/README_ZH.md) | 管理智能体控制流——模式、框架与最佳实践 |
| 19 | [接下来去哪里](./19-where-to-go-from-here/README_ZH.md) | 资源、实验项目、社区与下一步 |

## 如何使用本课程

- **按顺序阅读**：如果你是智能体领域的新手，每节课都建立在前一节的基础上。
- **跳跃阅读**：如果你已掌握基础知识，每节课都足够独立，可以单独阅读。
- **跟随链接**：通过链接前往官方文档、实验项目和教程进行实践。我们有意链接到有人维护的外部资源，而非重复那些容易过时的 API 文档或代码示例。

## 课程理念

本课程遵循以下原则：

- **类比优先**：在深入技术细节之前，先用日常比喻解释复杂概念。
- **基础重于框架**：先理解"为什么"，再学"怎么做"。框架会变，核心思想常青。
- **链接而非重复**：对于 API 参考、代码示例和安装说明，我们指向官方 Google Cloud 文档和实验项目，确保内容聚焦于概念，且始终呈现最新信息。
- **诚实面对权衡**：每一个架构选择都有代价，我们会呈现两面。

## 前提条件

- 基本 Python 知识（函数、类、HTTP 请求）
- Google Cloud 账号（[免费试用](https://cloud.google.com/free)）
- 熟悉 REST API 和 JSON

## 扩展资源

- [Google Cloud AI 文档](https://cloud.google.com/ai)
- [Vertex AI 文档](https://cloud.google.com/vertex-ai/docs)
- [Agent Development Kit（ADK）文档](https://google.github.io/adk-docs/)
- [Google Cloud AI 实验项目](https://codelabs.developers.google.com/?cat=AI)
- [Gemini API 文档](https://ai.google.dev/docs)

## 贡献

发现错别字？有改进建议？欢迎提交 PR 或 Issue，详见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

## 许可证

本项目遵循 Apache 2.0 许可证，详见 [LICENSE](./LICENSE) 文件。
