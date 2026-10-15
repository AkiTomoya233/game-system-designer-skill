# 多 AI 客户端兼容与安装须知

> 核验日期：2026-10-15。AI 客户端的目录和命令可能更新；安装前请同时查看对应官方文档。

## 先理解三个层次

1. **模型能读懂**：只要能把 `SKILL.md` 和必要参考文件交给模型，它通常能理解策划流程。
2. **客户端能发现**：客户端必须支持 Agent Skills，或能把本目录注册为技能，才能自动发现和按需加载。
3. **客户端能执行**：Excel、图片生成、Figma、流程图、联网检索和原生应用预览还需要对应工具。加载成功不等于拥有这些工具。

本仓库遵守通用的 `SKILL.md` 目录结构。核心规则可跨客户端使用；`agents/openai.yaml` 只为 OpenAI/Codex 提供界面元数据，其他客户端可以忽略。

## 通用安装前检查

- 下载或克隆完整仓库，不要只保存 `SKILL.md`；它会引用 `references/`。
- 确认目录最终形态为 `<技能根目录>/game-system-designer/SKILL.md`。
- 第一次用于某个项目时，准备并指定该项目的素材库绝对路径。
- 不要把项目配置表、UI、原画、需求文档、账号凭据或私有路径提交回公共 Skill 仓库。
- 首次正式交付前，用一个小需求验证：技能能否发现、参考文件能否读取、文件能否写入、Excel/图片/流程图工具是否真实可用。
- 客户端缺少某项工具时，只输出可验证的降级结果，并明确未完成的验证；不得声称已经生成或预览。

## 兼容矩阵

| 客户端 | 原生发现 | 推荐位置或安装方式 | 调用方式 | 主要注意事项 |
|---|---|---|---|---|
| OpenAI Codex | 是 | 用户级 `%CODEX_HOME%\skills\game-system-designer`；项目级 `.codex\skills\game-system-designer` | `$game-system-designer` 或由任务自动触发 | `agents/openai.yaml` 生效；具体文件、表格、图片和连接能力取决于当前 Codex 环境 |
| DeepSeek Harness | 是，但需启用 Skill 插件 | 用户级 `%DSH_HOME%\skills\game-system-designer`（默认 `%USERPROFILE%\.dsh\skills`）；项目级 `.dsh\skills\game-system-designer` 或 `.agents\skills\game-system-designer` | `/game-system-designer` 或自动触发 | 需要加载 `dsh-skill`、`dsh-skill-filesystem`、`dsh-tool-skill`；不会自动扫描 Codex 用户目录 |
| Claude Code | 是 | 用户级 `%USERPROFILE%\.claude\skills\game-system-designer`；项目级 `.claude\skills\game-system-designer` | `/game-system-designer` 或自动触发 | Claude Code 的工具名和权限与 Codex 不同；不要照搬 Codex 专用工具调用 |
| claude.ai | 是，需上传 | 将整个技能目录打包为 ZIP，在 Settings > Features 上传自定义 Skill | 由 Claude 自动匹配 | 需要支持自定义 Skills 的套餐并启用代码执行；与 Claude Code、Claude API 不自动同步 |
| Claude API | 是，需 API 上传 | 通过 Skills API 上传技能并在容器中引用 `skill_id` | API 参数指定 | 需要 API Key 与代码执行工具；容器无网络、不能运行时安装依赖 |
| Gemini CLI | 是 | `gemini skills install <仓库URL>`，或复制到 `.gemini\skills\game-system-designer` / `.agents\skills\game-system-designer` | 自动匹配；用 `/skills list` 检查 | 激活技能时会请求授权；可用 `/skills reload` 刷新修改 |
| Cursor | 是 | `.cursor\skills\game-system-designer`、`.agents\skills\game-system-designer`；也兼容 `.codex\skills` 与 `.claude\skills` | `/game-system-designer` 或 `@game-system-designer` | 云端 Agent 只同步指定的个人技能目录；本地工具不自动复制到云端 |
| GitHub Copilot | 是，取决于使用面 | 项目级 `.github\skills\game-system-designer`、`.agents\skills\game-system-designer`；个人级 `~/.copilot/skills/game-system-designer` | 自动匹配，或由 SDK 注册技能目录 | Copilot SDK 需要在会话中配置 `skillDirectories`；编辑器、CLI 与 SDK 能力不同 |
| OpenAI API / Agents API | 是，需注册 | 上传 ZIP/目录，或在本地 Shell 环境注册技能绝对路径 | 请求中显式提供技能或让模型按描述选择 | 托管和本地 Shell 的挂载方式不同；注意费用、容器和网络权限 |
| 普通网页聊天或其他模型 | 通常否 | 上传 `SKILL.md` 与本次需要的参考文件，或把核心规则放入项目指令 | 在提示中明确要求先读取 Skill | 这是手动提供上下文，不是自动 Skill；无法保证渐进加载、工具执行或持续绑定 |

