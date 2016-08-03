全データをMySQLコマンドの形でダンプしたもの。最もシンプルなバックアップ手法。`mysql`コマンドを使って読み込むことでリストアが可能。

```bash
$ mysql -hlocalhsot -uroot -p dbname < mysqldump
# 文字化けしたり、認識できない文字があるとエラーになる際は、文字コード指定を付与する。
$ mysql -hlocalhsot -uroot -p --default-character-set=utf8 dbname < mysqldump
# パイプで流し込めればいいので、遠隔に置いてあるものから転送も可能。
$ ssh remotehost "cat /tmp/mysqldump | gzip" | zcat | mysql -uroot -ppassword
```

* [MySQL :: MySQL 5.6 リファレンスマニュアル :: 2.11.5 MySQL データベースのほかのマシンへのコピー](https://dev.mysql.com/doc/refman/5.6/ja/copying-databases.html)