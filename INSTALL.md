# 安装与更新

## 前置条件

- Windows 电脑已安装 Git。
- Codex 本地 skills 目录可用，默认位置通常是当前用户目录下的 `.codex\skills`。

在 PowerShell 中可以用下面的命令查看目标安装目录：

```powershell
Join-Path $env:USERPROFILE ".codex\skills"
```

## 首次安装

推荐把仓库克隆到你自己的代码目录，目录名可以按个人习惯选择：

```powershell
git clone https://github.com/ArcherDoc1/codex-productivity-evolver.git
cd codex-productivity-evolver
$skillDir = Join-Path $env:USERPROFILE ".codex\skills\codex-productivity-evolver"
New-Item -ItemType Directory -Force $skillDir
Copy-Item .\SKILL.md (Join-Path $skillDir "SKILL.md") -Force
```

## 只下载 SKILL.md

如果你不需要完整仓库，也可以在 GitHub 页面打开 `SKILL.md`，点击 Raw 后保存文件，然后放到：

```text
<your-user-home>\.codex\skills\codex-productivity-evolver\SKILL.md
```

PowerShell 示例：

```powershell
$skillDir = Join-Path $env:USERPROFILE ".codex\skills\codex-productivity-evolver"
New-Item -ItemType Directory -Force $skillDir
Copy-Item .\SKILL.md (Join-Path $skillDir "SKILL.md") -Force
```

## 更新仓库

在你自己的仓库目录中执行：

```powershell
git pull
```

## 更新本地 Codex skill

在仓库根目录中执行：

```powershell
$skillDir = Join-Path $env:USERPROFILE ".codex\skills\codex-productivity-evolver"
Copy-Item .\SKILL.md (Join-Path $skillDir "SKILL.md") -Force
```

## 修改后上传 GitHub

```powershell
git status
git add .
git commit -m "Update skill docs"
git push
```

## 回滚到上一个提交

先只查看历史：

```powershell
git log --oneline -5
```

如需回滚某次提交，优先使用 `git revert`，它会生成一个新的反向提交：

```powershell
git revert <commit-sha>
git push
```

不建议直接使用 `git reset --hard`，除非你非常确定要丢弃本地修改。
