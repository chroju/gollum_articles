基礎
----

* スキーマレスなデータ検索エンジン。
* RESTFullにデータの書き込み、検索、削除等の操作ができる。
* データ形式はjsonでのやり取りになる。
* データ構造等はjsonを解釈して定義してくれるが、あらかじめ定義（mapping）も可能。

構造
----

* `index` : RDBのデータベースにあたる。
* `type` : RDBのテーブルにあたる。index内に複数作成できる。
* `document` : 一つ一つのデータ、行。
* `field` : カラム。

`mapping`はデータ型、`type`の構成をjsonで指定したもので、これを`index`を作成するPOSTリクエストに載せることで構造が作成される。

Core Type（データの基本型）は以下5通り。

* String
  * analyzer : 文字列の認識基準、分割点を空白にする、など定める。検索時の基準になる。
    * kuromoji : 日本語解析用。java製の形態素解析器。
    * not_analyzed : 解析をしない。検索は全文一致のみになるが、`/`等による予期せぬ分割認識を防げる。
    * 参考：[Kibana+Elasticsearchで文字列の完全一致と部分一致検索の両方を実現する - Qiita](http://qiita.com/harukasan/items/4ec517d8d96f557367e1)
  * filter : Upper caseへの統一といった文字列処理を定義する
* Number（実際はさらにshort, integer, float等に細分化される）
* Date
* Boolean
* Binary

構成
----

クラスタリング構成が前提になっている。

* `Cluster` : 文字通り負荷分散、耐障害冗長性のためのサーバーグループ。
* `Node` : 各サーバー。
* `Shard` : indexの分解単位。各Shardは別のNodeで動作可能なため、計算能力を分散できる。デフォルトは5 Shards。
* `Replica` : Primary Shardの完全コピー。耐障害。デフォルトで1に設定されているため、1 Nodeしかない構成だとCluster Health: yellowになる。
  [Elasticsearchのshardとreplica - なんかかきたい](http://t-cyrill.hatenablog.jp/entry/2015/02/18/190310)

使用
----

すべてRESTfulに操作する。最も基本的な構造として以下のURL。

```
GET /{index}/{type}
```

* [[Elasticsearch Cheat Sheet]]
* [第７回 Elasticsearch 入門 API の使い方をハンズオンで理解する 〜前編〜 ｜ Developers.IO](http://dev.classmethod.jp/server-side/elasticsearch-getting-started-07/)
* [第８回 Elasticsearch 入門 API の使い方をハンズオンで理解する 〜後編〜 ｜ Developers.IO](http://dev.classmethod.jp/server-side/elasticsearch-getting-started-08/)

```
GET /_cat/health?v # Clusterの状態確認
GET /_cat/indices?v # Index一覧
GET /_cat/indices?v&index=foo # 特定indexの情報表示
GET /_cat/shards?v # Shards状態確認

GET /foo/ # foo indexの情報表示
GET /foo/_mapping # fooのmapping情報を表示
```

設計
----

* [第１回 Elastisearch 入門 インデックスを設計する際に知っておくべき事 ｜ Developers.IO](http://dev.classmethod.jp/server-side/elasticsearch-getting-started-01/)
  * 分散処理を前提とするので、アプリ要件だけではなく処理も考えた設計が必要。
  * RDBと関連して考えがちだが、考慮点はまったく異なる。
* [第２回 Elasticsearch 入門 データスキーマ設計のいろは ｜ Developers.IO](http://dev.classmethod.jp/server-side/elasticsearch-getting-started-02/)
  * Document指向であることによるSQLとの設計思想の違い。
  * ネーミングルール。
  * Nestedの使い方に関して。

関連
----

* [[logstash]]

参考
----

* [Elasticsearchチュートリアル - 不可視点](http://code46.hatenablog.com/entry/2014/01/21/115620)