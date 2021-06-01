---
title: 高效的代码管理Git
date: 2021-06-01
tags: git
categories: tools
summary: Git是当今最流行的开源的版本管理系统，我们应当学会灵活使用它，让工作变得事半功倍。
---


---
## git介绍
---

### 历史和发展
---

Git诞生于一个充满争议和创举的时代。

#### 1991-2002

Linux内核开源项目有着众多的开发者，而大多数的内核维护工作在提交补丁、保存归档的事务上花费了太多时间。为什么呢？因为在2002年之前，世界各地的开发者把自己的改动通过diff生成补丁，再发给Linus(Linux之父)，Linux本人通过**手动**方式合并代码！

#### 2002-2005

但是随着代码量的增加，开发者们认为这样的管理方式效率太低，Linus于是选择了(商业的)BitKeeper作为Linux的版本控制系统，BitKeeper的母公司出于人道主义，单独授权了Linux社区免费使用该版本控制系统。然而好景不长，在2005年，社区中有人试图破解BitKeeper协议的举动被该公司发现，随即收回了Linux社区的免费试用权，Linux社区再度陷入窘境.....

#### 2005-Now

Linus他和自己的团队花了<span style="background-color:#F9FC17">两周</span>的时间，用C写了一个**分布式**版本控制系统Git，一个月后，Git已经部署在了Linux社区中了。这一系列的操作不得不让人对Linus这个天才的感叹。直至今日，Git仍然是当今最好的代码版本控制系统。


### git与svn
---

| 比较项 | SVN | Git |
| :--- | :--- | :--- |
| 系统 | 集中式(便于文档管理)<br>克隆1w commit的项目，需要1h | 分布式(便于代码管理)<br>克隆1w commit的项目，需要1min |
| 灵活性 | 所有的操作都必须与中央服务器交互<br>一旦出故障则无法工作 | 支持离线工作，即使服务器故障也没事<br>可在本地进行各种操作，效率高 |
| 安全性 | 较差，需要定期备份 | 较高，人均一个库，充当备份作用 |
| 分支 | 切换一个分支=copy整个项目<br>创建分支，会影响全组人员，大家都会有该分支 | 可以在任意节点创建分支，本地分支不会影响其他人，支持**cherry-pick** |
| 版本控制 | 保存版本之间的差异，通过**版本号**进行控制<br>每次操作都会产生(全局的)高版本号 | 只关心项目整体的数据变化<br>通过**hash值**进行控制 |
| 权限 | 权限管理很严格，可按照组、目录进行权限控制<br>每个目录下都有一个.svn文件 | 没有严格的权限控制，只有角色划分<br>在主目录下有.git目录 |

![svn-git](/pics/git/git_vs_svn.png)



---
## git操作
---

### 流程概览
---

git的基本流程有4个：stage，commit，push，pull。

![git-flow](/pics/git/git-flow.png)

#### 初始化

这里的Workding Directory就是我们当前的工作目录，当我们克隆一个项目/初始化一个仓库后，我们的状态为**最新**。

```bash
git clone https://github.com/Lucky-Jenny/Code_Study.git
git status
```

![init-status](/pics/git/status-uptodate.png)

#### 改动

在上述状态下，我们做的所有改动都将会被监视，分为`untracked`和`unstaged`两个状态。

![unstaged-status](/pics/git/status-unstaged.png)

- untracked: 不属于本仓库内的文件(新添加的)；
- unstaged: 修改了属于本仓库内的文件；

#### 暂存

> 暂存区的作用：区分当前仓库中哪些文件/目录需要提交。

当我们的改动需要**暂时**保存起来，可以用add/rm进行暂存。不暂存的哪些文件则不会被提交(状态保持)。

![unstaged-status](/pics/git/status-stage-part.png)


此时，切换到其他分支，我们查看状态，可以发现所有的分支都能显示了改动。

![unstaged-status-2](/pics/git/status-stage-part-2.png)

> 暂存区的改动对**所有分支**都是有效的。

#### 提交

> 本地仓库的作用：本地项目的正式改动保存，待确认无误推送到远程仓库。

我们把暂存区的改动进行提交

```bash
git commit -m "Add Atoi.c xxx"
git status
```

![commit-status](/pics/git/commit-1.png)

提交之后，本地仓库比远程仓库多了一次改动。这时我们切换到别的目录，却**没有该提交**。

> 本地仓库的提交**只对当前提交的分支有效**，对其他分支无效。

其实这一点是可以推理的，试想：若每次提交都每个分支上，那么每个分支的所有改动都是一样的，那分支的意义在哪里呢？

#### 分支

分支(branch)是版本管理中非常有效的机制，例如一个项目中，我负责模块A，他负责模块B，我们可以在各自的分支中编辑代码，这样不同模块的代码在分支合并时就不会发生冲突。

```bash
git branch -a          # 查看本地 & 远程的所有分支
git checkout master    # 切换到分支<master>
git merge script       # 在<master>中把<script>合并进来
```

我们通过`tig`(git的可视化工具)查看merge之后的master仓库：

![tig-merge](/pics/git/merge.png)

#### 标签

标签(tag)是对项目某个阶段进度的一种标记方式，我们可以通过标签去找到当时的项目仓库改动。

```bash
git tag study-v1.1      # 添加标签
git tag -l              # 查看所有的标签 
```

![tig-tag](/pics/git/tig-tag.png)

注意：<span style="background-color:#F9FC17">标签不会随着git push添加到远程仓库中</span>。如果我们想把标签推送至服务器，记住如下指令：

