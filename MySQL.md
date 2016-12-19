MySQL
========

記事
----

* [[Could not find first log file name]]
* [[REP再開時のmax_allowed_packetの調整|Mysql_eplication_and_max_allowed_packet]]
* [[monitoring mysql]]

特徴
----

* ストレージエンジンがプラグイン化しており、選択肢がある（ほぼInnoDBが使われている）。
* PostgreSQLのようなバキューム処理は不要。
* 

設定の勘所
----

* Replcationの実装
* キャッシュクエリのヒット率確保
* コネクション数の確認

バージョン毎の変更点
----

* [漢(オトコ)のコンピュータ道: MySQL 5.5新機能徹底解説](http://nippondanji.blogspot.jp/2010/12/mysql-55.html)
  * 準同期レプリケーションが出来るようになったあたり。
  * utf8mb4（4バイト対応UTF8）もこのバージョンから。
  * その他細々とした変更点が多い。
* [MySQL 5.7の罠があなたを狙っている](http://www.slideshare.net/yoku0825/mysql-57-51945745)
  * ぶっちゃけよくわからないんですが罠が多いらしいです。

コマンド操作
----

### 接続

```bash
$ mysql -h hostname -P port -u user -p [password]
# sqlコマンドを引数で与えて実行
$ mysql -e 'SQL COMMAND'
# 表枠を表示しない / この際自動で特殊文字はエスケープされるが、-rでエスケープ解除できる
$ mysql -s -r
# カラム名を表示しない
$ mysql -N
```

### 一覧表示

```
show databases;
use hoge;
show tables;
```

### MySQLコマンド

```
# 表示を見やすくする
> pager less -n -i -S;
# 設定値の確認
> show global variables LIKE 'performance_schema%';
# ステータス確認
> show global status LIKE 'thread_connected';
# レプリケーションステータスの確認
> show slave status\g
# レプリケーションステータスの変更
> change master to MASTER_LOG_FILE='mysqld-bin.000001';
```

### ユーザー

* ユーザーは接続元の情報を`root@localhost`のような形で持つ。localhostで全権を持っているユーザーでも、遠隔から接続した際は一切の権限がない、といったことが起こり得る。
* [MySQL の権限のコマンドまとめ。 - Qiita](http://qiita.com/PallCreaker/items/0b02c5f42be5d1a14adb)

```
# 全ユーザーを確認
> SELECT user,host,password FROM mysql.user;
# 管理者用ユーザー作成
# 最後のGRANTオプションを省けば権限管理は除外できる
> GRANT ALL ON *.* TO adminuser@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
```

### コメント

* `# `と`-- `と`/* */`がある。
* `/*!50001 */`形式で記載すると、MySQL5.00.01以降でのみ実行されるコマンドになる。mysqldumpで多用されている。

global variables
----

* `max_connections` : 最大接続数

status
----

* `thread_connected` : 現在接続中のスレッド数

log
----

`/var/mysql/data/`あたりを探る。

dual
----

[the Snow Color: MySQLのDUAL表](http://thesnowcolor.blogspot.jp/2013/01/mysqldual.html)

Replication
----

MySQLの醍醐味？ 基本的なフローは以下。

1. マスターサーバーがクエリをバイナリログに記録。
2. スレーブサーバーがマスターサーバーへ接続に行き、マスターからバイナリログを送信。
3. スレーブが受け取ったバイナリログをリレーログとして保存。
4. リレーログからクエリを読み取って実行。

状態の確認は`show slave status\G`が鉄板。

* [漢(オトコ)のコンピュータ道: MySQLにおけるレプリケーション遅延の傾向と対策](http://nippondanji.blogspot.jp/2011/12/mysql.html)

### 参考

* [MySQLリレーログの仕様を学ぶ | OpenGroove](http://open-groove.net/mysql/binlog-relay-log/)
* [MySQLのレプリケーションでLast_SQL_Errno: 1594が出た場合の対処方法 | Mindcircus.jp](http://www.mindcircus.jp/archives/5758)

my.cnf
----

設定ファイル。

* [[my.cnf]]

mysqldump
----

全データをMySQLコマンドの形でダンプしたもの。最もシンプルなバックアップ手法。`mysql`コマンドを使って読み込むことでリストアが可能。

* link : [[mysqldump]]
* [mysql の定期的なバックアップ - Qiita](http://qiita.com/crimson_21/items/6171a95f8ddb2861e2e6?utm_content=buffer59d96&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer)（シェルスクリプトでの実装）

Trouble
----

* [誰も教えてくれなかったMySQLの障害解析方法 - Qiita](http://qiita.com/muran001/items/14f19959d4723ffc29cc)
* [漢(オトコ)のコンピュータ道: もしもデータベースサーバがクラッシュしたら](http://nippondanji.blogspot.jp/2009/02/blog-post_23.html)
* [MySQLで処理に長時間かかっている複数クエリをまとめて殺す方法](http://tech.basicinc.jp/MySQL/2014/04/06/mysql_processlist_kill/)
