# PHP开发容器

### 构建使用

> 修改所有的`/home/zane/data`为自己的工作目录

```
# 构建镜像
docker-compose build

# 创建容器并运行
docker-compose up -d

# 启动容器
docker-compose start

# 进入容器
docker container exec -it php-74-dev bash

# 关闭容器
docker-compose stop

# 删除容器
docker container rm php-74-dev
```

### 切换构建与版本

> 注释修改`docker-composer.yml`

| block      | description |
| ---------- | ---------- |
| build | 构建 |
| image | 运行 |
| php-fpm-72 | php v7.2 |
| php-fpm-74 | php v7.4 |



### 导入导出

```
docker save -o php74.tar php_php-fpm-74:latest
docker load < php74.tar
```