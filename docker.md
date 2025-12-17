#Mysql

准备本机目录

```
mkdir -p ~/docker/mysql/data
mkdir -p ~/docker/mysql/conf
```

设置配置文件

```
vim ~/docker/mysql/conf/my.cnf
```

```
[mysqld]
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
default-time-zone = '+09:00'

max_connections = 300

[client]
default-character-set = utf8mb4
```
创建docker-compose.yml：

```
services:
  mysql:
    image: mysql:8.4
    container_name: mysql8
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: "YourStrongPassw0rd!"
      TZ: "Asia/Tokyo"
    volumes:
      - ./data:/var/lib/mysql
      - ./conf:/etc/mysql/conf.d
    restart: unless-stopped

```

目录结构

```
docker/mysql/
├── docker-compose.yml
├── data/
└── conf/
    └── my.cnf
```



| 目的     | 命令                             |
| ------ | ------------------------------ |
| 构建（后台运行）    | `docker compose up -d`          |
| 停并删容器  | `docker compose down`          |
| 删容器+数据 | `docker compose down -v`       |
| 临时停    | `docker compose stop`          |
| 再启动    | `docker compose start`         |
| 重建     | `docker compose up -d --build` |
| 查看状态     | `docker compose ps` |

















