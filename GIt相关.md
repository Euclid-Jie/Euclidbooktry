# Git相关

记录使用Git过程中的总结，主要包括Git命令，GIt与各种IDE的配置，Git与GitHub远程仓库连接

## Git配置

Git官网下载并安装，配置邮箱

## Git命

- 初始化一个仓库

  ```bash
  git init
  ```

- 储存

  ```bash
  git stash save "本地缓存内容标识" # 创建储存
  git stash list # 查看有哪些储存
  git stash clear # 清除所有储存
  ```

- 添加文件

  ```
  git add
  ```

- 查看是否有变动

  ```
  git status
  git status -s
  git diff f
  git diff --cached或者git diff --staged
  ```

  

- 提交

  ```bash
  git commit
  ```

- 推送

  ```bash
  git push
  ```

  查看提交记录

  ```bash
  git log
  ```

  

















