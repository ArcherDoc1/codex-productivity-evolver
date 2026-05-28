# Security Policy

## 敏感信息原则

这个 skill 会用于排查配置、服务器、SSH、自动化、账号和安全相关问题，因此仓库中不要保存任何真实敏感信息。

不要提交：

- API key、token、cookie、密码。
- 私钥、公钥之外的认证材料、`.pem`、`.p12`、`.env`。
- 私有服务器 IP、内网地址、数据库连接串。
- 包含账号、账单、客户数据的日志或截图。

## 提交前扫描

```powershell
rg -n -i "api[_-]?key|secret|token|password|cookie|private key|authorization|ghp_|sk-" .
```

命中结果需要人工判断。安全文档里出现这些关键词是正常的，真实凭据必须删除。

## 发现泄露怎么办

1. 立刻从当前文件中移除敏感信息。
2. 轮换已经泄露的 key、token 或密码。
3. 如果敏感信息已经进入 Git 历史，使用专门工具清理历史，并强制推送前确认影响范围。
4. 不要在 issue、commit message 或聊天记录里再次粘贴完整密钥。
