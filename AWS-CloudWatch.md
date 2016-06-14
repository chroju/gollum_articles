メトリクス監視。メトリクスは責任共有モデルに基づいてデフォルトで用意されているほか、カスタムメトリクスを作成して任意の値を監視させることもできる。

* [【AWS】カスタムメトリクスを使ったプロセス監視【CloudWatch】 - Qiita](http://qiita.com/koomaru/items/ac274f96fd541ffe4c31)
* [AWS Partner SA ブログ: [OpsJAWS] AWS共有責任モデルに伴った監視の考え方](http://aws.typepad.com/aws_partner_sa/2015/10/opsjaws-aws-monitoring-shared-rep-model-.html)

付帯サービスとしてLogsやEventがある。

* Logs: awslogsやvpc flow logs等、ロギングサービスから連携を受けてログを溜める。
* Events: メトリクスの閾値超過といったイベントをトリガーにアクションをキックする。