# yhw-prompt-guard — 回答质量护栏 Skill

Claude Code 全局 Skill：按问题类型路由到 5 个严谨回答协议（决策评估 / 代码技术 / 事实研究 / 长对话校准 / 审稿复核），防止献媚附和、凭空捏造、过度自信、答非所问、偷工减料。

基于 LLM 失效模式调研构建，20 项失效模式与对策均有论文/官方基准支撑（关键引用已于 2026-08 核实），详见 `references/`。

## 仓库结构

```
yhw-prompt-guard/
├── SKILL.md                      # Skill 主文件（路由 + 5 协议 + 总原则 + 兜底红线）
├── references/
│   ├── failure-modes.md          # 20 项失效模式清单（证据强度 + 数据 + 出处）
│   └── anti-patterns.md          # 已证伪的提示反模式 + 升级到人工/工具的阈值
└── extras/
    └── answer-quality.md         # 配套全局规则（8 条底线，需手动安装，见下）
```

## 安装（新电脑）

1. 克隆到 Claude Code 全局 skills 目录：

   ```bash
   git clone https://github.com/naixin10/yhw-prompt-guard.git ~/.claude/skills/yhw-prompt-guard
   ```

   Windows（PowerShell）：

   ```powershell
   git clone https://github.com/naixin10/yhw-prompt-guard.git "$env:USERPROFILE\.claude\skills\yhw-prompt-guard"
   ```

2. 安装配套全局规则（所有会话长期生效的 8 条底线）：

   ```bash
   cp ~/.claude/skills/yhw-prompt-guard/extras/answer-quality.md ~/.claude/rules/answer-quality.md
   ```

3. 重启 Claude Code 会话即生效（skill 列表在会话启动时加载）。

## 更新

```bash
cd ~/.claude/skills/yhw-prompt-guard && git pull
```

若 `extras/answer-quality.md` 有变更，重新执行上面第 2 步覆盖。

## 触发方式

- 自动触发：征求判断/评估建议、写代码/调试、事实研究/引用核查、长对话走偏、要求自检
- 手动触发：`/yhw-prompt-guard`，或说"质量护栏""严谨回答""防幻觉""钢人论证"
- 不触发：闲聊、翻译、润色、格式转换、单步常识问答
