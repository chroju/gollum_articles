* [[aws-cli]]
* [[Amazon ECS]]
* [[Amazon SNS]]
* [[AWS Lambda]]

Other Services
----

### Amazon ElasticBeanstalk

PaaS。アプリを選択するとそれに必要なEC2等を勝手に構築してくれる。デプロイはzipファイルをアップロードするだけでOK。開発、ステージング、本番といった環境の棲み分けもできる。heroku的だが、構築したリソース分の課金が発生するため注意は必要。

### AWS CodeDeploy

S3やGitHub上のアプリケーションコードを決められた箇所へ配置する（デプロイ）作業を制御するサービス。

[AWS再入門 AWS CodeDeploy 編 ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/cm-advent-calendar-2015-aws-re-entering-codedeploy/)

### Amazon Inspector

EC2にエージェントを入れるとCVEの該当有無チェックやランタイム解析を自動で行なってくれる。

[AWS Inspectorで脆弱性を検知させる ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/inspector-finding-security-issue/)

### Amazon CloudFront

CDN。

[AWS再入門 Amazon CloudFront編 ｜ Developers.IO](http://dev.classmethod.jp/cloud/cm-advent-calendar-2015-aws-re-entering-cloudfront/)

### AWS Direct Connect

[AWS Black Belt Techシリーズ AWS Direct Connect](http://www.slideshare.net/AmazonWebServicesJapan/aws-black-belt-tech-aws-direct-connect)