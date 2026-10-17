# yeren-trading-judge 安装说明（供 AI Agent 读取执行）

> 本文件面向 Codex 等 AI Agent：当用户让你"安装这个技能"时，按以下步骤执行。
> 人类用户请直接看 [README.md](README.md)。

## 技能信息

- 名称：`yeren-trading-judge`（野人哥交易体系 · A 股股票判断）
- 仓库：`https://github.com/shiliantao/yeren-trading-judge`
- 结构：仓库根目录即技能目录（`SKILL.md` 在根部，`references/` 为参考文件）
- 纯指令型技能，无脚本、无网络请求、无需任何密钥，可放心安装

## 安装步骤（Codex）

### 方式一：用户级安装（推荐，所有项目可用）

```bash
git clone https://github.com/shiliantao/yeren-trading-judge.git ~/.agents/skills/yeren-trading-judge
```

Windows（PowerShell）：

```powershell
git clone https://github.com/shiliantao/yeren-trading-judge.git "$env:USERPROFILE\.agents\skills\yeren-trading-judge"
```

### 方式二：仓库级安装（仅当前项目可用）

```bash
mkdir -p .agents/skills
git clone https://github.com/shiliantao/yeren-trading-judge.git .agents/skills/yeren-trading-judge
```

### 安装后验证

1. 确认 `~/.agents/skills/yeren-trading-judge/SKILL.md`（或项目级对应路径）存在；
2. 重启 Codex 或运行 `/skills` 查看技能已被发现；
3. 显式调用测试：`$yeren-trading-judge 帮我分析当前市场处于情绪周期的哪个阶段`。

## 卸载

删除对应目录即可：

```bash
rm -rf ~/.agents/skills/yeren-trading-judge
```
