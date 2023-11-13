记录使用Git过程中的总结，主要包括Git命令，GIt与各种IDE的配置，Git与GitHub远程仓库连接

# 使用GitBash

## Git配置

Git官网下载并安装，配置邮箱、

- 配置邮箱和姓名

  ```shell
  git config --global user.email "youremail"
  git config --global user.name "yourname"
  ```

- 查看邮箱和姓名

  ```shell
  git config --global user.email
  git config --global user.name
  ```

## Git基础命令

- 初始化一个仓库

  ```bash
  git init
  ```

- 查看远程信息

  ```bash
  git remote -v # 查看远程仓库地址
  git remote # 查看远程仓库分支
  git remote show origin # 查看某个分支的具体信息
  ```

- 储存 

  不常用，主要是为了处理冲突

  ```bash
  git stash save "本地缓存内容标识" # 创建储存
  git stash list # 查看有哪些储存
  git stash clear # 清除所有储存
  git stash push -m "test stash" -p  # -p进入交互式窗口, 指定部分文件的部分内容进行stash
  ```

- 添加文件

  ```
  git add
  git add . # 添加所有新增文件
  ```

- 查看被管理的所有文件

  ```git
  git ls-files
  ```

  查看是否有变动

  ```
  git status
  git status -s # 简要查看
  git diff  # 查看具体文件内容变化
  ```

- 提交

  与`Pycharm`不同，提交前都需要`add`

  ```bash
  git commit -m "commit by bash"
  git commit --amend -m "commit by bash" # 修正提交
  ```

- 绑定远程仓库，需要先配置SSH并在远程创建好仓库

  ```bash
  git remote add origin git@github.com:[yourGitHubName]/[yourRepositories].git
  ```

  或者请在GitHub创建完仓库后，自己观察页面，上述代码可以直接复制到

- 推送

  ```bash
  git push
  ```

  查看提交记录

  ```bash
  git log
  ```


## Git显示中文乱码

`step1`设置`config`中的引用路径

```bash
git config --global core.quotepath false
```

将终端设置为`utf-8`编码

`step2`在`git bash`的界面中右击空白处，弹出菜单，选择`选项->文本->本地Locale`，设置为`zh_CN`，而旁边的字符集选框选为`UTF-8`。

## Git使用新设备打开时，无法显示提交记录

```shell
git config --global --add safe.directory F:/GitHub/my-project
git config --global --add safe.directory * 
```

## Git无法Push，显示超时

```shell
Failed to connect to github.com port 443:connection timed out
```

需要删除`git`的全局代理后重新`Push`

```shell
git config --global --unset http.proxy
git config --global --unset https.proxy
```

有时候是因为SSL证书问题，需执行

```shell
git config --global http.sslVerify "false"
```

一般来说，如果实在解决不了的话，可以挂梯子后使用github desktop解决

### 建议从以下几个方面排查

- 检查协议

  一般远程仓库的连接有两种方式，git或者http，直接检测远程链接即可

  ```
  git remote -v
  ```

  返回值开头是啥就是啥协议

- 不同协议超时有不同的排除流程
  - git对应的是ssh协议，检查自己的电脑的ssh私钥和github网站上的公钥是否配置好
  - http协议则是因为墙，试试代理
  - 建议使用git ssh协议，兼容性更好

# 使用Pycharm

## 创建Git仓库

### 本地创建

`Pycharm`的`VCS`支持一键创建，就没啥好说的了，一般情况下，是需要使用git命令行创建的，命令好像是 `git init`，因为git我是好久以前就配置好了的，`ssh`那些都弄好了，所以就记得不太清楚了，在此就只写目前我的工作流

### 远程创建

此前一直使用`GitHub`，我也是它的忠实用户，但是无奈某些原因连接实在是不稳定，所以使用`Gitee`临时替代。`Pycharm`默认的就是`GitHub`，所以直接在`Git`窗口中登录`Github`账号，然后设置一下远程仓库的名字就好了，因为我已经在`Github`中添加了电脑的`ssh`，所以后续的推送都很顺利

`Gitee`与`GitHub`就是大同小异的，也就是登录、创建再提交就成

## 分享本地项目至远程

使用`Pycharm`可以很方便分享，根据提示做好仓库命名和介绍就成，另外要注意可以在在`.git`中的`config`文件中修改`url`为`https://{username}:{password}@github{username}/project.git`格式，这样的话可以避免推送的时候让你再次登录

## 提交与推送

这块就是勾选要提交的文件，然后写一些说明就提交就好了，一段时间后我会推送到远程

一般最开始推送的时候，我会不推送导出数据文件，以及一些设置文件，这样在最后提交项目的时候，就可以直接从`GitHub`或者`Gitee`上下载压缩包，会比较方便一点，因为确实提交项目的时候那些个人设置文件，一起运行程序的导出文件都是不必要的，会使得压缩包冗大，设置文件甚至出现不知名错误

