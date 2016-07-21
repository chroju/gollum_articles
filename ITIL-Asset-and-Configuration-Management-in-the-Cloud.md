原文（2016-07-21確認）：https://d0.awsstatic.com/whitepapers/AWS_Asset_Config_Management.pdf

まず前提として、AWS CAFの導入を推奨。CAFはITILと互換性のあるAWSのベストプラクティス。

## Asset and Configuration Management in the Cloud

* 資産(assets)：サービス提供に寄与するリソースや機能のこと
* 構成(configuration items)：ITサービス提供のために管理する必要のある資産（資産⊇構成）

### 資産／構成管理の目的は？

* 正確な構成情報を保つことで、問題解決を早めたり、意思決定の材料としたりすること。
* 正確ではない構成情報が故に引き起こされる、質的 / 法的問題の発生を抑止すること。
* サービスやインフラの状態を過去、現在、計画的な未来にわたって維持しておくこと。

### クラウド環境のCMDB例

* 包括的で動的なクラウドリソースの管理を行い、
  Auto Scalingのようにポリシーを変更すれば実際のリソースも作成 / 削除される。

### CMDBの構築

Configの活用

* 現存する構成から情報を吸い上げてCMDB化するパターン。
* サポートされているサービスについては、すべて自動で構成情報が記録される。
* 現状の構成、ヒストリカルな構成変更を検索することも可能。

### Configuration Lifecycle

* AMIで組織のポリシーに沿ったマシンイメージのテンプレートを作成する。
* インスタンスの状態変動は手動でも管理できるが、ChefやPuppetといった堅牢なツールを使う。
* サービス環境全体構成のテンプレートにはCloudFormationを使い、JSONで「ソース管理」を行う。
* アプリケーションライフサイクルは現代ではCIがベストだが、CodePipelineやCodeDeploy、CodeCommitを活用できる。
