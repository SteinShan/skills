# SteinShan Skills

按自己的工作习惯持续整理的个人 Agent Skills 仓库，面向 Codex、Claude Code，以及支持 [Agent Skills 标准](https://agentskills.io/specification)的其他工具。

一份技能源码，按需安装到不同客户端。每个技能围绕一个具体任务编写，逐步从真实使用中改进。

已收录 [first-principles：第一性原理](skills/first-principles/SKILL.md)。技能正文以中文编写，技能名称与标准元数据字段使用英文。

## 仓库结构

```text
skills/
├── skills/                    # 已完成、可安装的技能
│   └── first-principles/
│       ├── SKILL.md           # 名称、触发条件和工作方式
│       ├── agents/openai.yaml # Codex 展示信息
│       └── references/        # 按需阅读的示例和概念来源
├── templates/
│   └── SKILL.md.template      # 新技能模板，不参与安装发现
├── preferences/
│   └── common.md             # 跨任务的个人通用偏好
├── AGENTS.md                 # 维护本仓库时使用的规则
└── CLAUDE.md                 # 为 Claude Code 引入同一份仓库规则
```

分类记录在下方目录表，技能文件夹保持一层。脚本和输出模板在确有需要时，放入对应技能的 `scripts/` 和 `assets/`。

## 技能目录

加入技能时在这里登记用途、适用客户端和来源；适用客户端以实际验证结果为准。

| 技能 | 用途 | 已验证客户端 | 来源 |
| --- | --- | --- | --- |
| [first-principles](skills/first-principles/SKILL.md) | 将复杂问题解构至公理，重新推演，并用核心推论和例子解释 | 待实际任务验证 | 原创；[概念来源](skills/first-principles/references/example-and-sources.md#概念来源) |

## 安装到 Codex 和 Claude Code

使用 [Vercel 的 skills 命令行工具](https://github.com/vercel-labs/skills/blob/main/docs/commands.md#skills-add)。需要满足该工具要求的 Node.js 环境。

```bash
# 查看本仓库已经提供的技能
npx skills@latest add SteinShan/skills --list

# 交互选择技能，安装为两个客户端的用户级技能
npx skills@latest add SteinShan/skills -g -a codex claude-code

# 只安装第一性原理技能
npx skills@latest add SteinShan/skills -g -a codex claude-code --skill first-principles
```

省略 `-g` 可安装到当前项目。安装时核对所选技能和目标目录；已有同名技能时，先决定替换还是为自己的改编版更名。

客户端的本地技能目录见各自官方说明：

| 客户端 | 用户级目录 | 项目级目录 |
| --- | --- | --- |
| [Codex](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills) | `~/.agents/skills/` | `.agents/skills/` |
| [Claude Code](https://code.claude.com/docs/en/skills#choose-where-skills-load) | `~/.claude/skills/` | `.claude/skills/` |

这些目录用于发现已经安装的技能；本仓库的 `skills/` 用于维护源码。目录格式通用，特定工具、脚本依赖和客户端扩展仍需逐项验证。

## 增加和更新技能

1. 在本仓库创建一个技能目录并复制模板：

   ```bash
   mkdir -p skills/my-skill
   cp templates/SKILL.md.template skills/my-skill/SKILL.md
   ```

2. 将目录名、模板中的 `name`、`description` 和正文替换为真实内容。`name` 与目录名一致，使用小写字母、数字和连字符。
3. 只有需要时才添加 `references/`、`scripts/`、`assets/`。技能中引用的资源放在该技能内部，路径相对技能目录。
4. 在仓库根目录检查能否被发现：

   ```bash
   npx skills@latest add . --list
   ```

5. 在目标客户端安装该技能，用一个真实任务验证触发条件和输出，再登记到技能目录并提交。

在源码仓库中修改技能。修改提交并推送后，对需要更新的技能重新运行上面的指定名称安装命令。安装目录中的副本不作为长期编辑位置。

## 把偏好放在合适的位置

- **跨任务的习惯**：在 [preferences/common.md](preferences/common.md) 维护，例如语言和解释方式。
- **特定任务的做法**：写进对应技能，例如如何开展代码审查、解释技术概念或整理技术笔记。
- **只对某个项目成立的规则**：放在那个项目自己的 `AGENTS.md` 或 `CLAUDE.md`。

安装技能不会自动加载本仓库的通用偏好或仓库维护规则。若希望通用偏好对所有项目生效，可将其合并到客户端现有的用户指令中：[Codex 的 `~/.codex/AGENTS.md`](https://learn.chatgpt.com/docs/agent-configuration/agents-md)、[Claude Code 的 `~/.claude/CLAUDE.md`](https://code.claude.com/docs/en/memory#choose-where-to-put-claudemd-files)。合并时保留已有内容。

## 原创与改编

可以借鉴 [Matt Pocock 的 skills 仓库](https://github.com/mattpocock/skills)的组织方式，也可以逐步加入适合自己的原创技能。

收录外部技能时，记录来源链接和固定版本，保留原许可证与署名；改编版注明改动。需要与上游同时使用时，为改编版起一个不同的名字，例如 `stein-code-review`。

本仓库为公开仓库，只收录可以公开的内容；凭据和本机配置通过环境变量或未提交的本地文件提供。当前没有引入第三方技能，也尚未指定仓库统一的开源许可证。
