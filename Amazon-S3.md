ポリシー
----

バケット側でもポリシー設定が出来たりして、とにかく面倒な印象。バケットポリシーが優先されるので、IAMはゆるめ（S3全体など）に許可をしておいて、バケットポリシーで絞っていく運用がベターか。

[S3のアクセスコントロールが多すぎて訳が解らないので整理してみる ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/s3-acl-wakewakame/)

cli
----

### 基本操作

```bash
# バケット一覧
$ aws s3 ls
# 再帰的にアップロード
$ aws s3 cp hoge s3://my-bucket-name/hoge/ --recursive
# include, exclude
$ aws s3 cp hoge s3://my-bucket-name/hoge/ --recursive --exclude "*" --include "*.png"
# ダウンロード
$ aws s3 cp s3://my-bucket-name/hoge/fuga.txt ./
# 移動
$ aws s3 mv s3://my-bucket-name/hoge/fuga.txt ./
# 削除
$ aws s3 rm s3://my-bucket-name/hoge/ --recursive
```

### 同期

```bash
$ aws s3 sync source s3://bucket.name
```

* 同期判定をファイルサイズで行なっている。タイムスタンプでの判定としたい場合は`--exact-timestamps`が必要。
* `--delete`でソースに存在しないファイルはデストで消す。

### バケット操作

```bash
# 作成
$ aws s3 mb s3://hoge
# 削除（空のバケットじゃない場合は、--forceを付けなければ削除できない）
$ aws s3 rb s3://hoge
```