一旦推送后，最好不要进行修正，因为会导致需要先拉取远程更新，早进行提交推送，是`Git`流程出现合并分支的记录（主要是不美观）

## 分支与合并

这个功能是我新学的，很好用，在已有稳定版本的情况下，如果想做一些尝试性的修改，那么创建一个分支，在分支上修改并测试稳定后，将分支合并到原分支上，然后删除分支就可以了，这个功能真是让我赞不绝口

## 删除分支

本地的分支合并后，就可以直接删除了，但是远程的分支必须保证该分支表示`master`（主要）分支后，才能删除 ，如果是主要分支，那需要在`GitHub`或者`Gitee`上进入该仓库进行修改后再删除

## Git中的一些命名

	一般命名是：仓库名/分支名，一般本地仓库不标注直接是分支名master，对应的远程仓库一般叫：origin/master，当然这些就只是名字，是为了便于我们区分，因为使用时间较短，目前我还没有形成自己的命名标准。

新分支的时候，可以根据分支需要进行命名（可以为汉字）

# 使用VsCode

近期的工作都在Vscode中开展, 主要是连接服务器开发, Vscode更方便, 顺便记录一下VsCode中的git管理

## Git Graph插件

> VsCode中热度最大的git插件应该是git lens, 但是需要收费, Git Graph是一款非常类似Pycharm自带git管理的插件

得益于Git Graph这款插件, 使得在VsCode中进行git管理, 非常方便。有非常清晰的可视化分支, 并可以通过右键方式进行诸如, checkout, merge, rebase等操作

## merge or rebase ? 

> merge 和 rebase为git中进行分支合并时非常常见的操作, 网络上各种介绍很多, 不再班门弄斧

merge 和 rebase有着不同的常见, rebase会使得git历史呈现一条直线. 尽可能整洁, 并在PR时不会冲突(因为在rebase中已经提前解决); 而merge会使得分支溯源更为容易, 会清晰记录分支的走向

对我个人而言, 公司的项目多人参与且contribute较为严格, 使用rebase; 个人项目往往各种奇思妙想比较多, 故使用merge

## 如何借助Git Graph进行merge ?

> 定心丸: 只要不push到远程, 无论何种操作都能通过reset复原, 可大胆操作
>
> 后悔药: 如果在进行merge, 或者正在解决冲突途中, 想退出, 执行`git merge --abort`即可

确保自己处于master分支上, 选择dev分支右键进行`merge into current branch`, 如果有冲突(出现合并冲突), 则解决冲突, 完成后实现merge

## 如何借助Git Graph进行rebase ?

> 与merge一样, 仍旧有定心丸和后悔药可以吃, rebase途中退出, 执行`git rebase --abort`即可

确保自己处于dev分支上, 选择master分支右键进行`rebase current branch on Branch`, 一般来说都会遇到冲突, 有冲突解决冲突即可, 完成后实现rebase

参数-i可以在交互窗口中实现pick

# tipis

## 后悔药`reflog`

只要没被`push`到远程，本地的所有操作都可以通过`reflog`进行恢复

- 查看操作历史记录

    ```bash
    git reflog
    ```

    > demo中展示了此repo的最近几条操作记录，寻找出你需要回退的记录对应的hash头

    ```bash
    0c326f8 (HEAD -> dev/Jie/half_hour_features) HEAD@{0}: reset: moving to 0c326f8
    6426675 HEAD@{1}: reset: moving to 6426675
    cd44d32 (github/test, github/master, github/HEAD, master) HEAD@{2}: reset: moving to cd44d32
    6426675 HEAD@{3}: reset: moving to HEAD
    6426675 HEAD@{4}: rebase (finish): returning to refs/heads/dev/Jie/half_hour_features
    6426675 HEAD@{5}: rebase (pick): add AfterFog ClimbPeak
    80f1155 HEAD@{6}: rebase (squash): clear code and add unittest
    fe39abc HEAD@{7}: rebase (squash): # 这是一个 2 个提交的组合。
    d3a491e HEAD@{8}: rebase (start): checkout master
    2388e09 HEAD@{9}: rebase (finish): returning to refs/heads/dev/Jie/half_hour_features
    2388e09 HEAD@{10}: rebase (pick): add AfterFog ClimbPeak
    37a1991 HEAD@{11}: rebase (pick): fix distance to high
    5046792 HEAD@{12}: rebase (pick): add real_stats, corr_price_volume, large_volume
    d3a491e HEAD@{13}: rebase (pick): clear code and add unittest
    274dd93 HEAD@{14}: rebase (pick): add DeriveHalfHourFeatureFromTickTradeMinBar
    f9797f5 HEAD@{15}: rebase (pick): init branch
    ```

- 进行回退

  > 需要说明的是，进行回退后，将回到此条操作结束后的状态

  ```bash
  git reset --hard 6426675
  ```

  

## 其他

- 修改项目文件的*~.git\config*中的远程地址，可以直接修改http协议为ssh协议











