# docker


c/s架构， docker守护线程作为服务端接受来自客户端的请求，并处理， 服务端与客户端可以采用socket或restful api接口通信

采用runC和containerd容器格式

从容器中拷贝文件:  docker copy sourcePath targetPath

创建并启动容器： docker run -t -i imageName /bin/bash

启动容器： docker satrt containerName

结束容器： docker stop contaienr

进入容器内部：
    1. attach: docker attach containerName
    2. exec: docker exec -it conatinername bash 

删除容器： docker rm container 

删除镜像： docker rmi imageName

创建数据卷： docker volume create volumeName

查看数据卷： docker volume ls; docker volume inspect volumeName

删除数据卷： docker volume rm volumeName; docker volume prune(清理无主的数据卷)

挂在数据卷到容器：
    1. 在容器启动时添加参数： --mount source=volumeName,target=containerPath


挂在主机目录作为数据卷：
    1. 在容器启动时添加参数： --mount type=bind,source=主机目录,target=容器目录