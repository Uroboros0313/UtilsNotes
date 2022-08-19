# 镜像操作

- docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
OPTIONS说明：

-a :拉取所有 tagged 镜像

--disable-content-trust :忽略镜像的校验,默认开启
```

# 常用命令

- 新建容器并运行        
`docker run -it imageID /bin/bash`

- 进入正在运行的容器(exit之后不会自动停止容器)          
`docker exec -it containerID(Name) /bin/sh` 

- 进入正在运行的容器(exit后会停止容器)      
`docker attach containerID(Name)` 

- 重命名容器     
`docker rename <old_container_name> <new_container_name>`

- 复制文件到container:       
`docker cp <main machine path> <your container name/id>:<file path>`

- 从container复制文件到宿主机:    
`docker cp <your container name/id>:<file path> <main machine path>`
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
- 清理磁盘，删除关闭的容器、无用的数据卷和网络，以及dangling镜像(即无tag的镜像)。   
`docker system prune`          
    
-  删除**将没有容器使用Docker镜像** + `docker system prune`       
`docker system prune -a`


