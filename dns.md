DNS
----

* [DNSの仕組みと運用（1）：DNSの仕組みの基本を理解しよう - ＠IT](http://www.atmarkit.co.jp/ait/articles/0112/18/news001.html)
* 名前解決。ドメインからのアクセスを適切なIPへ連携するための仕組み。

### レコード

* Zone Apexに対してCNAMEレコードは設定できない。
  * この仕様はAWSの場合にハマるので注意→ [ドメイン名を使ってEC2を運用していたら、ELBのスケールアウトで苦労した話 - MUGENUP技術ブログ](http://mugenup-tech.hatenadiary.com/entry/2014/05/12/104009)

BIND
----
現在広く普及しているDNSサーバー。ISCライセンスに基づくフリーソフトウェア。

### 構成

#### named.conf

すべての起点となるブートファイル。各種ゾーンファイルをここから参照する。オプション等の設定もここで行う。

#### ゾーンファイル

名前解決の対照表を記載したデータファイル。デフォルトでは`/var/named/`配下に置かれる。ドメイン、セグメントごとに正引きと逆引きでそれぞれファイルを用意する。

#### named.ca

ヒントファイル。世界各地のルートサーバー情報が記載されている。たまに更新されるらしいが、基本は更新不要。


ゾーンファイルの書式
----

テスト
----

named.confテスト用の`named-checkconf`コマンド、ゾーンファイル用の`named-checkzone`コマンドが存在する。文法しか確認しないみたいだがやるに越したことはない。

cf. http://futuremix.org/2010/03/bind-named-checkconf-error-check-command