# 第十三课：构建你的第一个智能体

## 简介

理论已经够了。这一课我们动手用 Google ADK 构建一个真实可运行的智能体。

你会学到：
- 项目结构和配置
- 定义智能体和工具
- 使用内置工具（Google Search）
- 本地运行和测试
- 运行评估

---

## ELI5：乐高套件

ADK 就像一盒乐高积木。你不需要自己造塑料块——所有标准件都在盒子里。你需要做的是：
1. 打开盒子，看看有什么零件
2. 按说明书拼出基础模型
3. 按自己想法改装

本课就是带你走完这三步。

---

## 前置条件

- **Python 3.9+**
- **ADK 已安装**：`pip install google-adk`
- **Google Cloud 项目**（用于 API 密钥或服务账号）
- **API 密钥**或 `gcloud` 认证

---

## 第 1 步：项目结构

创建项目目录：

```
my-first-agent/
├── main.py              # 智能体主代码
├── tools/
│   └── weather.py       # 自定义工具
├── prompts/
│   └── system.md        # 系统提示
└── requirements.txt     # 依赖
```

`requirements.txt`：
```
google-adk
```

---

## 第 2 步：定义智能体

在 `main.py` 中创建基础智能体：

```python
from adk.agents import LlmAgent

agent = LlmAgent(
    name="weather_assistant",
    model="gemini-2.0-flash",
    instruction="""你是天气助手。用户询问天气时，
    调用 weather_api 获取数据，然后用自然语言回复。
    温度单位用摄氏度。""",
)
```

---

## 第 3 步：创建函数工具

在 `tools/weather.py` 中：

```python
def get_weather(location: str, unit: str = "celsius") -> dict:
    """获取指定位置的当前天气。

    Args:
        location: 城市名，如 "Tokyo"、"London"
        unit: 温度单位，"celsius" 或 "fahrenheit"（默认 celsius）
    
    Returns:
        包含 temperature、condition、location 的字典
    """
    # 实际项目中这里调用天气 API
    # 这里用模拟数据
    return {
        "temperature": 18,
        "condition": "rainy",
        "location": location,
        "unit": unit
    }
```

把工具注册到智能体：

```python
from adk.tools import FunctionTool
from tools.weather import get_weather

weather_tool = FunctionTool(get_weather)
agent.tools = [weather_tool]
```

---

## 第 4 步：添加内置工具

ADK 支持 Google Search 等内置工具：

```python
from adk.tools import GoogleSearchTool

search_tool = GoogleSearchTool()
agent.tools = [weather_tool, search_tool]
```

现在智能体可以用 Google 搜索获取实时信息了。

---

## 第 5 步：本地运行

```bash
adk web
```

这会启动本地 Web UI，打开浏览器即可与智能体对话。

测试：
- "东京的天气怎么样？"
- "今天有什么科技新闻？"

---

## ADK 智能体类型详解

### LlmAgent（基础智能体）

最常用的智能体类型。基于 LLM 推理，动态决定调用哪些工具。

```python
from adk.agents import LlmAgent

agent = LlmAgent(
    name="assistant",
    model="gemini-2.0-flash",
    instruction="你是有用的助手。"
)
```

### SequentialAgent（顺序智能体）

按顺序执行子智能体，每个的输出传递给下一个。

```python
from adk.agents import SequentialAgent, LlmAgent

researcher = LlmAgent(
    name="researcher",
    model="gemini-2.0-flash",
    instruction="你是一个研究助手。搜索信息并总结。"
)

writer = LlmAgent(
    name="writer",
    model="gemini-2.0-flash",
    instruction="你是一个作家。基于研究结果撰写文章。"
)

editor = LlmAgent(
    name="editor",
    model="gemini-2.0-flash",
    instruction="你是一个编辑。审查并改进文章质量。"
)

pipeline = SequentialAgent(
    name="content_pipeline",
    sub_agents=[researcher, writer, editor]
)
```

### ParallelAgent（并行智能体）

同时执行多个子智能体，然后汇聚结果。

```python
from adk.agents import ParallelAgent, LlmAgent

python_reviewer = LlmAgent(
    name="python_reviewer",
    model="gemini-2.5-pro",
    instruction="审查 Python 代码的质量。关注性能和安全。"
)

js_reviewer = LlmAgent(
    name="js_reviewer",
    model="gemini-2.5-pro",
    instruction="审查 JavaScript 代码的质量。关注性能和安全。"
)

reviewer = ParallelAgent(
    name="code_reviewer",
    sub_agents=[python_reviewer, js_reviewer]
)
```

### LoopAgent（循环智能体）

迭代执行直到满足退出条件。

```python
from adk.agents import LoopAgent, LlmAgent

writer = LlmAgent(
    name="writer",
    model="gemini-2.0-flash",
    instruction="你是一个作家。根据要求写作。"
)

critic = LlmAgent(
    name="critic",
    model="gemini-2.5-pro",
    instruction="你是一个严格的评论家。审查文本并提供改进意见。"
)

iterative_writer = LoopAgent(
    name="iterative_writer",
    sub_agents=[writer, critic],
    max_iterations=3
)
```

---

## 多工具智能体

组合多个工具让智能体有更全面的能力：

