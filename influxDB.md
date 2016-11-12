* 時系列指向のDB（e.g. RRDtool）。
* JSON形式のデータをREST APIで登録するElasticsearchに似た感覚。
* デフォルトで認証機構を持っている。
* GUIが内蔵しており、ブラウザからクエリをかけて結果を確認できる。またグラフの描画も多少はできるが、Grafanaと接続するのが一般的。
* クエリはSQL文に対応。
* 参照：[InfluxDB の概要 - sonots #tokyoinfluxdb](http://www.slideshare.net/sonots/influxdb-study-20140627)

データ登録
----

* JSONで登録できるが、Elasticsearchのように自由なフォーマットではなく、登録するKeyは定められている。
  * `fields` : いわゆる値が入る箇所。複数のキーバリューを指定できる。
  * `time` : タイムスタンプ。`YYYY-mm-DDTHH:MM:SSZ`の形式。指定しなかった場合は登録したときの時刻がデフォルト値とされる。UTC。
  * `measurement` : ちょっとわからない。
  * `tags` : 付随する情報。`fields`以外で入れたいメモやデータの種別に関する情報と思えば良さそう。文字列型。必須ではない。
  * 参照：[InfluxData | Documentation | Key Concepts](https://docs.influxdata.com/influxdb/v0.9/concepts/key_concepts/#retention-policy)

