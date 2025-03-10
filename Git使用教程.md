# Git 使用教程

# 一、说明

## 1.1 为什么将 Git 作为首位教程

Git 是一款分布式的、可供多人开发的版本控制软件，在多人项目开发当中用于控制项目版本，方便执行该场景下的提交、合并、回退等操作。如果你不会使用 Git，那么你的成员将无法合并你的工作，这对于团队来说是灾难性的。所以新手入门，不管前后端，都应该从 Git 开始了解如何使用 Git！

## 1.2 如何学习本教程及文档中心其他教程

文档中心存在的初衷就是为了后来的学弟学妹可以快速掌握一些基础的知识而搭建的，你们可以在连接好项目组宽带，或者 WIFI 来访问[603 文档中心]()，从这里面访问其它文档资源。

找到文档后可以根据文档指示搭建好对应环境，复制里面的代码或指令自己动手实践，对工具的原理有一定了解并且熟悉常用指令之后就可以熟练运用该工具。所以你们了解工具文档介绍的原理和基础指令即可进入开发。

## 1.3 学习与实践 Git 的方式

在项目中主流的使用 Git 的方式有两种：使用 IDE 的可视化提交按钮和终端指令执行。个人建议是使用终端指令执行 git 操作，这样你可以让自己对 git 的理解更加深刻

# 二、git 运作原理

## 2.1 原理图示与运行流程

