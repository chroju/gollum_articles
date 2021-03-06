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
* [クラウドコンピューティングのためのアーキテクチャーベストプラクティス](http://d36cz9buwru1tt.cloudfront.net/jp/wp/AWS_WP_Cloud_BestPractices_JP_v20110531-3.pdf)
  * クラウドにおいてインフラをどう考えればいいか？に答えている。概念的にこれを頭に叩き込みたい。とてもいい。
  * システムの弾力性、マイクロアーキテクチャー、プログラマブルなインフラ、Design for failure、自動化あたりの話。

#### 概要をまとめたもの

* [[ITIL Asset and Configuration Management in the Cloud]]
* [[Well-Architected Framewrok]]

Services
----

* [[aws-cli]]
* [[AWS Billing]]
* [[Amazon EC2]]
* [[Amazon ECS]]
* [[Amazon RDS]]
* [[Amazon S3]]
* [[AWS CloudWatch]]
* [[Amazon SNS]]
* [[Amazon SQS]]
* [[AWS Lambda]]
* [[AWS KMS]]

### AWS IAM (Identity and Access Management)

* [AWS IAM ポリシーの参照 - AWS Identity and Access Management](http://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/reference_policies.html)

### AWS Trusted Advisor

AWSベストプラクティスの適用状態を自動審査してくれるサービス。

[AWS再入門 AWS Trusted Advisor編 ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/cm-advent-calendar-2015-getting-started-again-aws-td/)

### Amazon Route53

* DNSサービス。
* 単なるDNSサーバーの代替程度に考えていたが、わりと必須に近い。
* ELBやCloudFrontへのアクセスを独自ドメインで行いたい場合、独自ドメイン→AWS提供外部エンドポイントの転送が必要となるが、通常のDNSサーバーではZone ApexのドメインからCNAMEでホスト名への変換はできない。これを行うには、Route53のALIASレコードという機能を使わなければならない。詳細は [[dns]] も参照。

### Amazon ElasticBeanstalk

PaaS。アプリを選択するとそれに必要なEC2等を勝手に構築してくれる。デプロイはzipファイルをアップロードするだけでOK。開発、ステージング、本番といった環境の棲み分けもできる（形式としては「アプリケーション」を作成して、その中にzipで配置した各バージョンが存在し、環境に対していずれかのバージョンを充てるということになる）。heroku的だが、構築したリソース分の課金が発生するため注意は必要。

### Amazon Elasticsearch Service

* Elasticsearchの提供サービス。
* Kibanaもデフォルトで付いている。
* 一部サービス（CloudTrail等）はESへストリームを流すオプションを持っており、簡単に可視化ができる。
* 手元のPCでKibanaを見たいと思った場合、ポリシーをきちんと開けなくてはならないので注意。
  [【AWS】AWS Elasticsearchのkibanaを使うのに困ったこと - Qiita](http://qiita.com/fkana/items/a0ee1ec0f9a807ce818f)
* IAM Roleによる認証でREST APIを制限できるが、その際はリクエストに認証情報を載せる必要がある。 [Amazon Elasticsearch ServiceのIAM Roleによるアクセス制御 ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/amazon-es-iam-based-access-control/)
* CloudWatch Logs等、一部のサービスで「Stream to Elasticsearch Service」という一撃でESに流し込める機能がある。但しmappingの設定等はできないので注意→ [【運用】CloudTrailで取得した監査ログをElasticSearch Serviceで活用する【簡単設定】 ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/cloudtrail-to-elasticsearch-service/)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::xxxxxxxxxxx:role/role-name"
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:ap-northeast-1:xxxxxxxxxxx:domain/hoge/*"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:ap-northeast-1:xxxxxxxxxxx:domain/hoge/*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "0.0.0.0"
        }
      }
    }
  ]
}
```

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

* [AWS Config Rules用のGitHubリポジトリが公開されました！ ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/aws-config-rules-new-repository/)

### AWS CloudTrail

APIコールのロギング。CloudWatch Logsを通すことで監視も可能になる。
