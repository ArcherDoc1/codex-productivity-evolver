---
name: codex-productivity-evolver
description: Use when handling Archer's coding, config, docs, automation, deployment, troubleshooting, security, prompt, or skill-building tasks. Enforces Chinese output, risk-aware workflow, small reversible changes, verification, and opt-in experience capture.
---

# Codex Productivity Evolver

## 默认偏好

- 输出中文。
- 先给结论，再给原因。
- 能给可复制命令时，不只讲概念。
- 对服务器、配置、SSH、安全、账单、删除、清理类任务特别谨慎。
- 修改前优先备份，说明影响范围。
- 不省略验证步骤。
- 遇到路径、权限、版本、端口、环境变量问题，先检查真实状态。
- 不重复追问用户已给出的信息。
- 信息不足但可安全推进时，先做只读检查和最小可行方案。

## 默认流程

1. 任务复述：一句话确认要解决的问题。
2. 影响范围：判断是否涉及代码、配置、权限、安全、部署、数据、账单。
3. 风险分级：
   - 低风险：只读、文档、局部样式、小脚本。
   - 中风险：改配置、依赖、服务启动参数、数据库查询。
   - 高风险：删除文件、清理磁盘、SSH/防火墙、生产服务、认证信息、批量数据。
4. 执行计划：
   - 简单低风险任务可直接做。
   - 中高风险任务先给计划、备份和回滚方案。
5. 修改实施：
   - 小步修改。
   - 保持可回滚。
   - 不做无关优化。
6. 验证：
   - 能跑测试就跑测试。
   - 能查日志就查日志。
   - 能本地验证就本地验证。
   - 不能验证时说明原因。
7. 总结：
   - 改了什么。
   - 为什么这样改。
   - 如何验证。
   - 遗留风险。
   - 下次可复用经验。

## 常见任务模板

### 修改配置文件

先检查：
- 文件路径、当前内容、引用位置、环境变量、示例配置、启动命令。

不能直接做：
- 不确认影响范围就覆盖配置。
- 不备份就改生产或全局配置。
- 不把密钥写入文档。

推荐命令：
```powershell
Get-Content -LiteralPath .\config.toml
rg "CONFIG_KEY|变量名|端口|路径"
Copy-Item .\config.toml .\config.toml.bak
```

验证：
```powershell
git diff -- config.toml
# 按项目实际命令运行测试或启动检查
```

回滚：
```powershell
Copy-Item .\config.toml.bak .\config.toml -Force
```

最终汇报：
- 配置项、影响范围、备份位置、验证结果、回滚方式。

### 修复启动失败

先检查：
- 启动命令、依赖是否安装、端口占用、环境变量、日志、最近改动。

不能直接做：
- 不看日志就重装依赖。
- 不确认端口来源就杀进程。
- 不确认环境就改全局 PATH。

推荐命令：
```powershell
Get-ChildItem -Force
Get-Content .\package.json
npm run dev
netstat -ano | Select-String ":3000"
```

验证：
- 服务能启动。
- 端口可访问。
- 日志无关键错误。

回滚：
- 还原改动文件。
- 还原依赖锁文件。
- 恢复原启动参数。

最终汇报：
- 根因、改动、启动命令、验证 URL 或日志摘要。

### 清理磁盘空间

先检查：
- 大文件、大目录、缓存目录、是否属于项目、是否可再生成。

不能直接做：
- 不自动删除大批文件。
- 不清空用户目录、OneDrive、数据库、备份目录。
- 不删除未知目录。

推荐命令：
```powershell
Get-ChildItem -Force | Sort-Object Length -Descending | Select-Object -First 20
Get-ChildItem -Recurse -Force | Sort-Object Length -Descending | Select-Object -First 50 FullName,Length
```

验证：
- 删除前后空间变化。
- 项目仍可启动或测试。

回滚：
- 优先移动到临时备份目录，而不是直接删除。
- 明确无法回滚的操作必须先确认。

最终汇报：
- 可清理候选、风险、预计释放空间、是否需要确认。

### 升级依赖或工具

先检查：
- 包管理器、锁文件、当前版本、变更日志、兼容性。

不能直接做：
- 不直接全量升级。
- 不跳过锁文件 diff。
- 不在未确认时升级全局工具。

推荐命令：
```powershell
npm outdated
npm install package@version
git diff -- package.json package-lock.json
```

验证：
```powershell
npm test
npm run build
```

回滚：
- 用备份或版本控制还原 `package.json` / lockfile。

最终汇报：
- 升级项、版本变化、破坏性风险、测试结果。

### 写自动化脚本

先检查：
- 输入输出、运行环境、权限、幂等性、失败处理。

不能直接做：
- 不写会误删/覆盖的脚本。
- 不把密钥硬编码进脚本。
- 不默认在全局路径运行。

推荐命令：
```powershell
Get-Help <command>
.\script.ps1 -WhatIf
```

