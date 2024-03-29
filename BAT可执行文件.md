当有某项`cmd`指令需要被频繁操作时，每次打开`cmd`窗口后再输入指令运行非常麻烦

已开启`mongo`数据库服务为例，每次都要打开`cmd`窗口后运行

```shell
mongod --dbpath D:\Euclid_Jie\DBdata
```

所以将次命令作为一个可执行的`bat`文件，是非常有必要的，每次只要双击此`bat`就可以实现服务开启

## 下面解释`bat`生成流程

- 新建文本文件，更改文件类型为`bat`，将需要执行的命令直接写入文件即可，我会选择使用`sublime_text`进行更改文件类型和写入指令的操作，因为传统的记事本更改为`bat`后缀存在困难。

- 注意对`bat`文件命名为不要与本地命令相同，如果双击`bat`文件后，命令一直重复滚动，说明很可能遇到了此问题，需要对文件进行重命名，一般带几个中文，就不会有问题。
- 更进一步，将`bat`文件放在自己熟悉的地方，然后将其快捷方式放在桌面。这样既保证了不会误删文件，又可以对快捷方式的图标进行自定义。
  - 图标`ICO`文件生成[网站](http://www.ico51.cn/)
  - 图标下载[网站集合](https://zhuanlan.zhihu.com/p/431105940)，个人比较推荐的[网站](https://www.iconfinder.com/search/icons?price=free)

## 构建`bat`的几种`cmd`命令

- 切换路径

  ```shell
  E:  # 先切换磁盘
  cd E:\Euclidbooktry  # 再切换到路径
  ```

- 打开软件

  切换到路径后执行`exe`，或者将`exe`加入系统路径

  ```shell
  Typora.exe
  ```

- 打开文件

  ```shell
  SUMMARY.md  # 文件名+后缀
  ```

- 不关闭`cmd`窗口

  ```shell
  pause  # 回车后继续
  cmd    # 继续使用cmd
  ```

- 隐藏运行

  ```shell
  @echo off
  if "%1"=="h" goto begin
  start mshta vbscript:createobject("wscript.shell").run("""%~nx0"" h",0)(window.close)&&exit
  :begin  ## 命令写在下面
  SUMMARY.md 
  ```

- 查看进程并结束进程

  ```shell
  tasklist  # 查看进程
  taskkill /f /t /im Chrome.exe  # 关闭浏览器
  ```

- 使用`python`执行程序文件

  一般情况下直接

  ```python
  python demo.py 
  ```

  如果需要使用虚拟环境执行，需要先cd至虚拟环境目录（不能先激活再运行，会闪退）

  ```python
  cd D:\Program Files\Anaconda3\envs\scrapy
  python D:\Euclid_Jie\proxy_pool\proxyPool.py server
  ```

  
