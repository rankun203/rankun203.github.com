title: Docker with wordpress
date: 2016-03-06 16:36:50
categories:
- docker
tags:
- automation
- container
- docker
---

### UPDATE (2018-05-11):

Our team at [LodeStream](https://lodestream.com) has built a scaffold specifically for Wordpress development. You can check it out today and start play with it. Out of the box, it supports:

- Docker, Docker Compose
- Let's encrypt HTTPS
- Nginx as a reverse proxy with auto generated config
- Simplified domain configuration
- More information in the repo

Github repo: [lodestreams/wordpress-docker-compose](https://github.com/lodestreams/wordpress-docker-compose/)

----

_The original post:_

Install Docker on a Ubuntu:

Docker installation guide: https://docs.docker.com/engine/installation/linux/ubuntulinux/

If you don't know about datastore yet, refer to: https://getcarina.com/docs/best-practices/docker-best-practices-data-stateful-applications/

- `sudo docker create -v "$PWD":/var/lib/mysql --name dbstore mysql`
- `sudo docker create -v "$PWD":/var/www/html --name htmlstore php`
- `sudo docker run --name mysql -e MYSQL_ROOT_PASSWORD=password --volumes-from=dbstore -dp 3306:3306 mysql`
- `git clone https://github.com/youdarnet/wordpress.git`
- `sudo docker run -d --name wordpress --link mysql:mysql --volumes-from=htmlstore -p 80:80 youdar/wordpress`
- `sudo docker run -d --link mysql:mysql -e MYSQL_USERNAME=root --name phpmyadmin -p 3307:80 corbinu/docker-phpmyadmin`


Notes:

**添加新的 Wordpress 网站：**

使用现有的 MySQL 数据库。

- `sudo docker create -v "$PWD":/var/www/html --name wordpressNameStore php`
- `sudo docker run -d --name wordpressName --link mysql:mysql --volumes-from=htmlstore -p 800x:80 youdar/wordpress`

**其它提示**

- Remove dangling volumes: `sudo docker volume ls -f dangling=true | awk 'FNR > 1 {print $2}' | xargs sudo docker volume rm`
- Run a nginx at current dir: `sudo docker run -it --rm -v "$PWD":/usr/share/nginx/html -p 8081:80 nginx`

- `sudo docker inspect --format="{{json .Mounts}}" nginx | json_pp`

<!-- more -->

- sudo docker inspect --format="{{json .Mounts}}" nginx | json_pp

Ubuntu 安装 Docker

- sudo docker create -v `pwd`:/var/lib/mysql --name dbstore mysql
- sudo docker create -v `pwd`:/var/www/html --name htmlstore php
- sudo docker run --name mysql -v `pwd`:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=password --volumes-from=dbstore -dp 3306:3306 mysql
- git clone https://github.com/youdarnet/wordpress.git
- sudo docker run -d --name wordpress --link mysql:mysql --volumes-from=htmlstore -p 80:80 youdar/wordpress
- sudo docker run -d --link mysql:mysql -e MYSQL_USERNAME=root --name phpmyadmin -p 3307:80 corbinu/docker-phpmyadmin
- docker run -d -p 80:80 -p 443:443 -v `pwd`/sites-enabled:/etc/nginx/conf.d -v `pwd`/certs:/etc/nginx/certs -v `pwd`/log:/var/log/nginx -v `pwd`/app:/var/www/html --link wordpress:wordpress --name nginx nginx

添加新的 Wordpress 网站：

使用现有的 MySQL 数据库。

- sudo docker create -v `pwd`:/var/www/html --name wordpressNameStore php
- sudo docker run -d --name wordpressName --link mysql:mysql --volumes-from=wordpressNameStore -p 800x:80 youdar/wordpress
- sudo docker run -d --name youdar2 --link mysql:mysql -v `pwd`:/var/www/html -p 8002:80 wordpress

/etc/sysctl.conf

```
# Digital Ocean Recommended Settings:
net.core.wmem_max=12582912
net.core.rmem_max=12582912
net.ipv4.tcp_rmem= 10240 87380 12582912
net.ipv4.tcp_wmem= 10240 87380 12582912

fs.file-max=999999
vm.swappiness=20
vm.vfs_cache_pressure = 70
```

cloudcmd

- git clone https://github.com/coderaiser/cloudcmd.git
- cd cloudcmd
- sudo docker build .
- sudo docker create -v `pwd`:/shared/ --name cloudstore busybox
- sudo docker run -d --volumes-from=cloudstore --name cloudcmd -p 420:8000 youdar/cloudcmd
- systemd: In /lib/systemd/cloudcmd.service

```
[Unit]
Description=Redis container
Requires=docker.service
After=docker.service

[Service]
Restart=always
ExecStart=/usr/bin/docker start -a cloudcmd
ExecStop=/usr/bin/docker stop -t 2 cloudcmd

[Install]
WantedBy=local.target
```
- upstart: sudo vi /etc/init/cloudcmd.conf

```
description "Cloudcmd Daemon"
author "youdar"
start on filesystem and started docker
stop on runlevel [!2345]
respawn
script
  /usr/bin/docker start -a cloudcmd
end script
```

- sudo docker stats cloudcmd mysql wordpress phpmyadmin