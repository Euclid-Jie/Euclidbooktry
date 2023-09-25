## PID

> 查看进程详情

```shell
ps -f -p PID
```

> 强制kill进程，如果无权限则加上sudo

```shell
Linux kill -9 PID
sudo Linux kill -9 PID
```

>  查询服务器pid对应用户

```shell
ps -f -p PID
```

## SYNC

> 同步数据, 已存在则跳过,  rsync[详情](https://www.ruanyifeng.com/blog/2020/08/rsync.html)

```shell
rsync -avzu --progress source_file  dest_file
```