![](https://github.com/theOnlyUnique/GitFortune/blob/master/img/git工作流程.png)







## 2.2 概念补充

-  Workspace：工作区，就是你写代码的 IDE 所看见的区域
-  Index / Stage：暂存区，执行 add 和 stash 之后，你的代码将会被放入该区域，不过 add 会对其进行追踪
-  Repository：本地仓库，执行 commit 之后将记录保存到本地
-  Remote：远程仓库，执行 push 之后将本地的记录与远程对比再合并

## 2.3 文件的状态

-  Git 概念当中的文件状态

![文章](https://github.com/theOnlyUnique/GitFortune/blob/master/img/文件跟踪状态.png)



**Untracked**: 未跟踪, 此文件在文件夹中, 但并没有加入到 git 库, 不参与版本控制. 通过 git add 状态变为 Staged.

**Unmodify**: 文件已经入库, 未修改, 即版本库中的文件[快照](https://so.csdn.net/so/search?q=快照&spm=1001.2101.3001.7020)内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为 Modified. 如果使用 git rm 移出版本库, 则成为 Untracked 文件

**Modified**: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过 git add 可进入暂存 staged 状态, 使用 git checkout 则丢弃修改过, 返回到 unmodify 状态, 这个 git checkout 即从库中取出文件, 覆盖当前修改

**Staged**: 暂存状态. 执行 git commit 则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为 Unmodify 状态. 执行 git reset HEAD filename 取消暂存, 文件状态为 Modified

-  VSCode 当中文件的状态

**U**：Untracked，未追踪，一般是新增文件时出现

**M**：Modified，文件已追踪已修改，但是未进入暂存

**A**：Added,文件已加入暂存区

# 三、项目 Git 常用指令

掌握这部分可以解决项目开发下 90%的场景遇到的问题

```
// 初始化项目
git init
// 拉取项目
git clone https:www.github.com/xxx.git
// 给远程仓库取别名，做映射便于使用
git remote add origin https:www.github.com/xxx.git
// 修改主机名映射信息
git remote set-url origin https:www.github.com/xxx.git
// 将所有文件添加到暂存区
git add .
// 将当前分支复制一份当做xxx分支，并切换过去
git checkout -b xxx
// 跳过ESLint校验提交代码
git commit --no-verify -m "xxx"
// 将A分支推送到远程仓库的B分支，并且建立联系
git push -u origin A:B
// 强制回退分支到指定hash码
git reset --hard 012789abcd012789abcd012789abcd012789abcd
// 查看本地所有tag
git tag
```



# 四、场景举例

## 4.1第一次使用

首先必须添加个人信息

```
git config --global user.name "Liu Qidong"
git config --global user.email "254****216@qq.com"
```

## 4.2将本地开发了很久的项目推送到新仓库

一些常用步骤

```
git init
git remote add origin "https:remote-url"
// 如果已经存在相同的主机名，执行以下命令替换
git remote set-url origin "https:remote-url"
// 绑定上下游分支,后续可直接用 git push复刻本次提交
git push -u origin xx分支名
```

## 4.3回退分支

适用于强制回退

```
// 查看需要回退的提交的hash值，假如为
// 012789abcd012789abcd012789abcd012789abcd
git log
git reset --hard 012789abcd012789abcd012789abcd012789abcd
// 这样所有记录将回到这个节点，但是回退中间的提交都会丢失
// 只想看看可以使用
git checkout 012789abcd012789abcd012789abcd012789abcd
```

## 4.4正常提交

```
git add .
git commit -m "554545"
git push origin A分支名:远程B分支名
```



# 五、Git 指令大全

## 5.1 项目初始化

-  git init

当你想将自己开发的项目结合上 git 进行版本控制时，可以使用该指令在当前目录创建一个本地仓库以进行版本控制。

此外，可以随便跟一个 name，代表在当前目录创建一个 name 文件夹，再执行`git init`

-  git clone \<url\>

当你想获取别人的代码到本地时，可以使用此指令

## 5.2Git 配置

-  git config --global user.name <"你的昵称，用于显示提交信息">

必填项，配置你的个人信息，不必要实名，显示你的昵称信息，用于提交到远程仓库

-  git config --global user.email <"你的邮箱">

必填项，配置你的邮箱，方便他人联系你

-  git config --list

查看当前 git 的配置

-  git config -e

弹出 git 的配置文件的 txt 文件，供你可视化修改

-  git config --global http.proxy \<127.0.0.1:PORT\>

设置 git 的 http 代理，解决 clone 在 Github 上的项目拉取不下来的问题

-  git config --global https.proxy \<127.0.0.1:PORT\>

设置 git 的 https 代理

-  git config --global --get http.proxy

查看 git 的 http 代理

-  git config --global --get https.proxy

查看 git 的 https 代理

-  git config --global --unset http.proxy

卸载 git 的 http 代理，用于切回国内网络的情况

-  git config --global --unset https.proxy

卸载 git 的 https 代理，用于切回国内网络的情况

## 5.3 项目拉取与推送

-  git fetch origin \<branchName\>

将远程仓库的项目，拉取到本地远程跟踪分支上，该远程跟踪分支表现为`origin/branchName`，相当于一个只读的本地分支。

我们切换到某个分支后，执行`git merge origin/branchName`,即可完成合并。

总的来说，`git fetch`只会将远程分支拉取下来，不会进行合并

-  git pull origin \<remoteBranch\>:\<localBranch\>

相当于执行了`git fetch `外加`git merge`,当远程和本地同名时，可以缩写为`git pull origin remoteBranch`

-  git push -u origin \<branchName\>

将本地的 branchName 分支设置为`origin/branchName`分支的上游

-  git push

假如当前分支名为 a，当 a 分支创建了上游，那么在 a 分支执行该命令，会自动将 a 分支推送到远程仓库的上游分支，否则其会提示还未创建上游分支

## 5.4 文件增添与撤销

-  git add \<fileName\>

将某个文件加入暂存区，需要全部加入，可使用`git add .`

-  git checkout \<branchName\>

将当前分支切换到 `branchName`,可以使用`-b`参数应对该分支不存在的情况，以此新建一个分支

-  git checkout [-- \<fileName\>]

将该文件的工作区内容使用缓存区中的内容进行替换，即丢弃当前文件更改

在不和分支名冲突的情况下，`--`可以省略。

使用`git checkout`可以全部撤销

-  git reset

将文件都撤回到上次 commit 时的状态

-  git reset --hard \<hashValue\>

将文件都撤回到上次 commit 时哈希值为 hashValue 时的状态

-  git revert \<hashValue\>

将项目以增量追加的形式恢复到 hashValue 时的状态，commit 会增长

-  git stash

将所有未 commit 的内容加入暂存区，独立放在一起

-  git stash pop

将所有缓存以合并的形式恢复到工作区，有冲突时需要手动解决

## 5.5 分支操作

该部分请查看`文件增添与撤销`,补充一些特殊的指令

-  git branch -a

查看本地所有的分支详情

-  git branch \<branch-name\>

创建一个本地分支，但是不切换

* git branch --contains <提交哈希>

查询某次提交包含在哪些分支里面，可以包含远程追踪分支，可以配合`git log --all --grep=<提交哈希>`使用

-  git branch -d \<branchName\>

删除一个本地分支

* git log

查看当前分支的所有提交信息详情，加上`--all`参数则是查看所有分支的提交信息详情

-  git checkout -

返回上一个分支

-  git merge \<branchName\>

将 branchName 合并到当前所在分支

-  git push origin --delete \<branch-name\>

删除远程跟踪分支，另一种写法是`git branch -dr <origin/branch>`

-  git cherry-pick \<hashValue\>

将某次提交值为hashValue时的代码状态，合并到当前的分支上，有冲突就需要解决

-  git rebase targetBranch workBranch

当多人开发的时候，总是基于某个版本分别拉取代码进行开发，所以合并代码的时候大家的版本只会有共同的祖先，但是却又很多冲突，这个指令会计算`targetBranch `和`workBranch`两个分支的共同组件，将`workBranch`的更改追加到`targetBranch `末尾并生成新的log

相当于`git checkout workBranch `加上`git rebase targetBranch ` 

其中`merge`和`rebase`作用差不多，但是前者按照时间线排列，后者按照指令操作进行记录合并。前者方便回溯，后者合并与审查更简洁

> 中途遇到冲突，合并完后会不在任何分支上，可以使用git rebase --continue继续操作
> 否则使用git rebase --abort放弃本次操作



## 5.6 远程仓库指令

-  git remote -v

查看本地的主机配置信息，一般一个主机名会有一对`fetch`和`push`地址

-  git remote add \<host\> \<url\>

对该项目的 host 绑定一个远程仓库地址，如果该主机已经绑定，则会失败。

注意，一个项目可以绑定多个 host，即可以映射多个仓库

-  git remote set-url \<host\> \<newUrl\>

将 host 对应的远程仓库地址进行修改

## 5.7 标签操作

标签是为了给某个提交打上特殊标注，相当于别名。可以用于纪念，也可以用这个标签代表该次提交的唯一标记。

-  git tag \<tagName\> [hashValue]

给当前分支打上一个 tag。如果附加提交哈希，那么就是为指定提交打上一个标签

-  git tag -a \<tagName\> [hashValue] -m \<附加消息\>

为当前分支打上一个附加消息的标签，称为附加标签。如果附加提交哈希，那么就是为指定提交打上一个附加标签

-  git tag [-l <通配规则>]

显示所有的标签，可通过`-l` 参数使用通配符进行查询

-  git show [tagName]

展示指定标签的详细信息。如果单独使用`git show`则展示最新一次提交的详细信息。

-  git tag -d \<tagName\>

删除本地指定标签

-  git push \<host\> \<tagName\>

因为 push 代码不会同时将 tag 提交上去，所以需要额外将某个标签推送到远程仓库。

-  git push \<host\> --tags

将所有 tag 推送到远程仓库

-  git push \<host\> :refs/tags/\<tagName\>

将指定的标签从远程仓库进行删除，也可以使用

`git push origin --delete <tagName>`

-  git checkout -b \<newBranchName\> \<tagName\>

根据标签，将指定标签的提交进行检出，并创建一个新的分支



# 六、提交类型

一个规范的 Git Commit 消息通常包含三个部分：**Header**、**Body** 和 **Footer**，通常情况下只有`Header`是必须的

**Header** 部分包括三个字段：**type**（必需）、**scope**（可选）和 **subject**（必需），通常不写**scope**。常见的`type`列出如下：

| 序号 |   type   |          应用场景          |                 备注                  |
| :--: | :------: | :------------------------: | :-----------------------------------: |
|  1   |   feat   |       添加了新的功能       |                                       |
|  2   |   fix    |       修复了某个bug        |                                       |
|  3   |   docs   |      只更改了文档部分      |                                       |
|  4   |  styles  |       修改了样式部分       |   不影响代码逻辑，即不影响代码逻辑    |
|  5   | refactor |      对功能进行了重构      | 既不是新增功能也不是修复bug的代码更改 |
|  6   |   perf   |          性能优化          |     比如图片加载，轻微的逻辑优化      |
|  7   |   test   |        添加单元测试        |                                       |
|  8   |  chore   |            杂项            |     不知道你写的是啥类型就用这个      |
|  9   |  build   | 构建系统或外部依赖项的变更 |         即工具链和依赖的变更          |
|  10  |  revert  |            回滚            |                                       |

> 示例：fix：修复了平台性能过强的bug
>
> 中英文冒号都行，建议中文，因为更宽更好看，后面打文字不用再切输入法。



# 七、参考链接

1.[图解 Git | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/git-graphical.html)

2.[gitReference/gitCommands.txt at master · GriefSeed/gitReference](https://github.com/GriefSeed/gitReference/blob/master/gitCommands.txt)

3.[Git_List/README.md at master · ZJF-Coder/Git_List](https://github.com/ZJF-Coder/Git_List/blob/master/README.md)

4.[Git 中文件的 4 种状态\_git 中文件状态-CSDN 博客](https://blog.csdn.net/alan418/article/details/106629307)

5.[Git 分支和文件名重名的时候如何切换分支\_git 新旧版本文件名重复-CSDN 博客](https://blog.csdn.net/weixin_43889618/article/details/119916947)

6.[Git 基础 - git tag 一文真正的搞懂 git 标签的使用-CSDN 博客](https://blog.csdn.net/qq_39505245/article/details/124705850)

7.[git 删除远程的 tag_git 删除远程 tag-CSDN 博客](https://blog.csdn.net/chuyouyinghe/article/details/114184913)

8.[git rebase详解（图解+最简单示例，一次就懂）-CSDN博客](https://blog.csdn.net/weixin_42310154/article/details/119004977)

9.[Git：Rebase和Merge之间的区别，看完这篇文章你就懂了！-CSDN博客](https://blog.csdn.net/xishining/article/details/115152823)

10.[git 代码提交规范，feat，fix，chore都是什么意思?_git chore-CSDN博客](https://blog.csdn.net/chenyajundd/article/details/139322838)
