# 第十二课：Vertex AI 与 ADK 入门——Google Cloud AI 技术栈

## 简介

前十一课建立了智能体的概念基础。从这一课开始，我们进入动手实践部分——使用 Google Cloud AI 构建和部署真实智能体。

本课全景概览：Google Cloud AI 技术栈有哪些组件、各自负责什么、如何协同工作。

---

## ELI5：木工工作坊

想象一个木工工作坊：

- **木材** —— 原始材料，决定做什么产品（模型：推理能力）
- **手工工具** —— 锯子、刨子、凿子，处理具体操作（工具：执行能力）
- **工作台** —— 固定平台，提供稳定工作环境（Agent Engine：托管平台）
- **电动工具套装** —— 标准化电源接口，即插即用（ADK：开发工具包）
- **质检仪** —— 检查产品质量（评估：质量保障）
- **安全护目镜** —— 保护操作者（护栏：安全保障）

你不需要所有工具来做一个简单的小鸟屋。但要做一套家具，你需要整个工作坊。智能体同理——简单任务用轻量组件，复杂系统需要完整技术栈。

---

## Google Cloud AI 技术栈全景

```
┌──────────────────────────────────────────────────────┐
│                    应用层                             │
│  你的智能体应用（用 ADK 构建）                        │
├──────────────────────────────────────────────────────┤
│                    平台层                             │
│  Vertex AI Agent Engine（托管部署）                   │
│  Vertex AI RAG Engine（检索增强）                     │
│  Model Armor（安全过滤）                              │
├──────────────────────────────────────────────────────┤
│                    模型层                             │
│  Gemini 2.5 Pro ── 复杂推理                           │
│  Gemini 2.0 Flash ── 均衡选择                       │
│  Gemini 2.0 Flash Lite ── 高吞吐量                    │
├──────────────────────────────────────────────────────┤
│                    基础设施层                         │
│  Google Cloud（GCE, GKE, Cloud Run, Storage...）     │
└──────────────────────────────────────────────────────┘
```

---

## Gemini 模型

### 模型谱系

```
轻量/快速/便宜                              重量/智能/贵
|----------------------------------------------------------|
Gemini Flash Lite          Gemini Flash          Gemini 2.5 Pro
（高吞吐量）               （均衡）               （复杂推理）
```

**类比：**
- **Flash Lite** = 自行车 —— 快、便宜、适合短距离
- **Flash** = 汽车 —— 平衡速度和能力
- **2.5 Pro** = 卡车 —— 能拉重货，但更慢更贵

### 模型能力

| 模型 | 上下文窗口 | 最适合 |
|------|-----------|--------|
| Gemini 2.5 Pro | 100 万 token | 复杂推理、代码生成、多步骤分析 |
| Gemini 2.0 Flash | 100 万 token | 大多数智能体任务、工具使用 |
| Gemini 2.0 Flash Lite | 100 万 token | 分类、提取、简单问答 |

### 多模态

所有 Gemini 模型都支持多种输入类型：

| 输入类型 | 示例 |
|----------|------|
| 文本 | 提示、文档、代码 |
| 图像 | 照片、图表、截图 |
| 音频 | 语音转录、音频文件 |
| 视频 | 视频分析、动作识别 |
| PDF | 文档理解、表格提取 |

### 特殊能力

- **上下文缓存（Context Caching）** —— 缓存重复发送的前缀内容（系统提示、工具定义），减少延迟和成本
- **Google Search Grounding** —— 搜索网络获取最新信息，内置事实核查
- **批量预测** —— 异步处理大批量请求
- **AutoSxS 评估** —— 自动对比评估两个模型/提示版本

---

## Vertex AI 平台

Vertex AI 是 Google Cloud 的托管 AI 平台，提供：

### 模型管理
- **Model Garden** —— 浏览和部署预训练模型
- **模型版本管理** —— 追踪不同模型版本的效果
- **微调** —— 用自有数据定制模型

### 推理服务
- **在线预测** —— 实时模型调用
- **批量预测** —— 大批量离线处理
- **上下文缓存** —— 自动缓存重复上下文

### 评估
- **AutoSxS** —— 自动并排对比评估
- **Vertex AI Evaluation** —— 托管评估服务

### RAG
- **Vertex AI RAG Engine** —— 托管 RAG 基础设施
- **Vertex AI Search** —— 企业搜索服务

---

## Agent Development Kit（ADK）

ADK 是 Google 开源的代码优先工具包，用于构建智能体。

### 核心特征