```bash
git push origin --tags      # 仅推送标签，不推送其他任何改动
```


### 远程仓库和本地仓库
---

远程仓库其实就是远程架设了一个服务器，供开发成员进行推送和拉取操作。

#### 推送

推送：`git push`。形象地理解为把所提交的改动发送到远程的服务器上，只有推送到远程仓库之后，其他的组员方可从该仓库获取改动。注意：我们既可以推送新的改动，又可以推送过去**重新编辑**的改动，但是极其不建议后者的操作。为什么呢？我们来看下面这个例子：

ABC三位开发人员共同在package/wifi/目录下进行为期一周的开发任务。在第6天的时候，A发现B在第1天的提交X有问题，于是他修改了X：

```bash
git rebase -i <Commit-X>
# 将要修改的提交ID，前面的`pick`改成`edit`，保存退出。
# 自动弹出该提交的信息，修改完保存退出。
# 此时HEAD应该回到原来的位置，若没有的话则执行以下操作：
git rebase --continue
```

注：该方法会<span style="background-color:#F9FC17">更改从X到HEAD的所有commit的hash值</span>。

与此同时B和C基于第5天的仓库进行**本地**的修改。A向远程仓库推送X的改动之后，B和C从远程仓库获取X的改动，此时会发生冲突(*本地仓库最新是第6天的改动，而远程仓库是第5天的改动*)，导致B和C**本地的改动直接作废**。这是因为从第一天到第5天已经提交了许多改动，即使B和C本地`reset`到第一天的代码，仍然无法兼容第6天的改动。

因此，修改过去的提交，我们建议采用以下两种方式：

```bash
# 方法一：revert
git revert <Commit-ID>       # 原来的改动和这次的撤销都保存在历史中
# 方法二：reset
git reset HEAD~2          # 向后回滚两次改动，保留当前的改动
git reset <Commit-ID>     # 回滚到过去某一次的改动
git reset --hard HEAD~4   # --hard 强制回滚，所有之前的改动全部删除
```

#### 拉取

拉取：`git pull`。在流程图中，我们会发现拉取的方向和另外两个动作是一致的，即`fetch`和`checkout`。这里就要好好叙述他们的区别：

```bash
git pull                 # 从远程仓库获取全部分支的最新改动，到工作区。
git fetch                # 从远程仓库获取全部分支的最新改动，到暂存区。
git fetch origin master  # 从远程仓库获取<master>分支的最新改动。
git checkout leetcode    # 切换到<leetcode>分支获取最新改动，到工作区。
```

综上，我们可以总结：

> 当获取当前分支的改动时，git pull = git fetch + git checkout \<branch\>



---
## 实际应用
---

在实际的工作环境中，也会遇到许多问题，针对这些问题可以有许多的解决办法，我们希望采用最佳的方法去解决。

### 遇到的问题
---

#### 工作区的暂时备份

> A正在修改代码尚未完成，此时有紧急的问题需要优先处理，应该如何快速保存当前的任务状态？

最简单的方法当然是：COPY。但反复的复制粘贴，其实效率并不高，我们期望有一个指令能够迅速备份，迅速还原：stash。

```bash
git stash           # 将当前工作区中的改动保存起来，还原现场。
git stash pop       # 把先前保存的工作区修改，恢复出来。
git stash clear     # 丢弃之前保存的工作区的修改。
```

注：<span style="background-color:#F9FC17">stash不保存untracked文件</span>，只保存unstaged文件。

#### 查看具体的提交信息

> A想知道在data_select.c中的134行代码是**谁在何时**修改的。

```bash
# 方法一：tig
tig -> g(grep):firmware       # 根据关键词，在tig中查找
# 方法二：blame
git blame -L 133,135 data_select.c
```

#### 二分法溯源

> 现有一个bug无法定位其根源，已知该bug是发生在tag <V1.2>和tag <V1.6>之间，而这两个标签之间有100+个提交，线性排查一定是最低效的，有没有高效率的方法？

git中有一个非常实用的检索工具：<span style="background-color:#00FA9A">git-bisect</span>，它采用的方式为**二分法**。

```bash
# 将HEAD移至<V1.2>和<V1.4>中间的提交
git-bisect start <V1.4> <V1.2>    # 注意顺序不要反
# 将HEAD回到原先(最新)的位置
git-bisect reset
```
当遇到分支时，比如有4个分支，则定位每个分支中的**最新节点**，分别测试：
- 若都存在该问题，则说明与这些分支无关，回到**主分支**中；
- 若**1**个分支存在，则追溯该分支；若**2**个分支存在，则追溯他俩上次分叉的位置；

![git-bisect](/pics/git/git-bisect.png)



### tig
---

tig作为git的可视化工具，对于开发人员来说是非常有用的工具。这里着重介绍一下tig相关的命令和快捷键：

#### 命令

```bash
tig              # 查看当前项目的改动历史
tig .            # 查看当前目录的改动历史
```

注意：只有当前目录为git仓库，tig才会有效。

#### 快捷键

进入到tig后，我们可以通过下面的快捷键来进行操作：

| 键 | 等价于 | 含义 |
| :--- | :--- | :--- |
| l | git log | 详细的改动历史 |
| r | git branch | 所有的分支 |
| s | git status | 当前暂存和临时的修改 |
| c | git stash pop | 查看临时保存的内容 |
| t | tree | 以树形结构查看仓库，\<Enter\>进入 \<,\>退出 |
| / | git branch | 当前提交中搜索关键词 |
| g | grep | 所有提交中搜索关键词 |

