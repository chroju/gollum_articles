全データをMySQLコマンドの形でダンプしたもの。最もシンプルなバックアップ手法。`mysql`コマンドを使って読み込むことでリストアが可能。

```bash
$ mysql -hlocalhsot -uroot -p dbname < mysqldump
# 文字化けしたり、認識できない文字があるとエラーになる際は、文字コード指定を付与する。
$ mysql -hlocalhsot -uroot -p --default-character-set=utf8 dbname < mysqldump
# パイプで流し込めればいいので、遠隔に置いてあるものから転送も可能。
$ ssh remotehost "cat /tmp/mysqldump | gzip" | zcat | mysql -uroot -ppassword
```

### 参照

* [MySQL :: MySQL 5.6 リファレンスマニュアル :: 2.11.5 MySQL データベースのほかのマシンへのコピー](https://dev.mysql.com/doc/refman/5.6/ja/copying-databases.html)

tips
----

### 分割実行

* ダンプファイルは容量が大きくなりがちなので、分割して実行した方が効率性が高い場合がある。必要に応じてsplitやsedで分割を検討する。
* 構造は変数定義→`CREATE DATABASE`→`USE hoge`→`CREATE TABLE`×複数→`USE hoge`となっているので、必要な部分を`sed`で探って切る。
  * `split`で適当に切るとSQLコマンドが分断されて実行できなかったりするので注意。
* 冒頭の変数定義が後々使われている場合がある。エラーが出るようなら変数定義だけ分割したダンプファイルへ付け足してみる。
* [MySQLのダンプファイルから任意のテーブルのみリストアする - Qiita](http://qiita.com/toshiro3/items/7844d45076b83103c095)

### Can't create table

* mysqldumpは文字コード順でDBとテーブルを出力しているため、外部参照キーの依存関係は考慮されていない。依存関係の問題でテーブルが作れない場合がある。
* 先頭行に`SET FOREIGN_KEY_CHECKS=0;`を追加することで、一時的に外部参照制約のチェックを外せる。最後に`1`へ戻すのも忘れずに。
