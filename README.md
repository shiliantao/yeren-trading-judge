# yeren-trading-judge（野人哥交易体系 · 股票判断 Skill）

一个面向 AI Agent 的 **A 股短线/波段交易判断技能包**（Agent Skill）。它将《野人哥交易实战笔记》的完整方法论固化为结构化工作流，让 AI 在回答"这只股票能不能买 / 要不要卖 / 仓位多少 / 帮我复盘"时，按统一框架输出**可落地、带数值、有防守位**的判断。

> ⚠️ **免责声明**：本项目为交易方法论的工程化整理，仅供学习与研究使用，不构成任何投资建议。股市有风险，入市需谨慎，据此操作风险自担。

---

## 体系核心

- 短线炒的是**情绪 + 流动性 + 资金合力**，不是业绩；
- **题材高度 = 政策/事件级别 × 板块容量 × 资金合力 × 情绪周期位置**；
- K 线是资金博弈的"脚印"，是结果不是原因——**选对周期比选对票重要**；
- 节奏口诀：**冰点试错 → 启动确认加 → 主升做分歧 → 高潮减 → 退潮空仓**；
- **控制回撤 × 只做模式内 = 稳定盈利的基础**，技术永远排第二位。

## 判断工作流（五步）

```
第 0 步  取数        获取行情/连板梯队/涨跌停数据（可对接 iFinD 等数据源）
第 1 步  定情绪周期   冰点/启动/主升/高潮/退潮 → 决定总仓位上限与动作基调
第 2 步  定个股地位   空间龙/中军/补涨龙/穿越龙/老龙/跟风 → 无地位直接放弃
第 3 步  匹配买卖点   四大买点逐条核对前置条件；持仓校验锚定点
第 4 步  防守与仓位   盈亏比 ≥3:1 前置；仓位金字塔；具体止损价位；防腰斩五问
第 5 步  输出结论     结构化模板 + 风险提示
```

输出模板示例：

```
【情绪周期】当前处于 X 期（依据：连板高度/跌停家数/梯队/中军表现），动作基调：……，总仓位上限 X%
【个股地位】XX 属于 XX 板块（主线/非主线），角色：空间龙/中军/补涨/跟风，地位依据：……
【买卖点判断】当前匹配/不匹配 XX 买点（逐条核对前置条件）；持仓者：锚定点 X 元，破则走
【操作结论】买/卖/持有/空仓；仓位 X%；防守位 X 元（-X%）；盈亏比 X:1
【风险提示】……（方法论参考，不构成投资建议）
```

## 文件结构

```
yeren-trading-judge/
├── SKILL.md                    # 技能主入口：触发条件、五步工作流、输出模板、铁律
├── install.md                  # 供 Codex 等 Agent 读取的安装说明（给链接即装）
├── references/
│   ├── cycle.md                # 情绪周期五阶段量化判定、仓位动作表、四大节点、鱼尾识别
│   ├── selection.md            # 主线五步法、真龙头三硬指标、角色体系、审美标准
│   ├── signals.md              # 主力四阶段、量价六原则、震仓vs出货、四大买点、卖点止损
│   └── discipline.md           # 仓位金字塔、止损铁律、防腰斩五问、复盘SOP、三大经典战法
└── yeren-trading-judge.skill   # 打包好的技能安装包（zip 格式）
```

## 安装与使用

### Kimi Work

方式一（推荐）：将本仓库目录复制到技能目录：

```
git clone https://github.com/shiliantao/yeren-trading-judge.git
# Windows：复制到 D:\KimiData\daimon-share\daimon\skills\yeren-trading-judge\
```

方式二：下载 `yeren-trading-judge.skill` 安装包，在 Kimi Work 中导入。

安装后，直接提问即可触发，例如：

- "帮我看看 XXX 现在能不能买"
- "我持有 XXX，成本 XX 元，该怎么处理"
- "今天市场情绪处于什么阶段"
- "按体系帮我复盘今天的操作"

配合 iFinD 插件可自动获取实时行情、连板梯队、涨跌停数据，完成第 0 步取数。

### OpenAI Codex（给链接即装）

**最省事：把下面这句话发给 Codex**，它会自己读安装说明并执行（安装说明见 [install.md](install.md)）：

```
Read https://github.com/shiliantao/yeren-trading-judge/blob/main/install.md and follow the instructions to install the skill.
```

手动安装也很一行：

```bash
# 用户级（所有项目可用）
git clone https://github.com/shiliantao/yeren-trading-judge.git ~/.agents/skills/yeren-trading-judge

# Windows PowerShell
git clone https://github.com/shiliantao/yeren-trading-judge.git "$env:USERPROFILE\.agents\skills\yeren-trading-judge"

# 仓库级（仅当前项目）
mkdir -p .agents/skills && git clone https://github.com/shiliantao/yeren-trading-judge.git .agents/skills/yeren-trading-judge
```

装好后用 `$yeren-trading-judge` 显式调用，或直接问股票问题自动触发（如看不到新技能，重启 Codex 或运行 `/skills` 确认）。

### Claude Code / 其他支持 Agent Skill 的平台

将仓库目录放入对应平台的 skills 目录（如 `~/.claude/skills/yeren-trading-judge/`），平台会自动识别 `SKILL.md` 的 frontmatter 并注册触发条件。

### 通用用法（任意 LLM）

不具备 Skill 机制时，直接把 `SKILL.md` 与 `references/` 四个文件的内容粘贴进系统提示词或上下文，即可让模型按此框架分析。

## 体系要点速览

| 模块 | 关键规则 |
|---|---|
| 情绪周期 | 冰点（连板≤3板+跌停≥10家）空仓试错；主升推仓 20%~40%；退潮无条件清仓 |
| 选股 | 只做主线内的空间龙/先锋/核心中军；真龙头需同时满足最高板+板块助攻+情绪标杆 |
| 买点 | 波段买点（20日线拐头）/ 主升首分歧低吸（最优）/ 弱转强（竞价高开2%~5%带量）/ B点（回撤15%~30%地量承接） |
| 止损 | 单笔 -5%~-7% 无条件砍；破锚（分歧日最低价/大阳半分位/5日线）立即走；严禁补仓摊成本 |
| 仓位 | 试错 5%~10% → 确认 20%~30% → 主仓 ≤50%；同时持仓 ≤2~3 只；连亏 2~3 笔强制降仓 |
| 盈亏比 | 潜在盈利÷潜在止损 ≥3:1 才出手，否则放弃 |
| 复盘 | 每日五步 SOP：涨跌停复盘→持仓校验→异动扫描→交易日志→周期定性 |

## 适用范围与边界

- ✅ 适用：A 股短线/波段，题材情绪驱动的交易决策与复盘
- ❌ 不适用：长线价值投资、美股/港股（规则不同）、纯基本面定价问题

## 来源与致谢

方法论整理自《野人哥交易实战笔记》（直播、连线、答疑、复盘笔记的合集），原书核心理念："保住本金是第一原则，慢就是快。"
