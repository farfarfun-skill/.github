# FarFarFun Skill

[farfarfun](https://github.com/farfarfun) 的 **AI Agent Skill 产品线**子组织，也是所有自研 Skill 的**源头**。每个仓库聚焦一个治理域，把项目规范、发布流程、执行边界这些原本靠人工评审的规则，转化为 Agent 可以直接调用的、确定性的检查器和工作流。

这里是所有自研 Skill 的 source of truth——提 issue、提 PR、改规范都在本组织。想一次装一批 Skill（含社区热门项目），或者需要 Gitee 访问，去聚合镜像组织 [farfarfun-skills](https://github.com/farfarfun-skills)。

> 🧭 **不确定该用哪个 Skill？** 先看 [`skill-router`](https://github.com/farfarfun-skill/skill-router) —— 全组织 10 个 Skill 的路由表，一页列清每个 Skill 属于哪个仓库、解决什么问题、怎么调用。

## 仓库总览

含 Skill 的仓库：

| 仓库 | 定位 | 包含的 Skill | 适用场景 |
| --- | --- | --- | --- |
| [`project-manager`](https://github.com/farfarfun-skill/project-manager) | 项目全生命周期治理 | `project-manager`、`project-structure-governance`、`github-repo-standards` | 检查 PRD/设计/技术方案/测试/发布/复盘产物；审计仓库目录结构与命名；审计 README 结构与 GitHub Topics |
| [`service-governance`](https://github.com/farfarfun-skill/service-governance) | 服务工程规范 | `service-release-governance`、`bash-service-guide`、`submodule-workspace-governance`，外加从 `lang-spec-hub` 同步的 `python-development-standards`、`java-development-standards` | 约束服务通过正式包发布启动；统一 Bash 生命周期脚本；编排 `apps/` 下多仓库子模块 |
| [`lang-spec-hub`](https://github.com/farfarfun-skill/lang-spec-hub) | 多语言开发规范 | `python-development-standards`、`java-development-standards` | Python/Java 代码实现与审查，优先遵循项目已有版本与工具链 |
| [`paperclip-governance`](https://github.com/farfarfun-skill/paperclip-governance) | Paperclip 平台专属治理 | `isolate-paperclip-work`、`paperclip-task-coordinator` | 隔离 Paperclip 执行边界；按任务/Agent 维度生成未完成工作报表 |

不含 Skill 的仓库：

| 仓库 | 作用 |
| --- | --- |
| [`skill-router`](https://github.com/farfarfun-skill/skill-router) | 全组织 Skill 路由表，选 Skill 的入口 |
| [`publish-skill`](https://github.com/farfarfun-skill/publish-skill) | 发布工具：校验各仓库 `SKILL.md`、生成 `npx skills add` 安装清单、可选镜像到 `farfarfun-skills` |
| `.github` | 本组织主页（`profile/README.md`） |

> `service-governance` 里的 `python-development-standards` / `java-development-standards` 是**从 `lang-spec-hub` 同步过来的副本**（放在一起方便服务类 Skill 就近引用具体语言规范）。权威版本在 `lang-spec-hub`，改规范请改那里。

## 如何选择仓库

- 做**项目管理和交付质量**门禁：从 [`project-manager`](https://github.com/farfarfun-skill/project-manager) 开始，它也是其余仓库互相引用的基线。
- 做**服务发布、启动脚本或多仓库编排**：用 [`service-governance`](https://github.com/farfarfun-skill/service-governance)。
- 写 **Python / Java 代码**：用 [`lang-spec-hub`](https://github.com/farfarfun-skill/lang-spec-hub)。
- 在 **Paperclip 平台**上执行任务：先装 [`paperclip-governance`](https://github.com/farfarfun-skill/paperclip-governance) 建立执行边界，再按需搭配 `project-manager` 做阶段门禁。

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

## 镜像与分发

本组织的仓库会被 [`publish-skill`](https://github.com/farfarfun-skill/publish-skill) 镜像到聚合组织 [farfarfun-skills](https://github.com/farfarfun-skills)，并进一步同步到 Gitee 组织 [farfarfun-skills](https://gitee.com/farfarfun-skills)（命名为 `farfarfun-skill--<repo>`，便于和社区 fork 区分）。

| 想做什么 | 去哪 |
| --- | --- |
| 提 issue / PR、改规范 | **本组织**（源头，镜像不接受 PR） |
| 一次装一批 Skill，含社区热门项目 | [farfarfun-skills](https://github.com/farfarfun-skills) |
| 国内网络访问 | [gitee.com/farfarfun-skills](https://gitee.com/farfarfun-skills) |

## 其他 farfarfun 组织

新东西默认先放在主组织 farfarfun，等某个模块仓库攒多、功能做完善后毕业成独立的子组织；早期规划时已经确定会自成一条产品线的，直接建了子组织。

| 组织 | 产物 |
| --- | --- |
| [farfarfun](https://github.com/farfarfun) | 通用 Python 工具链：`far*` 基础库 + `fun*` 领域库 |
| [farfarfun-drive](https://github.com/farfarfun-drive) | 网盘 / 云存储：统一接口框架 + 各网盘驱动 |
| [farfarfun-skills](https://github.com/farfarfun-skills) | Skill 聚合镜像：社区热门 fork + 本组织自研，每小时跟上游同步并镜像到 Gitee |
| [farfarfun-utools](https://github.com/farfarfun-utools) | uTools 插件：AI 聊天、网址导航、两步验证码 |

## 联系

- 📧 **Email**: farfarfun@qq.com
- 🐙 **GitHub**: [@farfarfun](https://github.com/farfarfun)
