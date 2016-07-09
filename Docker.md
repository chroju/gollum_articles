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
* yamlでcompose用のファイルを書き、`docker compose`コマンドにより複数コンテナを一律に扱う。

Docker Swarm
----

* 複数のDockerホスト制御。どのホストでどのコンテナを動かすか？という部分を担う。

### 参照

* [今だからこそ知りたい Docker Compose/Swarm 入門](http://www.slideshare.net/zembutsu/introduction-to-docker-compose-and-swarm)

CoreOS
----

* Dockerホスト用として構成されたOSイメージの小さなOS。

### update

* ローリングアップデートなので随時OS更新がかかる。
* デフォルトでは自動で一定間隔でOS更新→再起動を行う。手動で行う場合は以下。

```bash
$ sudo update_engine_client -update
```

### 参照

* [CoreOSを使ってDockerコンテナを動かす——15分でできるCoreOSクラスタの作り方 - さくらのナレッジ](http://knowledge.sakura.ad.jp/tech/3390/)

Alpine Linux
----

* この記事内で言及あり→ [お前のDockerイメージはまだ重い💢💢💢 // Speaker Deck](https://speakerdeck.com/stormcat24/oqian-falsedockerimezihamadazhong-i)
* Dockerイメージの元として本当に最小限のものしか入っていないディストリビューション。
* パッケージ管理は`apk`。
* crontabで実行させたいものは`/etc/periodic`配下へスクリプトを設置する。
  * スクリプトは拡張子を持ってはならない。