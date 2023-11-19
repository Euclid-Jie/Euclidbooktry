# 远程连接

`VSCode`连接远程主机进行开发真的很方便，下载插件`Remote-SSH`，然后设置`Config`文件，格式见下图，即可完成连接

```bash
Host github.com
  Hostname ssh.github.com
  IdentityFile "C:\Users\Ouwei\.ssh\id_rsa"
  Port 443
```

