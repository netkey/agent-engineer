# 第十九课：接下来去哪里——资源、实验与下一步

## 简介

课程结束了。现在你有了理论基础，接下来该做什么？

本课总结课程要点，提供学习路径、资源链接和社区入口，帮你从学习者变成建造者。

---

## ELI5：学开车

上完驾校课程不等于你是好司机。你还需要：
- 上路练习
- 遇到问题查资料
- 和其他司机交流经验
- 持续学习新交通规则

智能体开发同理。课程只是起点，真正的学习在动手实践中。

---

## 课程回顾

| 课 | 主题 | 核心概念 |
|----|------|----------|
| 01 | 什么是 AI 智能体？ | LLM + 工具 + 编排 = 智能体 |
| 02 | 智能体如何思考 | Token、上下文窗口、推理策略 |
| 03 | 工具 | 函数调用、工具设计、MCP |
| 04 | 设计模式 | ReAct、反思、规划、工具使用 |
| 05 | 记忆与上下文 | 短期/长期记忆、上下文管理 |
| 06 | 规划与推理 | 计划后执行、反应式、分层规划 |
| 07 | 多智能体 | 架构、通信、角色、协调 |
| 08 | 智能体 RAG | 检索 + 推理 + 自我修正 |
| 09 | 评估与测试 | 四大支柱、LLM-as-Judge、可观测性 |
| 10 | 护栏与安全 | 纵深防御、注入防御、人在回路 |
| 11 | 从原型到生产 | 评估门控、金丝雀发布、成本管理 |
| 12 | Vertex AI 与 ADK | 模型层、平台层、应用层 |
| 13 | 构建第一个智能体 | ADK 实战、工具、系统指令 |
| 14 | MCP 与 A2A | 工具协议、智能体间协议 |
| 15 | AGENTS.md | 项目上下文配置文件 |
| 16 | MCP 深度解析 | 架构、vs CLI、安全 |
| 17 | 智能体技能 | SKILL.md、渐进式披露 |
| 18 | 编排器 | 六种模式、最佳实践 |

---

## 四条学习路径

### 路径 1：构建你的第一个智能体

适合：刚开始动手的新手。

```
1. ADK Quickstart（官方文档）
2. Agent Starter Pack（生产模板）
3. 选择一个内部工具练手
4. 部署到 Agent Engine
```

### 路径 2：改进现有智能体

适合：已经有一个智能体，想提升质量。

```
1. 建立评估体系（黄金测试集 + LLM-as-Judge）
2. 优化系统指令
3. 审查和改进工具设计
4. 添加安全护栏
```

### 路径 3：规模化部署

适合：需要把智能体推向生产环境的工程师。

```
1. 部署到 Vertex AI Agent Engine
2. 配置 CI/CD 和评估门控
3. 设置金丝雀发布
4. 搭建监控和告警
```

### 路径 4：深入理论

适合：想更深入理解智能体原理的研究者。

```
1. 重读第 04-08 课（设计模式、规划、多智能体）
2. 阅读 Google Cloud 白皮书
3. 探索开源框架（LangGraph、CrewAI、AutoGen）
4. 实验新的推理策略
```

---

## Google Cloud 资源

