ps
```bash
# 起動中コンテナの表示
$ docker ps
# 全コンテナの表示
$ docker ps -a
# 最後に作成されたコンテナを表示（起動状態は問わない）
$ docker ps -l
# コンテナIDのみを表示
$ docker ps -q # `docker rm`等の引数として使用
# 特定の名前のコンテナを表示
$ docker ps -f "name=foo" # 部分一致
# イメージから抽出
$ docker ps -f ancestor=centos:7
```

images
```bash
# 全イメージの表示
$ docker images
# 特定イメージの表示
$ docker images foo/bar # 完全一致
# タグのないイメージの表示
$ docker images -f dangling=true
```

build
```bash
$ docker build -p 8080:80 --name hoge -t repository_name/image_name:tag_name Dockerfile
```

run
```bash
$ docker run image_name
# 名前を付ける
$ docker run --name foo image_name
# 対話
$ docker run -it image_name /bin/bash
# ディレクトリのマウント
$ docker run -v /host/dir:/docker/dir image_name
```


exec
```bash
$ docker exec -it container_name /bin/bash
```

stop/start
```bash
# コンテナの停止
$ docker stop id
# コンテナの再開
$ docker start id
```