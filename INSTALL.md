# 安装与更新

## 前置条件

- Windows 电脑已安装 Git。
- Codex 本地 skills 目录可用，默认位置通常是：

```powershell
C:\Users\Archer\.codex\skills
```

## 首次安装

如果你已经把本仓库放在 `E:\Codegit`，执行：

```powershell
New-Item -ItemType Directory -Force C:\Users\Archer\.codex\skills\codex-productivity-evolver
Copy-Item E:\Codegit\SKILL.md C:\Users\Archer\.codex\skills\codex-productivity-evolver\SKILL.md -Force
```

如果从 GitHub 重新克隆：

```powershell
git clone https://github.com/ArcherDoc1/codex-productivity-evolver.git E:\Codegit
New-Item -ItemType Directory -Force C:\Users\Archer\.codex\skills\codex-productivity-evolver
Copy-Item E:\Codegit\SKILL.md C:\Users\Archer\.codex\skills\codex-productivity-evolver\SKILL.md -Force
```

## 更新仓库

```powershell
cd E:\Codegit
git pull
```

## 更新本地 Codex skill

```powershell
Copy-Item E:\Codegit\SKILL.md C:\Users\Archer\.codex\skills\codex-productivity-evolver\SKILL.md -Force
```

## 修改后上传 GitHub

```powershell
cd E:\Codegit
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
