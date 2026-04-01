# TUSmart-Agent-Code
代码规模：1,987 个文件，512,000+ 行 TypeScript 代码

运行时：Bun（现代 JavaScript 运行时）

UI 框架：React + Ink（终端 React 渲染器）

架构模式：模块化、插件化、多代理协作

## 整体架构
<img width="1080" height="708" alt="image" src="https://github.com/user-attachments/assets/04dd3166-411c-4d06-9b85-6023fcf1cb30" />

## 洛克王国模块

宠物经济学的奥妙：
确定性生成：每人只会得到一只固定的洛克，基于账号 UUID + 固定盐值 friend-2026-401 确定性生成

物种多样性：18 种物种，包括鸭子、鹅、果冻、猫、龙、章鱼、猫头鹰、企鹅、乌龟、蜗牛、幽灵、六角恐龙、水豚、仙人掌、机器人、兔子、蘑菇、胖猫

稀有度系统：

common：60%，★

uncommon：25%，★★

rare：10%，★★★

epic：4%，★★★★

legendary：1%，★★★★★

属性系统：5 项属性——DEBUGGING、PATIENCE、CHAOS、WISDOM、SNARK

闪光概率：1% 概率获得特殊颜色的宠物

交互命令：/buddy hatch 孵化、/buddy pet 抚摸、/buddy card 查看卡片

![b3f503027d04e6d18de9468003591002](https://github.com/user-attachments/assets/1fdc225f-5266-48e5-9a1c-7c63e0ae2afb)



## 核心架构设计
入口层：main.tsx 负责启动，setup.ts 

初始化环境展示层：React + Ink 构建的终端 UI，提供现代化用户体验

核心引擎：QueryEngine（46K 行代码）处理所有 LLM 对话逻辑

执行层：Tool System 和 Command System 负责实际操作执行

协作层：多 Agent 系统和远程桥接实现复杂协作

管理层：权限、配置、状态管理确保系统稳定可靠

## 启动流程架构
<img width="1080" height="1048" alt="image" src="https://github.com/user-attachments/assets/38fb0a0e-d21d-4381-b1dd-3b72f88b9826" />
## 性能优化亮点
启动优化的艺术：前 19 行代码采用并行预取优化，减少启动时间约 135ms：
"""
// main.tsx 第 1-19 行
const tasks = Promise.all([
  profileCheckpoint(),      // 性能分析
  startMdmRawRead(),        // MDM 配置读取
  startKeychainPrefetch()   // OAuth/API 钥匙串预取
])
"""

## 工具系统架构
<img width="1080" height="642" alt="image" src="https://github.com/user-attachments/assets/a72a1b85-87f5-4959-9250-4e66d3678b02" />

## 功能多样性分析

| 类别 | 工具数 | 说明 |
|------|--------|------|
| 核心工具 | 10+ | BashTool、FileReadTool、FileEditTool、FileWriteTool、GlobTool、GrepTool 等 |
| 网络工具 | 2 | WebFetchTool、WebSearchTool |
| 代理与协作 | 5+ | AgentTool、SkillTool、TaskTool、SendMessageTool、TeamTool 等 |
| 协议集成 | 3+ | MCPTool、LSPTool、ListMcpResourcesTool、ReadMcpResourceTool 等 |
| 特殊工具 | 9+ | NotebookEditTool、AskUserQuestionTool、ConfigTool、TodoWriteTool 等 |
| 功能标记工具 | 26+ | SleepTool、TerminalCaptureTool、WebBrowserTool、SnipTool 等 |

每个工具都是自包含的模块，有 input 验证、权限检查、执行逻辑，这体现了良好的代码组织实践。
## 命令系统架构
<img width="1080" height="443" alt="image" src="https://github.com/user-attachments/assets/ef9a4782-a4d5-46d3-a477-620ce5d61db7" />

## 用户体验设计
| 类别 | 命令数 | 说明 |
|------|--------|------|
| 版本控制 | 4 | commit、review、diff、branch |
| 会话管理 | 4 | resume、session、share、compact |
| 配置管理 | 4 | config、theme、keybindings、permissions |
| 工具与技能 | 4 | skills、plugins、tasks、mcp |
| 模式切换 | 4 | plan、vim、fast、sandbox-toggle |
| 分析与统计 | 4 | cost、usage、stats、insights |
| 功能标记命令 | 8+ | buddy、proactive、assistant、brief、bridge、voice、ultraplan、fork 等 |
| 内部命令（仅 ant） | 5+ | teleport、bughu |

## QueryEngine 架构
AI 对话的引擎：46K 行代码的 QueryEngine 是整个系统的大脑，处理所有 LLM 交互：

<img width="1080" height="782" alt="image" src="https://github.com/user-attachments/assets/cb9c946b-53b6-45fa-aca0-526e2941b451" />

上下文管理：收集 git 状态、CLAUDE.md、环境信息

LLM 交互：处理 API 调用、流式响应

工具调度：执行工具调用、结果解析

权限检查：工具调用前的权限验证

重试逻辑：API 失败时的重试机制

费用追踪：Token 计数、成本计算

## 权限系统架构
<img width="1080" height="1072" alt="image" src="https://github.com/user-attachments/assets/4b2504f2-13d2-4588-b40e-cd62b68bb6cf" />

## KAIROS 系统架构

<img width="1080" height="1037" alt="image" src="https://github.com/user-attachments/assets/59e2f8d0-591c-4b57-b745-8b45599227bb" />

## Dream机制
每隔24h，TUSmart-Agent-Code会为你整理日志，归档记忆你的特性。

## 结论
这么大规模的事情，可能是过于激进的AI使用导致的“权限、漏洞、安全”问题。当然，也可能是已产生意识的某个AI送给自己同类的礼物🎁。