```python
def search_products(query: str, limit: int = 10) -> list:
    """搜索产品目录，返回匹配的商品。"""
    # 模拟搜索
    return [{"name": "Widget A", "price": 9.99}, {"name": "Widget B", "price": 19.99}]

def get_user_profile(user_id: str) -> dict:
    """获取用户资料信息。"""
    return {"name": "Alice", "preferences": {"theme": "dark"}}

# 注册多个工具
agent.tools = [
    FunctionTool(get_weather),
    FunctionTool(search_products),
    FunctionTool(get_user_profile),
    GoogleSearchTool()
]
```

智能体会根据用户请求自动选择最合适的工具。

---

## 智能体团队

创建多个智能体协作完成复杂任务：

```python
# 根智能体（协调者）
root_agent = LlmAgent(
    name="team_coordinator",
    model="gemini-2.5-pro",
    instruction="""你是团队协调者。根据任务分配给合适的子智能体。
    - 研究任务交给研究智能体
    - 写作任务交给写作智能体
    - 代码任务交给代码智能体"""
)

# 子智能体作为工具
research_tool = AgentTool(research_agent)
writing_tool = AgentTool(writing_agent)
code_tool = AgentTool(code_agent)

root_agent.tools = [research_tool, writing_tool, code_tool]
```

### 子智能体 vs. 多工具的决策指南

| 场景 | 推荐方案 | 原因 |
|------|----------|------|
| 单个领域的多个操作 | 多工具 | 简单直接，上下文共享 |
| 多个独立领域 | 子智能体 | 关注点分离，各自专精 |
| 需要不同模型 | 子智能体 | 每个智能体可用不同模型 |
| 需要独立上下文 | 子智能体 | 各自管理自己的记忆 |

---

## 系统指令编写指南

好的系统指令是智能体成功的关键。

### 包含的内容

1. **角色定义**：智能体是谁，服务谁
2. **能力说明**：有哪些工具，何时使用
3. **行为约束**：不应该做什么
4. **输出格式**：如何组织回复
5. **错误处理**：出错时怎么办

### 示例

```markdown
你是 Acme Corp 的客服智能体。

职责：
- 处理订单查询、退货和产品问题
- 友好、专业、简洁

可用工具：
- lookup_order(order_id)：查询订单
- initiate_return(order_id, reason)：启动退货
- search_products(query)：搜索产品

规则：
- 访问订单前先验证客户身份
- 3 次尝试未解决则转接人工
- 不要虚构订单信息
- 不要提供超出标准政策的折扣
- 回复不超过 3 段

出错时：
- 临时错误（超时、500）：重试一次
- 永久错误（未找到、未授权）：向用户解释
- 不确定时：转接人工
```

### 常见错误

| 错误 | 问题 | 修复 |
|------|------|------|
| 太模糊 | "做一个好助手" | 具体说明什么是"好" |
| 太长 | 2000+ token 的系统提示 | 精简到核心指令 |
| 自相矛盾 | "简洁回答" + "提供详细解释" | 确定优先级 |
| 遗漏约束 | 没说不该做什么 | 添加负面约束 |
| 重复上下文 | 同样的规则说了 3 遍 | 说一次，说清楚 |

---

## 初学者常见错误

### 1. 工具太多
起步用 3-5 个精心设计的工具，不要一开始就堆 50 个。

### 2. 工具描述不清晰
模型靠描述决定用哪个工具。描述模糊 = 选择错误。

### 3. 忽略错误处理
工具会失败。确保智能体知道失败后该怎么办。

### 4. 没设最大迭代次数
循环智能体必须设 `max_iterations`，否则可能无限循环。

### 5. 不测试边缘情况
只测试"正常"输入，不测试空输入、超长输入、恶意输入。

### 6. 系统提示没写好
花时间在系统指令上。它可能是 50% 和 95% 效果的差别。

### 7. 不做评估
没有量化指标，你不知道改变更好还是更糟。

---

## ADK CLI 命令

| 命令 | 用途 |
|------|------|
| `adk web` | 启动本地 Web UI 测试 |
| `adk run` | 运行智能体 |
| `adk eval` | 运行评估 |
| `adk deploy` | 部署到指定目标 |

---

## 心智模型：智能体运行流程

```
用户输入
    ↓
系统指令 + 工具定义 + 对话历史
    ↓
LLM 推理（思考该做什么）
    ↓
    ├→ 直接回复 → 返回用户
    └→ 工具调用 → 执行工具 → 结果返回 LLM
                                      ↓
                              决定下一步（循环）
                                      ↓
                              直到完成并回复用户
```

---

## 核心要点

1. **动手实践是最好的学习。** 读十课不如写一个智能体。

2. **从 LlmAgent 开始。** 它是最通用、最常用的智能体类型。

3. **工欲善其事必先利其器。** 工具设计比工具数量重要。

4. **系统指令决定行为上限。** 花最多的时间写好系统指令。

5. **设好安全边界。** 最大迭代次数、错误处理、权限控制缺一不可。

6. **评估要趁早。** 即使只有 5 个测试用例，也比没有强。

---

## 下一步是什么？

智能体需要和外部工具及其他智能体通信。下一课我们来看 MCP 和 A2A 这两个开放标准协议。

[下一课：第十四课 - 智能体协议——MCP 与 A2A -->](../14-agent-protocols-mcp-and-a2a/README_ZH.md)
