参照
----

* [RDS(mysql) general_log をLambdaを用いてS3に保存する方法 - Qiita](http://qiita.com/rev4t/items/cc539bb6083a7d9bda8e)
* [RDS for MySQLのスロークエリーログをAWS LambdaでElasticsearchに取り込む ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/rds-mysql-slowquerylog-to-es/)

特徴
----

### メンテナンスウインドウ

* あらかじめ設定しておくと、その時間帯でパッチ適用を自動実行する。
* Multi-AZ構成の場合はローリングアップデートになり、サービス停止は短くなる。
* 参考：[Amazon RDS のメンテナンスにどう立ち向かうべきか](https://blog.manabusakai.com/2016/01/rds-maintenance/)

### EndPointでの接続

* 後述のフェイルオーバー等もあり、IPが固定されないため、RDSへの接続はEndPointに対して実行する。

### リードレプリカ

* 読み取り専用のレプリカ。マスターインスタンスから同期される。read処理の性能向上に寄与する。

### Multi-AZ

* 複数のAvailability Zoneにインスタンスを配置し、障害時には数分で自動フェイルオーバーさせられる。障害は以下。
  * プライマリインスタンスの利用可能ゾーンの可用性損失
  * プライマリに対するネットワーク接続の喪失
  * プライマリ上でのコンピュートユニット障害
  * プライマリへのストレージ不良
* データのコピーは物理レプリケーションで行われる。

監視
----

### イベント通知

RDS上での種々のイベント発生はSNS経由で通知される。通知されるイベントの一例は以下。

* DBインスタンスのシャットダウン
* マスターパスワードのリセット
* フェイルオーバーの開始／完了
* すべてのイベントは→ [Amazon RDS イベント通知の使用 - Amazon Relational Database Service](http://docs.aws.amazon.com/ja_jp/AmazonRDS/latest/UserGuide/USER_Events.html)
* 監視についてのアドバイス→ [AWS Partner SA ブログ: [OpsJAWS] RDSイベントの監視](http://aws.typepad.com/aws_partner_sa/2015/05/aws-ops-monitoring-rdsevents-1.html)

APIの`describe-events`で能動的に取得も可能。最大で過去14日分。

### CloudWatch 標準メトリクス

主に以下の通り。

* OSの観点
  * CPU使用率
  * RAM、ディスクの空き容量
  * swapの容量
* DBの観点
  * コネクション数
  * ディスクI/O回数、時間、バイト数
  * バイナリログの容量
  * リードレプリカとのラグ

全容：[DB インスタンスのメトリックスの表示 - Amazon Relational Database Service](http://docs.aws.amazon.com/ja_jp/AmazonRDS/latest/UserGuide/USER_Monitoring.html)

### 拡張モニタリング

* [[新機能]Amazon RDSでOSの詳細情報を取得できるようになりました！ ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/rds-enhanced-monitoring/)
* 2015年12月頃に追加された、CloudWatch Logsにより詳細な情報を出力する機能。
* ローンチ時点の対応はMySQL5.6、Maria、Auroraのみ。
* 取得できるのはCPU使用率、ディスクI/O、プロセスリストといったOSレイヤーのメトリクス。RDSではOSレイヤーのメトリクスをユーザー側で取得できないため提供しているものと思われる。

### ログ

各DBツールごとに、定められたログをモニタリングできる。MySQLの場合はエラーログ、general log、スロークエリログ。APIから`describe-db-log-files`でアクセスできる。

### メンテナンスイベント

* AWSによるRDSインスタンスのメンテナンスは`describe-pending-maintenance-actions`で確認できる。
  * [AWS Partner SA ブログ: [OpsJAWS] RDSイベントの監視](http://aws.typepad.com/aws_partner_sa/2015/05/aws-ops-monitoring-rdsevents-1.html)
* `Required`と`Available`の2種類があり、前者は事前実施をしなければメンテナンスウインドウの時間帯に強制実行される。後者は見送り（無期限延期）が可能。