> 服务器上安装了docker 及 docker-compose

## 1. 安装

在 cluster 目录执行

```bash
  docker-compose up -d
```

> 注意：如果提示 `WARNING Memory overcommit must be enabled!`

这是因为 Redis 在启动时会检查操作系统的内存 overcommit 设置，而默认情况下，Docker 容器中的内存 overcommit 是被禁用的。
要解决这个问题，您可以按照以下步骤启用 Docker 容器的内存 overcommit：

打开宿主机上的 `/etc/sysctl.conf` 文件以编辑它：

```shell
  sudo vim /etc/sysctl.conf
```

在文件末尾添加以下行：

```shell
vm.overcommit_memory=1
vm.overcommit_ratio=50

```

vm.overcommit_memory=1 表示启用内存 overcommit，
vm.overcommit_ratio=50 表示将 overcommit 的比率设置为 50%。

保存并关闭文件。

在终端中运行以下命令以使更改生效：

```shell
  sudo sysctl -p
```

重新启动 Docker 服务：

```shell
  sudo systemctl restart docker
```

## 2. 配置

### 进入容器 

> docker exec -it redis1 sh

1. 建立集群
  ```shell 
  redis-cli --cluster create redis1:6379 redis2:6379 redis3:6379
  ```
2. 查看集群信息
  ```shell
  redis-cli --cluster check redis1:6379
  ```