- **[Google Cloud AI/ML Codelabs](https://codelabs.developers.google.com/?cat=AI)** —— 动手实践教程
- **[Vertex AI 文档](https://cloud.google.com/vertex-ai/docs)** —— 平台参考
- **[ADK 文档](https://google.github.io/adk-docs/)** —— 开发工具包参考
- **[Gemini API 文档](https://ai.google.dev/docs)** —— 模型 API 参考
- **[Google Cloud AI 官方博客](https://blog.google/technology/ai/)** —— 最新进展

### Agent Starter Pack

[Agent Starter Pack](https://github.com/GoogleCloudPlatform/agent-starter-pack) 是 Google 提供的生产就绪模板：

- CI/CD 流水线
- 评估体系
- 监控仪表板
- 安全护栏
- 成本管理

从模板开始比从零构建快得多。

---

## 社区

- **Google Cloud 社区论坛** —— 提问和分享
- **Stack Overflow**（标签：`google-cloud-ai`、`vertex-ai`） —— 技术问题
- **GitHub Issues**（[ADK](https://github.com/google/adk-python/issues)） —— Bug 报告和功能请求
- **Discord** —— 实时讨论

---

## Google Cloud 白皮书

| 白皮书 | 主题 |
|--------|------|
| [Introduction to Agents](https://cloud.google.com/whitepapers/introduction-to-agents) | 智能体基础概念 |
| [Agent Quality](https://cloud.google.com/whitepapers/agent-quality) | 评估和质量保障 |
| [Agent Tools and MCP](https://cloud.google.com/whitepapers/agent-tools-mcp) | 工具设计和 MCP |
| [Context Engineering](https://cloud.google.com/whitepapers/context-engineering) | 上下文管理策略 |
| [From Prototype to Production](https://cloud.google.com/whitepapers/agents-production) | 生产化最佳实践 |
| [Agents Companion](https://cloud.google.com/whitepapers/agents-companion) | 补充指南 |

---

## 开源框架

| 框架 | 用途 | 链接 |
|------|------|------|
| **ADK** | Google 智能体开发工具包 | [github.com/google/adk-python](https://github.com/google/adk-python) |
| **Agent Starter Pack** | 生产就绪模板 | [github.com/GoogleCloudPlatform/agent-starter-pack](https://github.com/GoogleCloudPlatform/agent-starter-pack) |
| **LangChain** | LLM 应用框架 | [github.com/langchain-ai/langchain](https://github.com/langchain-ai/langchain) |
| **LangGraph** | 图状工作流 | [github.com/langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) |
| **CrewAI** | 多智能体协作 | [github.com/crewAIInc/crewAI](https://github.com/crewAIInc/crewAI) |

**框架建议：** 不要花几周时间评估所有框架。选一个开始构建，有明确理由时再换。

---

## 新兴领域

这些领域正在快速发展，值得关注：

| 领域 | 描述 |
|------|------|
| **Computer Use Agents** | 智能体直接操作 GUI（点击、输入、滚动） |
| **Self-Evolving Agents** | 智能体从经验中学习并更新自身策略 |
| **Agentic Commerce** | 智能体自主完成购买、谈判等商业行为 |
| **Continuous Learning in Production** | 生产环境持续学习和自适应 |
| **Multi-Modal Agents** | 处理文本、图像、音频、视频的智能体 |
| **Agent Observability & Debugging** | 智能体行为可观测和调试工具 |

---

## 你的第一个项目

### 推荐的入门项目

| 项目 | 难度 | 涉及概念 |
|------|------|----------|
| **内部知识问答智能体** | 入门 | RAG、文档检索 |
| **工单分类智能体** | 入门 | 分类、工具调用 |
| **每日摘要智能体** | 中级 | 数据聚合、定时任务 |
| **代码审查助手** | 中级 | 代码分析、审查模式 |

### 项目检查清单

**部署前：**
- [ ] 有黄金测试集
- [ ] 安全护栏通过测试
- [ ] 错误处理覆盖所有工具
- [ ] 最大迭代次数已设置
- [ ] 系统指令经过审查

**部署中：**
- [ ] 使用金丝雀发布
- [ ] 监控指标已配置
- [ ] 告警阈值已设置
- [ ] 回滚流程已测试

**部署后：**
- [ ] 收集用户反馈
- [ ] 定期运行评估
- [ ] 追踪质量趋势
- [ ] 持续改进提示和工具

---

## 收藏资源

- [Vertex AI Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)
- [ADK Documentation](https://google.github.io/adk-docs/)
- [Agent Starter Pack](https://github.com/GoogleCloudPlatform/agent-starter-pack)
- [Google Cloud AI Codelabs](https://codelabs.developers.google.com/?cat=AI)
- [Gemini API Documentation](https://ai.google.dev/docs)

---

## 最后一句话

**动手做点什么。**

读完整课程不写一行代码，就像读完游泳手册不下水。打开编辑器，建个项目，跑起来。遇到不懂的回来查。这才是最好的学习方式。

---

**课程结束。** 祝构建顺利！
