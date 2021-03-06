MySQLレプリケーションが何らかの理由で停止し、その後再開する際、停止時間が長いとバイナリログのローテートが進み、中断時点から再開できない場合がある。具体的なエラーとしては`Could not find first log file name in binary log index file`が出力される。

特に間が空いてスキップしてしまっても問題ないということであれば、以下記事のように現状存在するバイナリログの適当な箇所からレプリケーションを再開すればいい。

[ケーワン・エンタープライズのエンジニアメモ(｀･ω･´)ゞﾋﾞｼｯ!!: CHANGE MASTER TO](http://k-1-ne-jp.blogspot.jp/2012/12/change-master-to-master.html)

しかしスキップさせたくない＝マスターとスレーブの同期性を保ちたい場合には、おそらく一旦ごっそりマスターのデータをスレーブへ移行し、その上でレプリケーションを再開させるしかないと思われる。

そもそもにしてバイナリログが不意にパージされてしまう状態がよろしくないので、レプリケーション状態を監視して、終了していないようであればパージせずログを保っておくような設定が必要なのかもしれない。具体的な実装は特に見つからないのだが、スクリプトで定期的に古い（時間的に）ログを監視し、relay_master_log_fileの値と鑑みて削除可否判断を行わせるのがベターなように思う。時間、もしくは容量だけをトリガーとした自動的なパージだと、レプリケーションにお構い無くバイナリログが消えていく。

[MySQL Replication: 'Got fatal error 1236' causes and cures](https://www.percona.com/blog/2014/10/08/mysql-replication-got-fatal-error-1236-causes-and-cures/)
