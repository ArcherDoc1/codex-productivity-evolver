# Codex Productivity Evolver

一个面向 Codex 日常协作的中文生产力增强 Skill。它把“先检查真实状态、小步修改、保留回滚、完成验证、沉淀经验”固化成默认工作方式，适合处理代码、配置、自动化、部署、排障、安全检查和 prompt/skill 编写任务。

## 适合什么场景

- 代码仓库修改、文档整理、脚本编写和本地验证。
- 配置、依赖、启动失败、端口占用、环境变量等工程问题排查。
- SSH、服务器、安全、删除、清理磁盘、账单等高风险操作前的谨慎流程。
- 编写或优化 prompt、Codex skill、自动化流程。
- 把一次解决问题的经验沉淀成以后可复用的检查清单。

## 核心原则

- 中文优先：默认用中文给出结论、原因和可执行步骤。
- 真实状态优先：遇到路径、权限、版本、端口、环境变量问题，先检查再判断。
- 风险分级：低风险任务直接推进，中高风险任务先说明影响、备份和回滚。
- 小步可回滚：避免无关重构，不为“看起来更整洁”扩大改动面。
- 验证闭环：能跑测试就跑测试，不能验证时明确说明原因。
- 经验可复用：把常见问题整理成模板，而不是只解决眼前一次。

## 仓库结构

```text
.
├── SKILL.md              # Codex skill 主体文件
├── README.md             # 项目介绍
├── INSTALL.md            # 安装和更新说明
├── CONTRIBUTING.md       # 贡献和维护规则
├── SECURITY.md           # 安全注意事项
├── CHANGELOG.md          # 版本变更记录
├── LICENSE               # MIT License
└── docs/
    ├── USAGE.md          # 使用示例
    └── DESIGN.md         # 设计理念
```

## 快速安装

把仓库克隆到任意工作目录后，将 `SKILL.md` 放入 Codex skills 目录：

```powershell
git clone https://github.com/ArcherDoc1/codex-productivity-evolver.git E:\Codegit
New-Item -ItemType Directory -Force C:\Users\Archer\.codex\skills\codex-productivity-evolver
Copy-Item E:\Codegit\SKILL.md C:\Users\Archer\.codex\skills\codex-productivity-evolver\SKILL.md -Force
```

更详细的安装、更新和回滚方式见 [INSTALL.md](INSTALL.md)。

## 使用方式

在 Codex 对话中处理工程类任务时，可以直接提到这个 skill 或把它作为默认协作规范使用。典型触发语：

```text
用 codex-productivity-evolver 的方式帮我检查这个仓库。
按照自我进化 skill 的流程修复启动失败。
把这次排障经验沉淀进 skill。
```

更多示例见 [docs/USAGE.md](docs/USAGE.md)。

## 维护建议

每次更新 `SKILL.md` 后，建议同时更新：

- `CHANGELOG.md`：记录改了什么。
- `docs/USAGE.md`：如果新增了使用场景或模板。
- `docs/DESIGN.md`：如果改变了核心原则或风险策略。

## License

MIT License. See [LICENSE](LICENSE).
