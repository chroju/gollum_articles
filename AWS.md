References
----

[【備忘録】AWSの最新情報が公開される場所をまとめてみた ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/latest-information-about-aws/)

### Info

* [Release Notes : Amazon Web Services](http://aws.amazon.com/releasenotes)
* http://status.aws.amazon.com/ 各サービスのステータス一覧。RSS配信あり。

### Whitepaper

* [AWS運用チェックリスト (PDF)](https://d0.awsstatic.com/whitepapers/aws-operational-checklists.pdf)
* [AWS アーキテクチャーセンター | AWS](http://aws.amazon.com/jp/architecture/)
* [ホワイトペーパー | AWS](https://aws.amazon.com/jp/whitepapers/)
* [セキュリティリソース - AWS クラウドセキュリティ | AWS](http://aws.amazon.com/jp/security/security-resources/)
* [コンプライアンスリソース –アマゾン ウェブ サービス (AWS)](http://aws.amazon.com/jp/compliance/resources/)
* [AWS_Security_Best_Practices.pdf](http://media.amazonwebservices.com/jp/wp/AWS_Security_Best_Practices.pdf)

Services
----

* [[aws-cli]]
* [[AWS Billing]]
* [[Amazon EC2]]
* [[Amazon ECS]]
* [[Amazon S3]]
* [[AWS CloudWatch]]
* [[Amazon SNS]]
* [[Amazon SQS]]
* [[AWS Lambda]]

### AWS Trusted Advisor

AWSベストプラクティスの適用状態を自動審査してくれるサービス。

[AWS再入門 AWS Trusted Advisor編 ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/cm-advent-calendar-2015-getting-started-again-aws-td/)

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

### Amazon SES

* メール送受信サービス。従来は送信だけだったが受信も可能になった。
  * [[新機能]Amazon SES でメール受信が出来るようになりました！ ｜ Developers.IO](http://dev.classmethod.jp/cloud/receiving-email-with-amazon-ses/)
* メール送信には審査が必要（SPAMでの使用を避ける意図）。

### AWS Key Management Service

暗号化キーを簡単に作成、管理し、AWS各リソースの暗号化を行う。

### AWS Direct Connect

[AWS Black Belt Techシリーズ AWS Direct Connect](http://www.slideshare.net/AmazonWebServicesJapan/aws-black-belt-tech-aws-direct-connect)

### AWS Config

構成変更のロギング。有効化することで使用可能になる。無償だが保存先S3バケット料がかかる。Config Rulesで構成変更の自動チェックができる。

### AWS CloudTrail

APIコールのロギング。CloudWatch Logsを通すことで監視も可能になる。
