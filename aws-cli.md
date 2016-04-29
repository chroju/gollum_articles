EC2
----

### インスタンスを新規起動

* [run-instances — AWS CLI 1.10.6 Command Reference](http://docs.aws.amazon.com/cli/latest/reference/ec2/run-instances.html)
* 通常のコマンドだとオプションが非常に多いので、jsonで設定を記述してインプットするのが無難。
  * [EC2インスタンス をcliでLaunch - Qiita](http://qiita.com/web_se/items/704e0d9b57c2bf251a98)
  * 上記ページは若干古い。また予めjsonのテンプレートを出力できる。→ [Generate CLI Skeleton and CLI Input JSON Parameters - AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/generate-cli-skeleton.html)
* `--associate-public-ip-address`を付けないとパブリックIPが付加されなくて死ぬ。

### インスタンス情報表示

* `describe-instances`
* 長いので `--filter` や `--query` をうまく使う。
```bash
$ aws ec2 describe-instances --filter "Name=instance-state-name,Values=running" --query  "Reservations[].Instances[].[InstanceId,Tags]"
```

### インスタンス終了

* `stop-insntaces --instance-id`

### インスタンス破棄

* `terminate-instances --insntance-id`
* インスタンスはデフォルトだと「インスタンス保護の有効化」がTrueになっており、APIからの削除はできないため、あらかじめFalseとしておく必要がある。
  * [インスタンスの終了 - Amazon Elastic Compute Cloud](http://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/terminating-instances.html#Using_ChangingDisableAPITermination)
  * `aws ec2 modify-instance-attribute --instance-id i-xxxxxxxx --attribute disableApiTermination --value true`

Security Groups
----

### 表示

* デフォルトVPCが存在しない状態では、`--group-name`オプションによる指定ができず、`--group-ids`での指定が必要になる模様（参考：[Error Codes - Amazon Elastic Compute Cloud](http://docs.aws.amazon.com/ja_jp/AWSEC2/latest/APIReference/errors-overview.html)）。

```bash
$ aws ec2 dscribe-security-groups --group-ids
```

S3
----

### 同期

```bash
$ aws s3 sync source s3://bucket.name
```

* 同期判定をファイルサイズで行なっている。タイムスタンプでの判定としたい場合は`--exact-timestamps`が必要。
* `--delete`でソースに存在しないファイルはデストで消す。

