# 如何提交代码和文档

本文以 `seccome/whoiswho` 项目为例说明如何提交代码和文档。如果您要提交文档或其他项目的 Pull Request（PR），请参考本文档完成设置。所有项目仓库请前往 [seccome](https://github.com/seccome/whoiswho "点击前往 GitHub 网站") GitHub 页面查看。

## 前提条件

<!--
### 签署 CLA （TODO） 
点击 **Sign in with Github to agree** 按钮签署 CLA 协议。

什么是 [CLA](https://www.apache.org/licenses/contributor-agreements.html)？

签署 CLA 协议 https://cla-assistant.io/
-->

### [可选] 配置 `SSH-key`

在本地生成 [`ssh-key`](https://www.ssh.com/ssh/keygen/) 并填写在 GitHub.com 的[`SSH and GPG keys`](https://github.com/settings/keys)页面.

### [可选] 配置本地 git 账号

```bash
git config user.name abc
git config user.email abc@def.com
```

### [可选] GitHub Desktop

如果您是 Windows 用户，也可以使用[GitHub Desktop](https://desktop.github.com/).

## 步骤

### Step 1: 通过 GitHub Fork

1. 访问 [https://github.com/seccome/whoiswho](https://github.com/seccome/whoiswho)
2. 点击右上角 `Fork` 按钮创建远程分支。

> 欢迎点击 `Star` 按钮收藏本项目。

## Step 2: 将分支克隆到本地

- clone 代码：

```bash
mkdir -p $work-dir # $work-dir 是你的本地工作目录
cd $work-dir
git clone git@github.com:$user/whoiswho.git
# 或: git clone https://github.com/$user/whoiswho.git

cd $work-dir/whoiswho
git remote add upstream git@github.com:seccome/whoiswho.git
# 或: git remote add upstream https://github.com/seccome/whoiswho.git

# 由于没有写访问权限，请勿推送至上游主分支
git remote set-url --push upstream no_push

git remote -v
# 确认远程分支有效, 正确的格式为：
# origin    git@github.com:$(user)/whoiswho.git (fetch)
# origin    git@github.com:$(user)/whoiswho.git (push)
# upstream  https://github.com/seccome/whoiswho (fetch)
# upstream  no_push (push)
```

## Step 3: 从本地main分支创建并切换工作分支

```bash
git pull upstream main
git checkout -b $my-work
```

通常，会有多个分支/pull request在并行开发、review。

## Step 4: 本地开发 (TODO)

### 代码风格

### 添加测试

### 运行测试

## Step 5: 保持本地与upstream同步

```bash
git checkout main
git pull upstream main
git checkout $my-work
git rebase main
```

git rebase main 过程中可能有多处冲突需要合并, 使用 `git add`和`git rebase --continue`。

### Step 6: Commit

提交代码更改

```bash
git add $new-files # 添加或者修改文件
git commit -a
```

### Step 7: Push

代码更改完成或需要备份代码时，将本地仓库创建的分支 push 到 GitHub 端的远程仓库：

```bash
# 首次 push
git push --set-upstream origin $my-work # git push
# 再次 push:
git push --force
```

### Step 8: 创建 pull request

1. 在浏览器点击你的[仓库](https://github.com/$user/whoiswho)
1. 点击 `my-work` 分支旁的 `Compare & pull request` 按钮。

### Step 9: 代码审查

公开的 pull request 至少需要两人(TODO)审查，代码审查包括查找 bug，审查代码风格等。

请根据审查意见重复 Step 5 - Step 9，直到最终该 pull request 被项目合并。

###  [可选] Step 10: 清理

- 本文采用一个独立的分支进行更改。合并后，这个分支已无用处。

```bash
git checkout main
git branch -D $my-work
```

- 此外，如果想将 commit 提交至 origin master，需要 hard reset 主分支：

```bash
git checkout main
git fetch upstream main
git reset --hard upstream main
git push --force origin main
```
