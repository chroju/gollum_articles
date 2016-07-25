update
----

* ローリングアップデートなので随時OS更新がかかり、自動でOSが再起動される。
* コンテナも当然一度落ちるので、自動起動のスケジューリングにはfleetやsystemdを用いる。
* デフォルトでは自動で一定間隔でOS更新→再起動を行う。手動で行う場合は以下。

```bash
$ sudo update_engine_client -update
```

cloud-config
----

* OS設定を記述するymlファイル。直接的なコマンド発行ではなく、基本はこのファイルで設定を行う。
* パスは`/usr/share/oem/cloud-config.yml`。
* ファイルは起動後に自動で読み込まれる。手動で読む場合は`sudo coreos-cloudinit --from-file`を使う。

fleet, etcd
----

* コンテナ管理、スケジューリングを行うのがfleet。
* CoreOSのクラスタリングを賄うのがetcd。この両者がCoreOSの特徴。相互に働き合って動作する。

参照
----

* [CoreOSを使ってDockerコンテナを動かす——15分でできるCoreOSクラスタの作り方 - さくらのナレッジ](http://knowledge.sakura.ad.jp/tech/3390/)
