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

使用
----

すべてRESTfulに操作する。

* [[Elasticsearch Cheat Sheet]]

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