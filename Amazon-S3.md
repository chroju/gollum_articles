ポリシー
----

* バケット側でもポリシー設定が出来たりして、とにかく面倒な印象。バケットポリシーが優先されるので、IAMはゆるめ（S3全体など）に許可をしておいて、バケットポリシーで絞っていく運用がベターか。
* バケットポリシーの`deny`の優先順位が強い。市販のファイアウォールで実施するポリシーの順位付けは出来ず、デフォルトの優先順位が適用される。いわゆる「All Deny, Some Allow」のような形で設定すると、All Denyが優先されてすべてのアクセスができなくなる。→ [コラム - Amazon Web Servicesを追いかける | 第3回　Amazon S3 で構築した webサイトの機能を強化しよう｜CTC教育サービス 研修/トレーニング](https://www.school.ctc-g.co.jp/columns/strawbag/strawbag03.html)

[S3のアクセスコントロールが多すぎて訳が解らないので整理してみる ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/s3-acl-wakewakame/)

### ポリシー設定時のARNの書き方

`arn:aws:s3:::bucket`の形を取るが、この書き方ではバケットそのものに対する権限になる。バケット内のファイルに対するアクセスを許可、拒否する場合は、`arn:aws:s3:::bucket/*`と、`/`でさらに配下を指定する必要がある。

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