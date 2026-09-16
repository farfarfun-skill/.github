# FarFarFun Skill

面向 AI 编码 Agent（Codex / Claude 等）的技能（Skill）仓库集合。每个仓库聚焦一个治理域，把项目规范、发布流程、执行边界这些原本靠人工评审的规则，转化为 Agent 可以直接调用的、确定性的检查器和工作流。

## 仓库总览

| 仓库 | 定位 | 包含的 Skill | 适用场景 |
| --- | --- | --- | --- |
| [`project-manager`](https://github.com/farfarfun-skill/project-manager) | 项目全生命周期治理 | `project-manager`、`project-structure-governance`、`github-repo-standards` | 检查 PRD/设计/技术方案/测试/发布/复盘产物；审计仓库目录结构与命名；审计 README 结构与 GitHub Topics |
| [`service-governance`](https://github.com/farfarfun-skill/service-governance) | 服务工程规范 | `service-release-governance`、`bash-service-guide`、`submodule-workspace-governance` | 约束服务通过正式包发布启动；统一 Bash 生命周期脚本；编排 `apps/` 下多仓库子模块 |
| [`paperclip-governance`](https://github.com/farfarfun-skill/paperclip-governance) | Paperclip 平台专属治理 | `isolate-paperclip-work`、`paperclip-task-coordinator` | 隔离 Paperclip 执行边界；按任务/Agent 维度生成未完成工作报表 |
| [`lang-spec-hub`](https://github.com/farfarfun-skill/lang-spec-hub) | 多语言开发规范 | `python-development-standards`、`java-development-standards` | Python/Java 代码实现与审查，优先遵循项目已有版本与工具链 |

## 如何选择仓库

- 做**项目管理和交付质量**门禁：从 [`project-manager`](https://github.com/farfarfun-skill/project-manager) 开始，它也是其余仓库互相引用的基线。
- 做**服务发布、启动脚本或多仓库编排**：用 [`service-governance`](https://github.com/farfarfun-skill/service-governance)。
- 在 **Paperclip 平台**上执行任务：先装 [`paperclip-governance`](https://github.com/farfarfun-skill/paperclip-governance) 建立执行边界，再按需搭配 `project-manager` 做阶段门禁。
- 写 **Python / Java 代码**：用 [`lang-spec-hub`](https://github.com/farfarfun-skill/lang-spec-hub)。

多个仓库可以同时安装，各 Skill 之间通过文档互相引用，不存在路径耦合。

## 通用约定

- 所有 Skill 面向 Codex（部分同时兼容 Claude），安装方式统一为软链接到 `${CODEX_HOME:-$HOME/.codex}/skills/`。
- 检查器输出统一为 `allow` / `revise` / `block` 三态，代表结构化产物是否达到门禁，不代替人做最终业务决策。
- 每个仓库的 `skills/<name>/SKILL.md` 是该 Skill 的唯一权威说明，README 只做导航。

## Install（通用步骤）

```bash
git clone https://github.com/farfarfun-skill/<repo>.git
cd <repo>

mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
for skill in skills/*; do
  ln -s "$(pwd)/$skill" "${CODEX_HOME:-$HOME/.codex}/skills/$(basename "$skill")"
done
```

具体依赖（如 `project-manager` 需要 PyYAML）见各仓库 README。
