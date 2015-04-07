# 个人笔记

--------------------

## 启动gitlab ##
#### 下载镜像 ####
docker pull sameersbn/redis
docker pull postgres
docker pull sameersbn/gitlab
#### 顺序依次启动 ####
**redis**

	docker run --name=redis -d sameersbn/redis:latest
**postgres**

	docker run --name gitlab-postgres -d \
	-p 5433:5432 -e POSTGRES_PASSWORD=123456 postgres
**gitlab**

	docker run --name='gitlab' -d \
	-e 'GITLAB_PORT=10080' -e 'GITLAB_SSH_PORT=10022' \
	-p 10022:22 -p 10080:80 \
	--link gitlab-postgres:gitlab-postgres \
	-e DB_TYPE=postgres -e DB_HOST=gitlab-postgres -e DB_NAME=postgres -e DB_USER=postgres -e DB_PASS=123456 \
	--link redis:redisio \
	-e REDIS_HOST=redisio -e REDIS_PORT=6379 \
	sameersbn/gitlab
