### SSLクライアントとして使う

* `openssl s_client`でSSLクライアントとして動作する。
* 標準入力から入力を受け付けて通信する。
* 証明書情報をデフォルトで表示する（不要な場合は`--brief`を使う）ため、標準入力から`/dev/null`を流すことで通信は瞬時に終了し、証明書情報だけを取得することができる。

```bash
$ openssl s_client -connect hostname:443

# 証明書情報だけ取得。-showcertsオプションでチェーン等の情報をフルで取得できる。
$ openssl s_client -connect hostname:443 -showcerts < /dev/null 2> /dev/null | openssl x509 -text
```