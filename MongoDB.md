* スキーマレスでjsonライクなデータストア

Structure
----

* データベース＞コレクション（テーブル）＞ドキュメント（行）＞フィールド（カラム）

Commands
----

* `mongo` でDBコンソールに入る

### コンソールコマンド

#### DB

* `show dbs;` DB一覧の表示
* `use dbname` DBをスイッチ
* `db.stats()` DBの詳細表示

#### Collections

* `show collections:` 選択中のDB内のコレクションを一覧表示
* `db.collecction_name.find(query, field)` コレクション内のドキュメント取得
  * queryは`{age:{$lt:100}}`や`{name:'hoge'}`といった形で指定
  * fieldは`{name:1}`とすると`name`と`id`だけが表示される（`id`不要であれば`_id:0`とする）
* `db.createCollection('collection_name');` コレクションの追加
* `db.collection_name.drop();` コレクションの削除

### 参考

* [MongoDBコマンド一覧（自分用メモ） - Qiita](http://qiita.com/k-staging/items/a386d272abb2c9b92f1a)
* [MongoDB超入門 - Qiita](http://qiita.com/saba1024/items/f2ad56f2a3ba7aaf8521)