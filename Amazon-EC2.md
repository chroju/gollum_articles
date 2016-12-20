EC2のサービス範囲
----

マネジメントコンソール上野分類では、以下が含まれる。

* Elastic Block Store (EBS)
* Elastic Load Balancing (ELB)
* Auto Scaling

### ELB (Elastic Load Balancing)

* 仮想ロードバランサー。
* 自動スケールして負荷上昇に対応するが、急速なスパイクが予想される場合にはサポートからPre-Warming（暖気申請）を行える。
  * [Elastic Load Balancing の暖気申請について ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/elastic-load-balancing-pre-warming/)
* スケール状況はインスタンス数やENI（ネットワークインターフェース）数で確認が可能。

```
・ ELB名・リージョン、またはFQDN
・ 予測されるピーク時のリクエスト数 (requests/秒)
・ 予想されるピーク時の1リクエストあたりの平均リクエストサイズ+レスポンスサイズ(bytes), または想定スループット(bit/秒)
(計算例： 1ページが20KBのHTML、30KBのCSS、10枚の15KBの画像で構成されるケースを考えます。まずリクエスト側については、このケースでの平均的なHTTPリクエスト文字列長を1KBであると仮定します。またレスポンス側については、1リクエストあたりの平均レスポンスサイズがおよそ16.66KB(=200KB/12リクエスト)であると計算できます。これらより、1リクエストあたりの平均リクエストサイズ+レスポンスサイズを、16.7 + 1 = 17.7[KB/req]と推定できます。)
・ Pre-warmingが必要となる期間(開始時刻および終了時刻)
・ HTTPSの利用有無、利用する場合にはHTTPとHTTPSの割合
・ 利用するAZ(アベイラビリティゾーン)の数
　→現在ご利用中のAZの数から変更予定があればお知らせください。
・ バックエンドインスタンスでのKeep-aliveの設定可否
　→ELBはバックエンドWebサーバのKeep-Alive有効化によってパフォーマンスが向上しますので、有効化することをおすすめいたします。
・ イベント日までにバックエンドEC2インスタンス数を増やしますか。(増やす場合はいつ、どのくらい増やしますか)
・ トラフィックパターンをお知らせください。
(トラフィックの傾向とともに予想される最大・最少アクセスの時間。 例： 朝8時頃にアクセス数のピーク 3000req/secとなり、徐々にリクエストが減り、23時以降はピーク時の4分の1ほどになる。)
・ユースケースをお知らせください。
(例： 新商品のプロモーション、テレビ連携のイベントで短期間に集中的なアクセスが見込まれるため。)
```

仮想化方式
----

[仮想化方式(HVM と PV)についてまとめ - 水深1024m](http://kanny.hateblo.jp/entry/2014/01/19/182759)

* 2種類ある、というよりは途中でHVM（完全仮想化）へ移行したらしい。
* 現在はPVはおそらく選択できない。
  古いAMIでPVのものがあるが、作成する場合は最近の（x2系）インスタンスタイプは使用できない。

設定
----

### インスタンスメタデータ

インスタンス内部から http://169.254.169.254/latest/meta-data/ にアクセスすることで、インスタンスの情報を取得することができる。

* [インスタンスメタデータとユーザーデータ - Amazon Elastic Compute Cloud](http://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)

### 設定変更

[EC2起動後に、後からできること・できないこと - 続 カッコの付け方](http://iga-ninja.hatenablog.com/entry/2014/10/30/000000)

cli
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

### Security Groups

#### 表示

* デフォルトVPCが存在しない状態では、`--group-name`オプションによる指定ができず、`--group-ids`での指定が必要になる模様（参考：[Error Codes - Amazon Elastic Compute Cloud](http://docs.aws.amazon.com/ja_jp/AWSEC2/latest/APIReference/errors-overview.html)）。

```bash
$ aws ec2 dscribe-security-groups --group-ids
```
