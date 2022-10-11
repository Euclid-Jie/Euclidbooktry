记录使用Git过程中的总结，主要包括Git命令，GIt与各种IDE的配置，Git与GitHub远程仓库连接

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

- 查看是否有变动

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













