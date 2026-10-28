# Personal Skills

维护个人使用的 AI agent skills，沉淀经过实际使用验证的工作流程。本仓库统一维护源码，运行配置和敏感信息留在仓库外。

## Skills

| Skill | 用途 |
| --- | --- |
| [project-context-bootstrap](project-context-bootstrap/SKILL.md) | 审计仓库结构，建立或系统重建 AGENTS.md 和 AI 项目上下文文档体系 |
| [agents-md-optimizer](agents-md-optimizer/SKILL.md) | 审查和局部优化现有项目指令，排查冲突、冗余与加载不生效 |
| [ui-no-ai](ui-no-ai/SKILL.md) | 从 UI、UX 与工程三层设计、实现和评审界面，统一视觉语言、操作流程与设计系统，并验证画面和交互 |
| [grok-code-review](grok-code-review/SKILL.md) | 调用本机 Grok CLI 审核代码并生成报告，由 Codex 核实、修复和复审 |

## 安装与使用

按所用工具的 skill 发现规则，将需要的 skill 目录复制或链接到对应安装位置。Codex 当前官方文档列出的用户级目录为 `~/.agents/skills`；已有环境可能使用其他目录，安装前核对实际加载位置，避免重复安装同名 skill。[官方说明](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)

安装目标已存在时，先核对来源和内容，再决定替换方式。软链接会让源码修改直接影响使用环境；需要稳定版本时，复制指定提交中的目录，并记录提交号。

在支持显式调用的 Codex 环境中使用：

```text
$project-context-bootstrap 审计当前仓库并初始化项目上下文文档
$agents-md-optimizer 审查现有项目规则，精简冗余并排查 AGENTS.md 加载问题
$ui-no-ai 优化当前页面的信息层级和操作流程
$grok-code-review 审核当前改动，修复确定问题，不确定事项集中询问我
```

## 维护约定

- 每个 skill 独立一个目录，目录名与 `SKILL.md` 的 `name` 一致；必需元数据为 `name`、`description`。
- 一个 skill 聚焦一个工作流程，写清触发条件和适用边界。主指令保持精简，按需添加 `references/`、`scripts/`、`assets/` 或 `agents/openai.yaml`。
- 统一在本仓库修改源码，再同步到使用环境；新增或调整 skill 时同步上方索引。
- 用实际任务检查行为，同时考虑不应触发、输入不足的情况；修改脚本时验证实际执行结果。
- 提交前检查文件清单、`git diff --cached` 和敏感信息。提交说明写清行为变化与原因。
- 个人 AI 维护约定保留在本地的 `AGENTS.md`，通过 `.git/info/exclude` 忽略，不纳入版本管理。此本地设置不会随克隆同步。

## 敏感信息

- 禁止提交密码、令牌、私钥、Cookie、真实业务数据和包含凭据的连接字符串。
- 服务器地址、账号、数据库标识和个人绝对路径通过仓库外配置提供。文档使用环境变量、虚构数据或明确占位值；`.env.example` 只保留字段和占位值。
- 只纳入 skill 实际需要且已审阅的资源；日志、截图、二维码、扫描报告和打包产物也可能包含敏感信息。
- [.gitignore](.gitignore) 用于减少误提交，无法识别写入正文的秘密，也不能清除已跟踪文件及历史；提交前仍需人工审阅，必要时用 Gitleaks 等工具扫描文件与历史。
- 凭据泄漏后先撤销或轮换，再处理历史与已分发副本；仅删除当前文件不足以消除历史记录。[GitHub 指南](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
- 公开仓库前检查完整历史、提交作者邮箱、第三方资源来源与许可证。当前未提供开源许可证，公开复用前应先确定许可方式。
