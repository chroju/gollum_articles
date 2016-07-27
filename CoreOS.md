* Docker/etcd/fleetにより、マイクロサービスアーキテクチャに最適化されたディストリビューション。
* ローリングアップデートなので随時OS更新がかかり、自動でOSが再起動される。
* コンテナも当然一度落ちるので、自動起動のスケジューリングにはfleetやsystemdを用いる。参照：[技術系: CoreOSでdockerコンテナを自動起動](http://automation-wb.blogspot.jp/2016/04/coreosdocker.html)
* デフォルトでは自動で一定間隔でOS更新→再起動を行う。手動で行う場合は以下。

```bash
$ sudo update_engine_client -update
```

cloud-config.yml
----

* OS設定を記述するymlファイル。直接的なコマンド発行ではなく、基本はこのファイルで設定を行う（他で編集しても再起動時にリセットされる）。
* パスは`/usr/share/oem/cloud-config.yml`。
* ファイルは起動後に自動で読み込まれる。手動で読む場合は`sudo coreos-cloudinit --from-file`を使う。

etcd
----

* CoreOSのクラスタリングを賄うのがetcd。
* Discoveryと呼ばれるURLへのアクセスを元に、動的にクラスタを構成できる。

### 参考

[［入門編］etcdでクラスタを構築する - Qiita](http://qiita.com/coreos/items/2e4ca397031d368832c4)

fleet
----

* コンテナ管理、スケジューリングを行うのがfleet。

参照
----

* [CoreOSを使ってDockerコンテナを動かす——15分でできるCoreOSクラスタの作り方 - さくらのナレッジ](http://knowledge.sakura.ad.jp/tech/3390/)
