# 100行合ったmod_rewirteっをngx_mrubyで書き換えた話
@buty4649
mod_rewriteがかなり複雑になっていてルーティング追加時のデバッグが困難だった
nginxとapache2とapache1が役割違うけど同居、apache2がc10kでボトルネックに
nginxに等号しようとしたけどifのネストができないしconfigが長くなる。。。
ngx_mruby nginx.conf内でmrubyによる拡張が出来る
Middleware as code テストが出来る

# Nyah
ペパボのプライベートクラウド OpenStack
4象限のペパボの技術的なロードマップええなあ
86%のサービスで使っている 558インスタンス（うおー）
開発メンバーがインスタンス起動やプロビジョニングをポチポチ行える
Mackerelでモニタリング
コストダウン（イニシャル、ランニングとも）にもつながっている
=>移行前後で測っておいて比較したい
アラート等の障害も減った
but バージョンアップが半年ごとにあるので追随大変（できてない）
機能を有効に使い切れていない部分がある。
nyah-cli
DVR
バージョンアップテストは？ Terraformが通ればOKでは

# 高集積ホスティングによる略
ロリポ
高集積にこだわる
リソース制御の自動化
mod_mruby mod_cgroup

# インフラCI
alotofwe
アプリのCI => drone.io（コンテナ利用のCI
puppet serverspec
docker-in-docker

# linuxユーザー管理
pyama
ldap? /etc/passwdの構成管理ツールによる配布？ rpm? deb?
ldap中身が複雑に成る 連携の複雑化
アプリケーションデプロイもsshでやるからユーザーが増えていく
stns simple toml name service Golangだ
名前解決、更改鍵取得、sudo認証だけやる
deploy用ユーザーの運用「deploy」
公開鍵を並べる運用、面倒では
=> link_usersで解決できる
組織構造の表現も出来る => link_groups
GH:Eからデータ取ってtomlのユーザー情報つくる
GitHub Flowでユーザー管理
APIでいろんなDBとかから直接ユーザー取ってくるようにしたい
passwdバックエンドを用意したい

# ベンチマーク
fio

# 構成管理ツールを用いたインフラ開発フローの改善
構成管理してたつもりだけどサーバーがおかしい挙動する？
変更のコード化を忘れる、PRのマージ忘れる
CIだと一からイメージ立てるけど本番は差異の反映だから差異あるやん
=> puppet, serverspec最新版と本番の差分可視化
https://github.com/hanazuki/puppet-theatre

# talk
,,


