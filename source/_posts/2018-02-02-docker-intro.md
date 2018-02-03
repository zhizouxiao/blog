---
title: docker 入门
date: 2018-02-02 17:12:17
tags: docker
---

### docker 入门

1. linux启动docker服务
sudo systemctl start docker

2. 建立一个container
sudo docker run -i -t --name=fun ubuntu /bin/bash

3. 显示所有container
docker ps -a

4. 启动container
sudo docker start fun

5. 进入到已经启动的container
sudo docker attach fun

6. 守护container
sudo docker run -i -t --name=daemon -d ubuntu /bin/bash -c "while true; do echo hello world; sleep 1; done"
查看日志
sudo docker logs -ft daemon

7. 检测container中的进程
sudo docker top daemon

8. 在container中执行命令
sudo docker exec -d daemon touch /etc/new_config
sudo docker exec -i -t daemon /bin/bash

9. 停止contianer 
sudo docker stop fun

10. docker退出后，重新启动 
sudo docker run -i -t --name=daemon2 --restart=always -d ubuntu /bin/bash -c "while true; do echo hello world; sleep 1; done"

11. 删除container
sudo docker rm fun
sudo docker rm \`docker ps -a -q\`

### 镜像images

1. 列出所有images
sudo docker images

2. 下载image
sudo docker pull fedora

3. 搜索image
sudo docker search puppet

4. build
默认从失败的步骤继续build
sudo docker build -t="zhizouxiao/static_web" . 
指定无缓存
sudo docker build --no-cache -t="zhizouxiao/static_web" . 

5. 查看image历史
sudo docker history c7039fdaee4d

6. 运行build之后的image, host端口为8080，container端口为80
sudo docker run -p 8080:80 --name=static_web zhizouxiao/static_web nginx -g "daemon off;"