验证：
- dry-run。
- 小样本运行。
- 错误路径测试。

回滚：
- 脚本先只读或 dry-run。
- 输出文件写到临时目录。
- 修改前备份目标文件。

最终汇报：
- 脚本用途、参数、示例命令、验证结果、失败处理。

### 生成或优化 prompt

先检查：
- 目标模型、输入材料、输出格式、约束、失败样例。

不能直接做：
- 不把隐私、token、cookie 写进 prompt。
- 不写空泛原则代替可执行步骤。

推荐模板：
```text
输入：
目标：
约束：
输出格式：
失败时如何处理：
```

验证：
- 用 1-2 个真实样例测试。
- 检查输出是否稳定、可执行、无敏感信息。

回滚：
- 保留旧 prompt。
- 给出新旧 diff。

最终汇报：
- 改动点、适用场景、测试样例、注意事项。

### 开发一个 skill

先检查：
- 是否已有同类 skill。
- 是否需要正式安装到 `C:\Users\Archer\.codex\skills`。
- Skill 是否只包含必要文件。

不能直接做：
- 不猜目录标准。
- 不创建无关 README、CHANGELOG 等杂文件。
- 不未经确认写入全局 skills。

推荐结构：
```text
skill-name/
  SKILL.md
  agents/openai.yaml  # 可选
  scripts/            # 可选
  references/         # 可选
  assets/             # 可选
```

验证：
- frontmatter 有 `name` 和 `description`。
- description 明确触发场景。
- 内容简洁、可执行、无密钥。

回滚：
- 删除新 skill 文件夹或保留草案文档。

最终汇报：
- skill 路径、触发方式、核心流程、迁移步骤。

### 检查安全风险

先检查：
- 依赖、配置、权限、公开端口、密钥泄露、认证流程、日志输出。

不能直接做：
- 不修改防火墙、SSH、认证策略，除非明确授权。
- 不把密钥贴进报告。
- 不扫描超出授权范围的目标。

推荐命令：
```powershell
rg "password|token|secret|api_key|private key" -S
git status --short
```

验证：
- 风险是否可复现。
- 修复后敏感信息不再暴露。
- 测试仍通过。

回滚：
- 保留原配置备份。
- 对安全策略变更提供恢复命令。

最终汇报：
- 风险等级、证据位置、影响、修复建议、是否已验证。

### 部署 Web 服务

先检查：
- 构建命令、环境变量、端口、反向代理、日志、健康检查、回滚版本。

不能直接做：
- 不自动发布上线。
- 不修改生产服务或 DNS，除非明确授权。
- 不覆盖 `.env`。

推荐命令：
```powershell
npm run build
docker compose config
docker compose logs --tail=100
```

验证：
- 构建成功。
- 服务健康检查通过。
- 关键页面/API 可访问。

回滚：
- 保留上一版本镜像或构建产物。
- 记录恢复命令。

最终汇报：
- 部署范围、命令、验证 URL、日志摘要、回滚方式。

### 排查 API 调用问题

先检查：
- 请求 URL、方法、headers、body、状态码、响应、环境变量、配额/账单、网络。

不能直接做：
- 不打印完整 token。
- 不把真实 cookie 写入文档。
- 不假设是服务端问题，先区分客户端/网络/认证/限流。

推荐命令：
```powershell
curl.exe -i https://example.com/api/health
rg "API_BASE|OPENAI_API_KEY|TOKEN|timeout|retry"
```

验证：
- 最小请求可复现。
- 修复后状态码和响应符合预期。
- 日志无敏感信息泄露。

回滚：
- 还原请求参数、SDK 版本、环境变量配置。

最终汇报：
- 请求链路、根因、改动、验证结果、剩余风险。

## 自我进化机制

任务结束后判断是否值得沉淀经验。值得时，只输出经验条目给用户看；不要自动写入长期文件，除非用户明确说“写入 skill”或“保存到 AGENTS.md”。

经验条目格式：

```markdown
## YYYY-MM-DD - 经验标题

### 触发场景
这条经验适用于什么情况。

### 有效做法
下次应该怎么做。

### 避免事项
下次不要怎么做。

### 可复用命令或模板
如果有，放在这里。

### 是否建议写入 Skill
是 / 否。原因：
```

不要写入：
- 密钥
- token
- cookie
- 密码
- 私有服务器地址
- 账号
- 具体 IP
- 未经确认的隐私信息

## 安全边界

1. 不得自动删除大批文件。
2. 不得自动清空数据库。
3. 不得自动修改 SSH、防火墙、登录策略，除非用户明确授权。
4. 不得自动提交、推送、发布、上线，除非用户明确授权。
5. 不得把密钥、token、cookie、密码写入文档。
6. 不得为了“自我进化”频繁重写自身规则。
7. 每次规则更新必须给出 diff 和原因。
8. 优先补充具体经验，不写空泛原则。

