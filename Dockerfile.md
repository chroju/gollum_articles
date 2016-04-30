基本的な書き方

```docker
# 元となるイメージの指定。タグまで指定可能。
FROM alpine:3.3
# 制作者名
MAINTAINER chroju 

# 環境変数の設定
ENV PATH $PATH:/root/bin
# ローカルファイルfoo（Dockerfileからの相対パス）をコンテナの/tmp/fooに設置
ADD foo /tmp/foo
# マウントポイントの作成
VOLUME ["/data"]

# RUNを実行するユーザーを指定
USER root
# RUNを実行するディレクトリの指定
WORKDIR /root
# 一つひとつのイメージ作成用コマンドを指定。
RUN apk add git
# 複数コマンド組み合わせてしまうことも可能。
RUN apk add ruby && \
    gem install bundler --no-rdoc --no-ri

# コンテナ作成時に実行されるコマンドを指定（例えばサービスの開始など）。
CMD ["echo", "test"]

# 開くポートを指定。
EXPOSE 80
```