MySQL Replication再開時のmax_allowed_packetの調整
========

MySQLでレプリケーションがエラーとなり、エラー時点から再開した際、`mysqld.log`に以下のエラーが出ることがある。

```
Packets larger than max_allowed_packet are not allowed.
```

平常時ではレプリケーション元バイナリログの最新箇所のみを追いかけているため、`max_allowed_packet`に引っかかることはない。しかしエラー時点から再開した場合、すでにローテート済みのバイナリログファイルを読み取ろうとするため、ファイルサイズが`max_allowed_packet`を超えていれば上記のアラートが発生する。

対処としては一時的に`my.cnf`を書き換えて`max_allowed_packet`を増やす必要がある。

```bash
$ vi /etc/my.cnf
# max_allowed_packetを書き換え
$ systemctl restart mysql
$ mysql -hlocalhost -uroot -p
mysql> reset slave;
mysql> show slave status\G
```

参考
----

[MySQL に大きなデータを送る際に max_allowed_packet を確認した方がいい | Sun Limited Mt.](http://blog.syuhari.jp/archives/1307)