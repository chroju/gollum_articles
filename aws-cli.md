profile
----

実行アカウントをプロファイルで管理している。現在のプロファイルを確認するには以下。

```bash
$ aws configure list
      Name                    Value             Type    Location
      ----                    -----             ----    --------
   profile                <not set>             None    None
access_key     ****************RE2A              env
secret_key     ****************9DO2              env
    region           ap-northeast-1              env    AWS_DEFAULT_REGION
```

output
----

基本はjson。`--output`オプションで`text`と`table`が選べる。

参考
----

* [(レポート) DEV301: AWS CLIによる自動化 #reinvent ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/reinvent2015_dev301-automating-aws-with-the-aws-cli/)
  * 見ていると少し辛い気持ちになるが、かなりガチガチにCLIで頑張ろうとしている。
  * jsonのパース、jqの使い方に精通していくしか答えがないという感じ。