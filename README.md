# 个人笔记

--------------------

## vim 快捷键 ##

#### 游標移動 ####

	gg = 移到整份文件的最上方
	G = 移到整份文件的最下方
	H = 移到目前螢幕的最上方
	L = 移到目前螢幕的最下方
	10Enter = 游標往下移動10行，前面的數字表示行數
	:10Enter = 游標直接移動到第10行
	{、} = 把游標移動到上一個、下一個段落
	Ctrlwj = 把游標往下面的分割視窗移動
	Ctrlwk = 把游標往上面的分割視窗移動
	Ctrlwh = 把游標往左邊的分割視窗移動
	Ctrlww = 在各個分割視窗間切換

#### NERDTree ####

	B = 叫出bookmark
	C = 把目前游標停留的這個目錄設定為根目錄
	p = 把游標移動到上一層目錄
	P = 把游標移動到根目錄
	J = 把游標移往這個結點的第一個
	K = 把游標移往這個結點的最後一個
	u = 把樹狀結構的根目錄往上移一層
	I = 切換是否顯示隱藏檔案
	m = 叫出NERDTree的系統選單

#### 其他 ####

	:! = 執行外部指令，例如:!ls則是執行ls指令

## docker搭建gitlab ##
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
