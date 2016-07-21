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

### CT (Certificate Transparency)

* 証明書発行の監査ログを公開し、証明書の透明性を高めるための技術仕様。Googleの考案を元にRFC6962で規格化されている。
* 監査者は定期的にログをチェックすることで、第三者が不正に証明書発行を行なっていないか確認を行うことができる。
* ロギングを行なったEV証明書にはSigned Certificate Timestamp（SCT）が埋め込まれる。ChromeはSCTをチェックすることで、その証明書がCTに対応した透明性の高いものであるかを判断している。
* CT対応を行う場合、証明書作成→ロギング→SCTを埋め込んで証明書発行という順序となるため、実際の証明書発行前にロギングが必要になってしまう。
  * 従って実際の証明書と同じIDを持つPrecertificateを使ってロギングを行い、Precertificateは絶対公開しないようにするというちょっとしたネジレがあるらしい。
* Chromeは41より、CTのないEV証明書は緑色表示をしないよう仕様変更している。
* 参考：[Certificate Transparencyについて勉強会で発表したので、その補足や落ち穂拾い - ろば電子が詰まっている](http://d.hatena.ne.jp/ozuma/20150516/1431769141)

### 参考

* [サーバー証明書のつくりかたと、その原理 - kirinwikiblog](http://kirinwiki.hatenablog.com/entry/2014/07/03/220315)
* [第3回　SSL証明書ビギナー歓迎！ httpsから始まるURLの役割と仕組みを0から学ぼう：Webデザイナーなら知っておくべき サーバ知識相談室｜gihyo.jp … 技術評論社](http://gihyo.jp/design/serial/01/server-knowledge/0003)
* [SSL/TLSの基礎と最新動向](http://www.slideshare.net/shigeki_ohtsu/security-camp2015-tls)
