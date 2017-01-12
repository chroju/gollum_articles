Docker
========

* [[Dockerコマンドチートシート|DockerCheatSheet]]
* [[Dockerfile]]

Docker Networking
----

* [Dockerコンテナ間のlink，database.ymlの書き方 | SOTA](http://deeeet.com/writing/2014/03/20/docker-link-container/)
  * 基本形。`docker run`の際に`--link image:alias`の形で、
    `image`とlinkし、リンク情報はコンテナ内の環境変数で読み取れるようになる。
  * リンクしたコンテナには、コンテナ内から`http://alias`の形でアクセスできる（/etc/hostsが書き換えられている）。
    [Legacy container links](https://docs.docker.com/engine/userguide/networking/default_network/dockerlinks/#/updating-the-etc-hosts-file)

Docker Compose
----

* 例えばWebとDBで2コンテナ、といった複数コンテナから成るサービスを制御する。
* yamlでcompose用のファイルを書き、`docker-compose`コマンドにより複数コンテナを一律に扱う。

### インストール

* GitHubから最新版をダウンロードしてきて、コマンドに実行権を与えるのみ。
* CoreOSでもデフォルトでは搭載されていない。
  * [CoreOSにdocker-composeを導入 - Qiita](http://qiita.com/hiroseabook/items/50bda4b0fd85ab228c6d)

### コマンド

```bash
# 起動
$ docker-compose up
```

### docker-compose.yml



Docker Swarm
----

* 複数のDockerホスト制御。どのホストでどのコンテナを動かすか？という部分を担う。

### 参照

* [今だからこそ知りたい Docker Compose/Swarm 入門](http://www.slideshare.net/zembutsu/introduction-to-docker-compose-and-swarm)

CoreOS
----

* Dockerホスト用として構成されたOSイメージの小さなOS。
* 詳細は別ページで→ [[CoreOS]]


Alpine Linux
----

* この記事内で言及あり→ [お前のDockerイメージはまだ重い💢💢💢 // Speaker Deck](https://speakerdeck.com/stormcat24/oqian-falsedockerimezihamadazhong-i)
* Dockerイメージの元として本当に最小限のものしか入っていないディストリビューション。
* パッケージ管理は`apk`。
* crontabで実行させたいものは`/etc/periodic`配下へスクリプトを設置する。
  * スクリプトは拡張子を持ってはならない。

こんなときは
----

* [Dockerの時刻 - Qiita](http://qiita.com/HommaHomma/items/c6dbb554afb51f1b95d5)