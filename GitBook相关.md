`GitBook`在线挂载时，需要注意：章节内容第一行请勿使用标题格式，否者会造成无法显示文章内容

# 关于`GitBook`本地使用

更多教程看查看[其它博主的分享](https://www.chengweiyang.cn/gitbook/gitbook.com/edit.html)

有关更多`gitbook`命令可使用`gitbook help`获取

## 下载GitBook并安装

需要使用`node`工具，没有`node`的需要先安装`node`

> `GitBook`已停止维护，需要使用旧版本的`node`，附V10下载[链接](https://nodejs.org/download/release/v10.24.1/node-v10.24.1-x64.msi)

- 安装`gitbook-cli`，如遇到权限问题，使用管理员权限运行CMD，后再执行

  ```shell
  npm install -g gitbook-cli
  ```

> 此时`GitBook`并未执行安装，在首次执行`gitbook init`后，将执行安装

## 书本初始化

在文件夹内下，打开`cmd`窗口，进行初始化

```bash
gitbook init
```

初始化后，目录下会出现`README.md、SUMMARY.md`两个文件

- `README.md`表示对书本的介绍
- `SUMMARY.md`用于控制书本的结构

## 书本构建

- 自动生成文件

  在`SUMMARY.md`中写入目录后再次初始化，会自动创建文件目录及文件，例如：

  ```markdown
  # SUMMARY
  * [Chapter1](chapter1/README.md)
    * [Section1.1](chapter1/section1.1.md)
    * [Section1.2](chapter1/section1.2.md)
  * [Chapter2](chapter2/README.md)
  ```

- 构建书本

  ```bash
  gitbook build
  ```

  会生成一个`_book`目录，储存`html`格式的书本内容

## 书本查看

- 启动`serve`，会返回一个本地端口，即可在浏览器中查看书本

  ```bash
  gitbook serve
  ```

- 发布书本为指定格式

  ```bash
  gitbook pdf
  ```

# `GitHub Pages`关联`GitBook`

为GitHub仓库设置说明文档，使用此方式非常合适且便捷

## 书本初始化

同样需要在项目路径启动`CMD`，运行`gitbook init`进行初始化，会自动创建`README.md`和`SUMMARY.md`

> 如果项目已有`README.md`，则只会新建`SUMMARY.md`，已有的`READEME.md`不会丢失
>
> 如果书籍的内容在项目路径下的一个文件夹内，本例中为Wiki，则直接在Wiki下进行init即可

## 书本构建

`SUMMARY.md`文件控制了整书本的结构，一般来说最多构建至二级目录

编辑完成`SUMMARY.md`，使用`build`命令构建

```shell
gitbook build Wiki docs
```

> 代码示例为：`Book` 相关内容全部放在Wiki目录下， 新生成的`html`文件将储存至`docs`目录下
>
> gitbook build [书籍路径] [输出路径]，如果不指定参数，将默认使用项目目录下所有文件参与构建Book，并输出到_book目录下
>
> 需要注意的是，Wiki中的README.MD可以有

## 书本查看

使用`serve`命令可在本地400端口查看书籍

```shell
gitbook serve Wiki
```

>代码示例为：`Book` 相关内容全部放在Wiki目录下
>
>gitbook serve [书籍路径] [output]

## 关联`GitHub Pages`

- 首先确保此项目在`GitHub`上的仓库状态为公开
- 项目设置>`Pages`>`Branch`，设置分支及书籍`html`文件路径，本例中为`docs`

![image-20230527181536349](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/202305271815515.png)

- 查看`pages`，`url`为：https://[GitHub用户名].github.io/[仓库名]

# `Gitbook`网页端服务

如果使用网页端的`GitBook`服务，可以不用安装`GitBook`。事实上安装`GitBook`会遇到很多苦难，所以直接使用`GitBook`网页端是一个很不错的选择。

## 注册`GitBook`账号

网站上注册一个号，可能需要梯子。

## 关联`GitHub`

关联`GitHub`后，可以将一本书与仓库绑定，我习惯的做法是，本地写内容，`Push`到`GitHub`上，`GitBook`会自动根据仓库变动，更新书本内容。

## 查看书本

`GitBook`的优秀之处就是不需要向本地一样，构建书本、启动服务，直接会有一个网址，即为书本的网页阅读模式。[例如本书](https://euclid-jie.gitbook.io/gitbookdemo/)

## 注意事项

有些目录不是必须的，比如`_book`，不必`Push`至仓库，`GitBook`需要识别的`SUMMRAY.md`及其中的章节文件。

换言之，其实如果确定使用`GitBook+GitHub`的方式创建书本，只使用得到`gitbook init`。
