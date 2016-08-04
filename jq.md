オプション
----

* `-C` : カラー出力の強制。パイプに渡してもカラーが維持される。

```bash
# 色付きでlessに流す
$ cat hoge.json | jq '.' -C | less -R
```

参考
----

* [jqで簡単JSON加工 ｜ Developers.IO](http://dev.classmethod.jp/tool/jq/)
* [jqコマンドでjsonデータを整形・絞り込み - Qiita](http://qiita.com/Nakau/items/272bfd00b7a83d162e3a)