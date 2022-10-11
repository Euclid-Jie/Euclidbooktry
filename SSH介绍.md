SSH是一种通信验证方法，一般用来实现免登录实现`GitHub`与本地的通信

如果你已习惯使用`Pycharm`进行`coding`工作，那建议你直接看本文最后一行

## 生成公钥和私钥

需要在`C:\Users\yourname\.ssh`目录下使用`cmd`窗口，如果`C:\Users\yourname`目录下没有`.ssh`文件夹，手动创建即可，或者直接在`C:\Users\yourname`此目录下使用`cmd`也可以

使用如下命令创建SSH对

```bash
ssh-keygen -t rsa -C "azureuser@myserver" -f "filename"
```

需要注意的是，`azureuser@myserver`为自己确定的标识符，一般为标记为你所要授权的平台的登录邮箱。

`filename`为生产的密钥对的文件名，如果需要生成多个秘钥对，请命名，以免覆盖。

生成过程中全程回车即可，最后会在`.ssh`目录下出现`filename.pub`、`filename`两个文件，第一个为公钥，需要放到远程中，第二个为私钥，用于通信时验证。

## 配置密钥到GitHub

为了使得本地的Git能够成功与GitHub中的远程仓库绑定，需要配置上一步生成的公钥。

进入到`GitHub`的`setting`中，选择`SSH and GPG keys`，点击`New SSH key`，将公钥中的内容复制并保存即可。需要注意的是，公钥可以使用记事本打开，保存时可能需要收取`GitHub`验证码。

除`GitHub`外的其他平台类似，当然我会选择在`Pycharm`中安装`GitHub`插件，然后通过登录账户实现本地与`GitHub`的通信，创建远程仓库并推送等操作都可以在`GitHub`插件的帮助下轻松完成，非常建议使用此种方式。