MySQL
========

* [[REP再開時のmax_allowed_packetの調整|Mysql_eplication_and_max_allowed_packet]]

設計
----

* Replcationの実装
* キャッシュクエリのヒット率確保
* コネクション数の確認

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
[MySQL の権限のコマンドまとめ。 - Qiita](http://qiita.com/PallCreaker/items/0b02c5f42be5d1a14adb)

```
# 全ユーザーを確認
> SELECT user,host,password FROM mysql.user;
# 管理者用ユーザー作成
# 最後のGRANTオプションを省けば権限管理は除外できる
> GRANT ALL ON *.* TO adminuser@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
```

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

mysqldump
----

全データをMySQLコマンドの形でダンプしたもの。最もシンプルなバックアップ手法。`mysql`コマンドを使って読み込むことでリストアが可能。

```bash
$ mysql -hlocalhsot -uroot -p dbname < mysqldump
# 文字化けしたり、認識できない文字があるとエラーになる際は、文字コード指定を付与する。
$ mysql -hlocalhsot -uroot -p --default-character-set=utf8 dbname < mysqldump
```

* [MySQL :: MySQL 5.6 リファレンスマニュアル :: 2.11.5 MySQL データベースのほかのマシンへのコピー](https://dev.mysql.com/doc/refman/5.6/ja/copying-databases.html)

Trouble
----

* [誰も教えてくれなかったMySQLの障害解析方法 - Qiita](http://qiita.com/muran001/items/14f19959d4723ffc29cc)
* [漢(オトコ)のコンピュータ道: もしもデータベースサーバがクラッシュしたら](http://nippondanji.blogspot.jp/2009/02/blog-post_23.html)
* [MySQLで処理に長時間かかっている複数クエリをまとめて殺す方法](http://tech.basicinc.jp/MySQL/2014/04/06/mysql_processlist_kill/)
