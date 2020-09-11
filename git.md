# Git

## Cherry Pick

```bash
git cherry-pick commit-id-beg...commit-id-end
```

(commit-id-beg, commit-id-end]

```bash
git cherry-pick commit-id
```

(commit-id~, commit-id]

## Rebase Squash

```bash
git rebase -i commit-id
```

(commit-id, HEAD]

## 修改本地分支的 upstream

```bash
git branch -u origin/remote-branch local-branch
```

## 新建分支时设置 upstream

```bash
git  checkout -b new-branch-name  [--track] origin/remote-branch_name
```
