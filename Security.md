SSL/TLS
----

* 機能は認証（証明）、暗号化、改ざん検出の3点。SSLが古いバージョンにあたり、最新はTLS1.2。
* ドメイン所有元を証明するサーバー証明書、サーバー証明書の認証局を証明する中間証明書、クライアント側のルート証明書による証明書チェーンから成る。
* ルート証明書が古い環境に備えた「クロスルート証明書」という手段も在る。
* SSL証明書の問題は各社が提供するチェッカーで確認できる。 [SSL Checker | Symantec CryptoReport](https://cryptoreport.websecurity.symantec.com/checker/views/certCheck.jsp)
  * opensslコマンドでも確認は可能。[OpenSSLコマンドの備忘録 - Qiita](http://qiita.com/takech9203/items/5206f8e2572e95209bbc)
* いわゆる「オレオレ証明書」というのは認証局がルート証明書からのチェーンで証明できず、信頼性の低いものを言う。

### DV/OV/EV

信頼性が異なる。

* DV: 申請者の権利だけが確認され、会社情報は確認されていない。
* OV: 会社（組織）の存在確認が行なってある。アドレスバーの鍵は緑。
* EV: 会社の連絡先など複数の情報が確認された最も信頼性の高いもの。アドレスバー全体が緑になり、組織名が表示される。

### 参考

* [サーバー証明書のつくりかたと、その原理 - kirinwikiblog](http://kirinwiki.hatenablog.com/entry/2014/07/03/220315)
* [第3回　SSL証明書ビギナー歓迎！ httpsから始まるURLの役割と仕組みを0から学ぼう：Webデザイナーなら知っておくべき サーバ知識相談室｜gihyo.jp … 技術評論社](http://gihyo.jp/design/serial/01/server-knowledge/0003)
* [SSL/TLSの基礎と最新動向](http://www.slideshare.net/shigeki_ohtsu/security-camp2015-tls)
