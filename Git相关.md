记录使用Git过程中的总结，主要包括Git命令，GIt与各种IDE的配置，Git与GitHub远程仓库连接

# 使用GitBash

## Git配置

Git官网下载并安装，配置邮箱

## Git命令

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











