# Contributing

这个仓库主要服务个人 Codex 工作流，但仍然按清晰、可回滚、可验证的方式维护。

## 修改原则

- 保持 `SKILL.md` 是唯一的 skill 主体入口。
- 新增规则时，优先放到已有章节；只有当重复明显增加时再新增章节。
- 每条规则尽量可执行，少写抽象口号。
- 涉及安全、删除、账号、密钥、服务器的规则要更保守。
- 不把真实 token、cookie、密码、私有服务器地址写进仓库。

## 提交前检查

```powershell
cd E:\Codegit
git status
rg -n -i "api[_-]?key|secret|token|password|cookie|private key|ghp_|sk-" .
git diff --check
```

如果 `rg` 命中的是安全说明里的示例词，可以保留；如果是真实凭据，必须删除后再提交。

## 推荐提交信息

```text
Update usage docs
Add troubleshooting template
Refine safety checklist
Fix encoding notes
```

## 文档风格

- 面向使用者，先讲怎么用，再讲为什么。
- 命令用可复制代码块。
- 对高风险操作明确写出影响范围、备份方式和回滚方式。
- 中文内容使用 UTF-8 编码。
