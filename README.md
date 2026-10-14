# .github

farfarfun-skill 组织的 Community Health Files 仓库，承载组织主页所展示的 profile README，本身不包含可安装的 Skill。

## Install

无需安装。本仓库为 GitHub 特殊仓库，[`profile/README.md`](profile/README.md) 会自动渲染至 [组织主页](https://github.com/farfarfun-skill)。

## Usage

如需新增或修改组织主页的展示内容，直接编辑 [`profile/README.md`](profile/README.md) 并提交即可。

新增或调整 Skill 时，需同步更新两处手工维护的清单：本仓库 `profile/README.md` 中的「仓库总览」表，以及 [`skill-router`](https://github.com/farfarfun-skill/skill-router) 的路由表。两者均不会自动跟随各仓库变化。

## 关于组织

本仓库属于 [farfarfun-skill](https://github.com/farfarfun-skill) —— [farfarfun](https://github.com/farfarfun) 旗下的 AI Agent Skill 产品线子组织，也是全部自研 Skill 的源头。组织内各仓库分别聚焦一个治理域，把原本依赖人工评审的规范，转化为 Agent 可直接调用的确定性检查器与工作流；issue、PR 与规范变更均在此处提交。

本仓库在其中只承担组织主页的展示职责，不含任何 Skill。要确认某个任务该用哪个 Skill，先查 [`skill-router`](https://github.com/farfarfun-skill/skill-router)；需要批量安装或通过 Gitee 访问，请前往镜像组织 [farfarfun-skills](https://github.com/farfarfun-skills)。
