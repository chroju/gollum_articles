メトリクス監視。メトリクスは責任共有モデルに基づいてデフォルトで用意されているほか、カスタムメトリクスを作成して任意の値を監視させることもできる。

* [【AWS】カスタムメトリクスを使ったプロセス監視【CloudWatch】 - Qiita](http://qiita.com/koomaru/items/ac274f96fd541ffe4c31)
* [AWS Partner SA ブログ: [OpsJAWS] AWS共有責任モデルに伴った監視の考え方](http://aws.typepad.com/aws_partner_sa/2015/10/opsjaws-aws-monitoring-shared-rep-model-.html)

付帯サービスとしてLogsやEventがある。

* Logs: awslogsやvpc flow logs等、ロギングサービスから連携を受けてログを溜める。
* Events: メトリクスの閾値超過といったイベントをトリガーにアクションをキックする。

cli
----

存在するメトリクスをリストアップ

```bash
$ aws cloudwatch list-metrics --namespace AWS/EC2 --dimensions "Name=InstanceId,Value=i-xxxxxxxx" --metric-name CPUCreditUsage
{
    "Metrics": [
        {
            "Namespace": "AWS/EC2",
            "Dimensions": [
                {
                    "Name": "InstanceId",
                    "Value": "i-0df49b92"
                }
            ],
            "MetricName": "CPUCreditUsage"
        }
    ]
}
```

あるメトリクスの値を取得

```bash
$ aws cloudwatch get-metric-statistics --namespace AWS/EC2 --dimensions "Name=InstanceId,Value=i-xxxxxxxx" --metric-name CPUCreditUsage --start-time `date -u -d "5 mins ago" '+%FT%TZ'` --end-time `date -u '+%FT%TZ'` --period 300 --statistics Average
{
    "Datapoints": [
        {
            "Timestamp": "2016-06-14T09:52:00Z",
            "Average": 0.0,
            "Unit": "Count"
        }
    ],
    "Label": "CPUCreditUsage"
}
```

参考
----

* [[JAWS-UG CLI] CloudWatch:#1 メトリックを見る (SNS) - Qiita](http://qiita.com/tcsh/items/e2184f8c7c283e93b167)