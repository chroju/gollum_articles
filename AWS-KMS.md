Key Management Service。データ暗号化キーを暗号化するキーを保管してくれている。AWS各サービスでの暗号化／復号化処理に用いる。

ユースケース
----

* S3の暗号化キーを保管。
* Lambda内で使用するAPIキーをKMSキーで暗号化。

参考
----

* [KMSで認証情報を暗号化しLambda実行時に復号化する ｜ Developers.IO](http://dev.classmethod.jp/cloud/decrypt-sensitive-data-with-kms-on-lambda-invocation/)