## 各客户端的最低要求

### OpenAI Codex

1. 安装完整目录，而不是单独复制主文件。
2. 新开任务后确认 `game-system-designer` 出现在可用 Skills 中。
3. 使用 `$game-system-designer` 明确调用，或直接提出符合描述的游戏系统策划请求。
4. 处理表格、图片、Figma 或流程图时，另外确认对应工具/插件可用。

官方参考：

- <https://developers.openai.com/api/docs/guides/tools-skills>
- <https://developers.openai.com/plugins/concepts/skills>

### DeepSeek Harness

1. Harness 组合中加载以下三个插件：

   ```yaml
   - name: '@deepseek-ai/dsh-skill'
   - name: '@deepseek-ai/dsh-skill-filesystem'
   - name: '@deepseek-ai/dsh-tool-skill'
   ```

2. 将完整目录放入 `.dsh/skills/`、`.agents/skills/`、用户技能目录，或加入 `customSkillDirs`。
3. 在会话中检查技能目录是否出现；若未出现，先检查插件组合和扫描根目录，而不是反复改提示词。
4. DeepSeek 只把本 Skill 当作规则来源；Excel、图片、浏览器、Figma 和原生预览仍需单独配置相应插件或工具。

官方参考：

- <https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/skill/skill-filesystem/README.md>
- <https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/skill/tool-skill/README.zh.md>

### Claude Code、claude.ai 与 Claude API

- Claude Code：复制到 `~/.claude/skills/` 或项目 `.claude/skills/`。
- claude.ai：上传完整 ZIP；Skill 只对当前用户生效。
- Claude API：通过 Skills API 上传，并在请求中结合代码执行容器使用。
- 三个使用面互不自动同步，需要分别安装或上传。
- Claude 专用 hooks、AskUserQuestion、插件命令等不是本 Skill 的依赖；若某份参考提到宿主专用工具，应转换为当前环境等价能力。

官方参考：<https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview>

### Gemini CLI

推荐直接安装：

```text
gemini skills install https://github.com/AkiTomoya233/game-system-designer-skill
```

安装后使用：

```text
/skills list
/skills reload
```

也可把完整目录放入 `.gemini/skills/` 或 `.agents/skills/`。Gemini CLI 在技能激活时会要求授权。

官方参考：<https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/using-agent-skills.md>

### Cursor

项目技能可放在 `.cursor/skills/` 或 `.agents/skills/`。Cursor 也会兼容读取 `.codex/skills/` 与 `.claude/skills/`，因此同一项目通常不必复制多份。通过 `/game-system-designer` 或 `@game-system-designer` 使用。

官方参考：<https://cursor.com/help/customization/skills>

### GitHub Copilot

编辑器或 CLI 的项目技能可放在 `.github/skills/`、`.claude/skills/` 或 `.agents/skills/`。使用 Copilot SDK 时，在创建会话时把父目录加入 `skillDirectories`。

官方参考：

- <https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/customization-cheat-sheet>
- <https://docs.github.com/en/copilot/how-tos/copilot-sdk/features/skills>

## 不支持原生 Skill 的 AI 怎么用

只在确认客户端没有原生支持后采用手动模式：

1. 上传 `SKILL.md`。
2. 根据任务上传它明确引用的必要 `references/`，不要一次塞入全部项目资料。
3. 提示模型：“先完整读取 Skill 与相关参考；缺少项目素材库时先询问；阻断问题必须整批确认后再正式制作。”
4. 每次新对话重新提供，因为普通聊天通常不会持续保存本地 Skill 绑定。
5. 将输出视作草案，尤其是涉及 Excel、图片、配置和原生预览的结论。

## 工具能力检查表

在要求完整交付前，确认宿主至少具备任务真正需要的能力：

- 文件读取与写入；
- XLSX 创建、修改、公式检查与图片/形状保真；
- Microsoft Excel 或等价原生预览；
- Draw.io 或其他可编辑流程图输出；
- 图片生成、图片编辑和透明背景处理；
- Figma 读取或写入权限；
- 联网检索与引用；
- 项目素材库访问权限；
- 中文路径、字体和编码支持。

缺少某项能力时，应把结果降级为文字规范、线框说明、待填配置或未验证产物，并明确说明缺口。
