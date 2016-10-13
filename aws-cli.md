profile
----

実行アカウントをプロファイルで管理している。現在のプロファイルを確認するには以下。他のプロファイルの権限でコマンド実行する際は、`--profile`オプションを使用する。使用していない場合は`default`が使われる。

```bash
$ aws configure list
      Name                    Value             Type    Location
      ----                    -----             ----    --------
   profile                <not set>             None    None
access_key     ****************RE2A              env
secret_key     ****************9DO2              env
    region           ap-northeast-1              env    AWS_DEFAULT_REGION
```

query
----

* 表示項目の絞り込みに使用する。
* [AWS CLI の query による絞り込み - Qiita](http://qiita.com/draco/items/fa09ae0c2f51de9de449)
* [JMESPath](http://jmespath.org/)というjsonをパースするための書式で指定する。`jq`相当のことは賄えるはず。
  * 基本的には`.`で階層を下っていき、`[]`で配列内を探索する。
  * 複数要素にアクセスする際は`{ID: InstanceId, IP: PrivateIpAddress}`のようにKey-Value指定になる。

filters
----

* 表示 **リソース** の絞り込み＝フィルタリングに使用する。
* JMESPathではなく、`'Name=hoge,Values=fuga`の形式で特定の値が何であるか？という形でフィルタ条件を指定する。
* AND検索は先の文を複数並べていく。OR検索はValuesに複数の値をカンマ区切りで並べる。
* コマンドによっては出力を絞るオプションが用意されている場合もあるため、`filters`を使用しなくて良いこともある。
* すべてのパラメーターがfiltersで指定可能ではない。指定できるものは各コマンドのhelpで確認する。

output
----

基本はjson。`--output`オプションで`text`と`table`が選べる。

tips
----

### References

AWS CLI Documentsにはオプションの記載がない場合がある。APIドキュメントを合わせて参照したり、AWS-Shellのバルーンヘルプを確認することで情報が補完できる。

参考
----

* [(レポート) DEV301: AWS CLIによる自動化 #reinvent ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/reinvent2015_dev301-automating-aws-with-the-aws-cli/)
  * 見ていると少し辛い気持ちになるが、かなりガチガチにCLIで頑張ろうとしている。
  * jsonのパース、jqの使い方に精通していくしか答えがないという感じ。