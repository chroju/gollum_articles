* [[aws-cli]]
* [[AWS Billing]]
* [[Amazon EC2]]
* [[Amazon ECS]]
* [[Amazon S3]]
* [[Amazon SNS]]
* [[AWS Lambda]]

References
----

* http://status.aws.amazon.com/ 各サービスのステータス一覧。RSS配信あり。

Other Services
----

### Amazon ElasticBeanstalk

PaaS。アプリを選択するとそれに必要なEC2等を勝手に構築してくれる。デプロイはzipファイルをアップロードするだけでOK。開発、ステージング、本番といった環境の棲み分けもできる。heroku的だが、構築したリソース分の課金が発生するため注意は必要。

### AWS CodeDeploy

S3やGitHub上のアプリケーションコードを決められた箇所へ配置する（デプロイ）作業を制御するサービス。

[AWS再入門 AWS CodeDeploy 編 ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/cm-advent-calendar-2015-aws-re-entering-codedeploy/)

### AWS CodePipeline

CDツール。CodeDeployやElastiBeanstalkと連携して、コードのコミットをトリガーに自動でデプロイを行う。

[AWS CodePipeline触ってみた « サーバーワークス エンジニアブログ](http://blog.serverworks.co.jp/tech/2015/07/15/aws-codepipeline/)

### AWS CloudFormation

AWSの構成をjsonでインポートして自動構築。AWS as a code。

### Amazon Inspector

EC2にエージェントを入れるとCVEの該当有無チェックやランタイム解析を自動で行なってくれる。

[AWS Inspectorで脆弱性を検知させる ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/inspector-finding-security-issue/)

### Amazon CloudFront

CDN。

[AWS再入門 Amazon CloudFront編 ｜ Developers.IO](http://dev.classmethod.jp/cloud/cm-advent-calendar-2015-aws-re-entering-cloudfront/)

### AWS Key Management Service

暗号化キーを簡単に作成、管理し、AWS各リソースの暗号化を行う。

### AWS Direct Connect

[AWS Black Belt Techシリーズ AWS Direct Connect](http://www.slideshare.net/AmazonWebServicesJapan/aws-black-belt-tech-aws-direct-connect)

### AWS CloudWatch

メトリクス監視。メトリクスは責任共有モデルに基づいてデフォルトで用意されているほか、カスタムメトリクスを作成して任意の値を監視させることもできる。

* [【AWS】カスタムメトリクスを使ったプロセス監視【CloudWatch】 - Qiita](http://qiita.com/koomaru/items/ac274f96fd541ffe4c31)
* [AWS Partner SA ブログ: [OpsJAWS] AWS共有責任モデルに伴った監視の考え方](http://aws.typepad.com/aws_partner_sa/2015/10/opsjaws-aws-monitoring-shared-rep-model-.html)

付帯サービスとしてLogsやEventがある。

* Logs: awslogsやvpc flow logs等、ロギングサービスから連携を受けてログを溜める。
* Events: メトリクスの閾値超過といったイベントをトリガーにアクションをキックする。

### AWS Config

構成変更のロギング。有効化することで使用可能になる。無償だが保存先S3バケット料がかかる。Config Rulesで構成変更の自動チェックができる。

### AWS CloudTrail

APIコールのロギング。

### Amazon SQS

キューサービス。SNS等から連携されたキューメッセージをストック。エンドポイント（URL等）へのアクセスに応じてsendする。