# 镜像操作

- docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
OPTIONS说明：

-a :拉取所有 tagged 镜像

--disable-content-trust :忽略镜像的校验,默认开启
```

# 数据迁移

- win
```
wsl --export docker-desktop-data <your-dir>\docker-desktop-data.tar
wsl --export docker-desktop <your-dir>\docker-desktop.tar
wsl --unregister docker-desktop-data
wsl --unregister docker-desktop
wsl --import docker-desktop-data <your-dir>\docker-desktop-data <your-dir>\docker-desktop-data.tar
wsl --import docker-desktop <your-dir>\docker-desktop <your-dir>\docker-desktop.tar
```
# 空间清理
- docker system prune          
    清理磁盘，删除关闭的容器、无用的数据卷和网络，以及dangling镜像（即无tag的镜像）。
- docker system prune -a       
    删除**将没有容器使用Docker镜像** + docker system prune

# docker容器与宿主机进行文件传输 

- 复制文件到container:       
`docker cp <main machine path> <your container name/id>:<file path>`

- 从container复制文件到宿主机:    
`docker cp <your container name/id>:<file path> <main machine path>`