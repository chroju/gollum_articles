インストールから起動まで
====

RubyGemsにより配布されているため非常に簡単。`fluent.conf`は起動前に要編集。

```bash
gem install fluentd --no-ri --no-rdoc
fluentd --setup ./fluent
fluentd -c ./fluent/fluent.conf -vv &
```

概念
====

* 入力を`source`、出力を`match`で定義し、データストリームをコントロールする。
* 入力、出力されるデータの種別はそれぞれ`type`を指定する。`type`にはデフォルトのものの他、プラグインで提供されているものが多数あり、例えばElasticsearch出力用のプラグイン、S3出力用のプラグイン等を使うことで、データを簡単にパースして送信ができる。
* 出力条件のフィルタリングは、入力されたデータについた`tag`により判定される。syslog的。`source`ディレクティブの中で`tag`を付与することができる。

参考
====

* [fluentdインストール（丁寧な説明つき） - Qiita](http://qiita.com/shuntaro_tamura/items/e897cdc8a155cfcf9da7)