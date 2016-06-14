cli
----

### 同期

```bash
$ aws s3 sync source s3://bucket.name
```

* 同期判定をファイルサイズで行なっている。タイムスタンプでの判定としたい場合は`--exact-timestamps`が必要。
* `--delete`でソースに存在しないファイルはデストで消す。