- **开源** —— 代码在 [github.com/google/adk-python](https://github.com/google/adk-python)
- **多语言** —— 支持 Python、Java 等
- **模型无关** —— 可用 Gemini，也可用其他模型
- **部署无关** —— 可部署到 Agent Engine、Cloud Run、GKE 或本地

### ADK 智能体类型

| 类型 | 用途 | 模式 |
|------|------|------|
| **LlmAgent** | 基础智能体，基于 LLM 推理 | 动态、反应式 |
| **SequentialAgent** | 按顺序执行子智能体 | 计划后执行（流水线） |
| **ParallelAgent** | 并行执行多个子智能体 | 扇出/汇聚 |
| **LoopAgent** | 迭代执行直到满足条件 | 迭代优化 |

### ADK 工具支持

| 工具类型 | 描述 |
|----------|------|
| **FunctionTool** | 将 Python 函数定义为工具 |
| **MCP Tools** | 通过 MCP 协议连接外部工具 |
| **OpenAPI Tools** | 从 OpenAPI 规范自动生成工具 |
| **内置工具** | Google Search、代码执行等 |
| **SkillToolset** | 加载 SKILL.md 技能模块 |

### ADK 技能（Skills）

技能是打包的领域专业知识，通过 SKILL.md 文件定义：

```
my-skill/
├── SKILL.md          # 技能定义
├── references/       # 参考文档
├── assets/           # 资源文件
└── scripts/          # 脚本文件
```

**渐进式披露：**
- **L1 元数据**（约 100 token）—— 名称、描述，用于决定是否加载
- **L2 指令**（2,000-5,000 token）—— 详细操作指南
- **L3 资源**（可变）—— 参考文档、脚本、模板

ADK 只在需要时加载完整技能，而不是始终占用上下文窗口。

---

## Agent Engine

[Vertex AI Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview) 是托管的智能体部署平台。

### 它管理什么

- **生命周期** —— 部署、启动、停止、重启
- **会话管理** —— 自动存储和检索会话状态
- **自动扩展** —— 根据流量自动调整实例数
- **监控** —— 内置指标和日志集成
- **安全** —— IAM 权限控制

### 部署选项对比

| 部署方式 | 运维负担 | 扩展性 | 最适合 |
|----------|----------|--------|--------|
| **Agent Engine** | 低（托管） | 自动 | 生产智能体 |
| **Cloud Run** | 中 | 自动 | 自定义智能体服务 |
| **GKE** | 高 | 手动配置 | 大规模复杂部署 |
| **本地** | 低 | 无 | 开发/测试 |

---

## 快速开始

### 1. 安装 ADK

```bash
pip install google-adk
```

### 2. 认证

```bash
# 使用 Google Cloud CLI
gcloud auth application-default login
```

或使用 API 密钥（开发用途）。

### 3. 创建简单智能体

```python
from adk.agents import LlmAgent

agent = LlmAgent(
    name="assistant",
    model="gemini-2.0-flash",
    instruction="你是友好的助手。简洁回答问题。"
)
```

### 4. 运行

```bash
adk web
```

这启动本地 Web UI，可以对话测试智能体。

---

## 服务选择决策树

```
你需要构建智能体吗？
  │
  +-- 是 --> 你需要代码优先控制吗？
  │            │
  │            +-- 是 --> 使用 ADK
  │            │           │
  │            │           +-- 需要托管部署？
  │            │           │    │
  │            │           │    +-- 是 --> ADK + Agent Engine
  │            │           │    +-- 否 --> ADK + Cloud Run/本地
  │            │
  │            +-- 否 --> 需要无代码构建？
  │                        │
  │                        +-- 是 --> Agent Builder（控制台）
  │
  +-- 否 --> 只需要模型 API？
              │
              +-- 是 --> 直接使用 Vertex AI Gemini API
```

---

## 课程到服务映射

| 课程 | 涉及服务 |
|------|----------|
| 13. 构建第一个智能体 | ADK（LlmAgent、FunctionTool） |
| 14. 协议（MCP/A2A） | ADK MCPToolset、Apigee |
| 15. AGENTS.md | 项目配置（与平台无关） |
| 16. MCP 深度解析 | ADK MCP Tools、Apigee 网关 |
| 17. 智能体技能 | ADK SkillToolset |
| 18. 编排器 | ADK（SequentialAgent、ParallelAgent、LoopAgent） |
| 19. 接下来去哪里 | 所有服务的进阶资源 |

---

## 核心要点

1. **Google Cloud AI 是分层架构。** 模型层 → 平台层 → 应用层，每层有明确职责。

2. **Gemini 有三种规格。** 根据任务复杂度选择：Lite（简单）、Flash（均衡）、Pro（复杂）。

3. **ADK 是代码优先工具包。** 开源、多语言、模型无关，提供智能体类型、工具和技能系统。

4. **Agent Engine 是托管部署平台。** 处理生命周期、会话、扩展和监控。

5. **上下文缓存降低成本。** 对重复前缀（系统提示、工具定义）使用缓存减少 token 消耗。

6. **从简单开始。** 先用 ADK 本地开发，需要生产部署时再接入 Agent Engine。

---

## 下一步是什么？

理论到此为止。下一课我们动手——用 ADK 逐步构建第一个可运行的智能体。

[下一课：第十三课 - 构建你的第一个智能体 -->](../13-building-your-first-agent/README_ZH.md)
