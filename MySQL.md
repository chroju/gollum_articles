MySQL
========

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
* [誰も教えてくれなかったMySQLの障害解析方法 - Qiita](http://qiita.com/muran001/items/14f19959d4723ffc29cc)