## PID

> 使用 `glances` 查看所有进程情况
> 再使用ps查看指定进程详情

```shell
ps -f -p PID
```

> 强制kill进程，如果无权限则加上sudo

```shell
kill -9 PID
sudo kill -9 PID
```

>  查询服务器pid对应用户

```shell
ps -f -p PID
```

> 查询pid对应的开始时间

```shell
 ps -o lstart -p PID
```

## SYNC

> 同步数据, 已存在则跳过,  rsync[详情](https://www.ruanyifeng.com/blog/2020/08/rsync.html)

```shell
rsync -avzu --progress source_file  dest_file
```

## 查看硬盘容量

```base
dust -d 2
```

```bash
df -h
```
## 批量删除文件
删除7日前修改的文件, 其中 `-type f`限制了查找类型为文件, 如果不加则也会删除目录
```
find . -type f -mtime +7 -delete
```
