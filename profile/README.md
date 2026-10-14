# FarFarFun Skill

[farfarfun](https://github.com/farfarfun) 的 **AI Agent Skill 产品线**子组织，也是全部自研 Skill 的**源头**。各仓库分别聚焦一个治理域，将项目规范、发布流程与执行边界等原本依赖人工评审的规则，转化为 Agent 可直接调用的确定性检查器与工作流。

本组织是全部自研 Skill 的权威来源，issue、PR 与规范变更均在此处提交。如需批量安装 Skill（含社区项目）或通过 Gitee 访问，请前往聚合镜像组织 [farfarfun-skills](https://github.com/farfarfun-skills)。

> 🧭 **如需确认适用的 Skill**，请先查阅 [`skill-router`](https://github.com/farfarfun-skill/skill-router)：该路由表汇总了全组织 10 个 Skill 的归属仓库、适用问题与调用方式。

## 仓库总览

含 Skill 的仓库：

| 仓库 | 定位 | 包含的 Skill | 适用场景 |
| --- | --- | --- | --- |
| [`project-manager`](https://github.com/farfarfun-skill/project-manager) | 项目全生命周期治理 | `project-manager`、`project-structure-governance`、`github-repo-standards` | 检查 PRD、设计、技术方案、测试、发布与复盘产物；审计仓库目录结构与命名；审计默认分支、README 结构与 GitHub 描述/Topics |
| [`service-governance`](https://github.com/farfarfun-skill/service-governance) | 服务工程规范 | `service-release-governance`、`bash-service-guide`、`submodule-workspace-governance`，以及由 `lang-spec-hub` 同步的 `python-development-standards`、`java-development-standards` | 约束服务须通过正式包发布并启动；统一 Bash 生命周期脚本；编排 `apps/` 下的多仓库子模块 |
| [`lang-spec-hub`](https://github.com/farfarfun-skill/lang-spec-hub) | 多语言开发规范 | `python-development-standards`、`java-development-standards` | Python 与 Java 的代码实现与审查，优先遵循项目既有版本与工具链 |
| [`paperclip-governance`](https://github.com/farfarfun-skill/paperclip-governance) | Paperclip 平台专属治理 | `isolate-paperclip-work`、`paperclip-task-coordinator` | 隔离 Paperclip 执行边界；按任务与 Agent 维度生成未完成工作报表 |

不含 Skill 的仓库：

| 仓库 | 作用 |
| --- | --- |
| [`skill-router`](https://github.com/farfarfun-skill/skill-router) | 全组织 Skill 路由表，选择 Skill 的统一入口 |
| [`publish-skill`](https://github.com/farfarfun-skill/publish-skill) | 发布工具，用于校验各仓库 `SKILL.md`、生成 `npx skills add` 安装清单，并可选择镜像至 `farfarfun-skills` |
| `.github` | 本组织主页（`profile/README.md`） |

> `service-governance` 中的 `python-development-standards` 与 `java-development-standards` 是**由 `lang-spec-hub` 同步而来的副本**，就近存放便于服务类 Skill 引用具体语言规范。权威版本位于 `lang-spec-hub`，规范变更请在该仓库提交。

## 如何选择仓库

- 建立**项目管理与交付质量**门禁：建议从 [`project-manager`](https://github.com/farfarfun-skill/project-manager) 入手，该仓库同时是其余仓库相互引用的基线。
- 处理**服务发布、启动脚本或多仓库编排**：使用 [`service-governance`](https://github.com/farfarfun-skill/service-governance)。
- 编写 **Python 或 Java 代码**：使用 [`lang-spec-hub`](https://github.com/farfarfun-skill/lang-spec-hub)。
- 在 **Paperclip 平台**执行任务：先安装 [`paperclip-governance`](https://github.com/farfarfun-skill/paperclip-governance) 建立执行边界，再按需配合 `project-manager` 实施阶段门禁。

多个仓库可同时安装，各 Skill 之间仅通过文档相互引用，不存在路径耦合。

## 通用约定

- 全部 Skill 面向 Codex 设计（部分同时兼容 Claude），统一以软链接方式安装至 `${CODEX_HOME:-$HOME/.codex}/skills/`。
- 检查器统一输出 `allow`、`revise`、`block` 三种状态，用于判定结构化产物是否满足门禁要求，不替代人工做出最终业务决策。
- 各仓库的 `skills/<name>/SKILL.md` 为对应 Skill 的唯一权威说明，README 仅承担导航作用。

## Install（通用步骤）

```bash
git clone https://github.com/farfarfun-skill/<repo>.git
cd <repo>

mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
for skill in skills/*; do
  ln -s "$(pwd)/$skill" "${CODEX_HOME:-$HOME/.codex}/skills/$(basename "$skill")"
done
```

具体依赖要求（例如 `project-manager` 需要 PyYAML）请参见各仓库 README。

## 镜像与分发

本组织的仓库由 [`publish-skill`](https://github.com/farfarfun-skill/publish-skill) 镜像至聚合组织 [farfarfun-skills](https://github.com/farfarfun-skills)，并进一步同步至 Gitee 组织 [farfarfun-skills](https://gitee.com/farfarfun-skills)，镜像仓库统一命名为 `farfarfun-skill--<repo>`，以便与社区 fork 区分。

| 使用场景 | 对应位置 |
| --- | --- |
| 提交 issue 或 PR、变更规范 | **本组织**（源头仓库，镜像组织不接受 PR） |
| 批量安装 Skill，含社区项目 | [farfarfun-skills](https://github.com/farfarfun-skills) |
| 国内网络环境下访问 | [gitee.com/farfarfun-skills](https://gitee.com/farfarfun-skills) |

## 其他 farfarfun 组织

farfarfun 的新项目默认在主组织孵化，当某一方向的仓库数量与功能完整度达到一定规模后，即毕业并独立为子组织；规划阶段已确定为独立产品线的，则直接建立子组织。

| 组织 | 产物 |
| --- | --- |
| [farfarfun](https://github.com/farfarfun) | 通用 Python 工具链，含 `far*` 基础库与 `fun*` 领域库 |
| [farfarfun-drive](https://github.com/farfarfun-drive) | 网盘与云存储，含统一接口框架与各网盘驱动 |
| [farfarfun-skills](https://github.com/farfarfun-skills) | Skill 聚合镜像，含社区 fork 与本组织自研，每小时与上游同步并镜像至 Gitee |
| [farfarfun-utools](https://github.com/farfarfun-utools) | uTools 插件，覆盖 AI 聊天、网址导航与两步验证码 |

## 联系

- 📧 **Email**: farfarfun@qq.com
- 🐙 **GitHub**: [@farfarfun](https://github.com/farfarfun)
