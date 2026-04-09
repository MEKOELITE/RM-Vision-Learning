# 掌握 GitHub 协作

Git 是本地工具，GitHub 是把代码放到网上托管的平台。光会 Git，你只能一个人玩得转。加上 GitHub，才算是真正进入了协作开发的世界。

---

## 远程仓库基础操作

**克隆别人的仓库：**
```bash
git clone https://github.com/MEKO747/RM-Vision-Learning.git
```

克隆下来之后，默认远程名字叫 `origin`。

**查看远程信息：**
```bash
git remote -v
```

**关联自己的远程仓库（第一次本地初始化项目时）：**
```bash
git remote add origin https://github.com/你的用户名/你的仓库.git
```

---

## Fork —— 在自己的仓库里复制一份

如果想参与别人的项目，但没有推送权限，Fork 就派上用场了。

在 GitHub 网页上点一下 Fork 按钮，GitHub 会在你的账户下创建一个一模一样的副本。这个副本完全属于你，想怎么改怎么改。

之后：
```bash
git clone https://github.com/你的用户名/RM-Vision-Learning.git
```

---

## Pull Request —— 提交你的贡献

这是 GitHub 协作的核心流程。

1. 在你的 Fork 里新建分支，改代码
2. push 到你的远程仓库
3. 在 GitHub 上点 "Compare & pull request"

PR（Pull Request）就是"请求对方拉取我的代码"的意思。对方可以看到你改了什么，在哪里改，可以评论，可以要求你修改。

团队协作的时候，Code Review 就是通过 PR 完成的。

---

## 同步上游仓库

别人的原仓库（upstream）有新提交了，怎么拉到你 fork 的仓库里？

```bash
# 添加上游仓库的别名
git remote add upstream https://github.com/MEKO747/RM-Vision-Learning.git

# 拉取上游的最新代码
git fetch upstream

# 切换到 main 分支
git checkout main

# 合并到你的 main
git merge upstream/main

# 推送到你的远程仓库
git push origin main
```

第一次配置会麻烦一些，但这是值得的。之后每次上游有更新，重复这几步就行了。

---

## GitHub 上的几个重要概念

**Watch / Star / Fork**
- Star 相当于收藏
- Watch 是关注，有更新会通知你
- Fork 是复制到自己的账户

**Issues**
用来记录 bug、提需求、问问题。每个项目都可以开 Issue，团队成员通过 Issue 沟通。

**Actions**
CI/CD 工具，可以在代码 push 或 PR 的时候自动运行测试、部署。

---

## 常见的团队协作流程

以 RM 比赛项目为例，假设团队有三个人：

1. 每个人 fork 主仓库到自己的 GitHub 账户
2. 各自 clone 到本地，从主仓库的 main 新建自己的功能分支
3. 在功能分支上开发，完成后 push 到自己的远程仓库
4. 在 GitHub 上发起 PR，请求合并到主仓库的 main
5. 队长 review 代码，通过后合并

这个流程的好处是：所有人的代码改动都要经过 review，主仓库的 main 分支始终是可用的稳定版本。

---

## SSH Key 配置

每次 push 都要输密码很烦。配好 SSH Key 之后就不用了：

```bash
ssh-keygen -t ed25519 -C "你的邮箱"
cat ~/.ssh/id_ed25519.pub
```

把输出的内容复制到 GitHub → Settings → SSH Keys 里保存。

之后 clone 和 push 都走 SSH 协议，体验会好很多。

---

说实话，GitHub 协作的坑挺多的。权限问题、冲突问题、PR 写得一塌糊涂让人看不懂……但这些都是细节，多踩几次就熟悉了。

核心就一句话：**用 PR 来合并代码，用 Code Review 来保证质量。**
