ポリシー
----

バケット側でもポリシー設定が出来たりして、とにかく面倒な印象。

[S3のアクセスコントロールが多すぎて訳が解らないので整理してみる ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/s3-acl-wakewakame/)

cli
----

### 同期

```bash
$ aws s3 sync source s3://bucket.name
```

* 同期判定をファイルサイズで行なっている。タイムスタンプでの判定としたい場合は`--exact-timestamps`が必要。
* `--delete`でソースに存在しないファイルはデストで消す。

