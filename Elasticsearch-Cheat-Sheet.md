[第３回 Elasticsearch 入門 ドキュメント管理は意外と高度なことができる ｜ Developers.IO](http://dev.classmethod.jp/server-side/elasticsearch-getting-started-03/)

mapping
----

* 参考：[Elasticsearch マッピング — Hello! Elasticsearch. — Medium](https://medium.com/hello-elasticsearch/elasticsearch-9a8743746467#.hbkqbcoeu)
* 一度作成されたmappingに項目の追加は可能だが更新は不可。
  * あれ？できる？→ [Elasticsearchで既にあるインデックスのスキーマを変更する方法 - shnagaiのインフラ備忘録](http://kobitosan.hatenablog.com/entry/2014/12/23/103746)

```
# get mapping
$ curl -XGET "http://host/index/_mapping"
# set mapping
$ curl -XGET "http://host/index" -d '
json...'
```

put data
----

```
# set
$ curl -XPUT "http://host/index/type/1" -d '
json...'
# Delete（mapping含めすべて消えるので注意）
$ curl -XDELETE 'http://host/index/_all'
```

bulk API
----

* [【elasticsearch】idを指定せずに、bulk-insert - Qiita](http://qiita.com/4cteru/items/074d8dc956103c36b7fa)
* indexとdataのjsonを交互に設定する必要があるため、大量のデータを必ずしもそのまま投入できるわけではない。

analyze API
----

* TODO