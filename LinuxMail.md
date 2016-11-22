email
========

MTA
----

Mail Transfer Agent。メールを実際に送信先へ送信するところを担うソフトウェア。実装としてはsendmail、postfix、qmail、MS Exchangeなど。Linuxでは古き良きsendmail、最近はpostfixという印象。10年以上前の記事だが取りあえず参考に以下。

* [An obsolete MTA, sendmail (Make full use of qmail, a high performance mail transfer agent)](http://www.gcd.org/sengoku/docs/NikkeiLinux00-03/sendmail.ja.html)

MUA
----

Mail User Agent。メールの作成や管理などを行ういわゆるメーラー。`mailx`コマンドを使う場合が多いか。


Tools
========

mail(x)
----

mailコマンド（mailx）によるメール送付。本文は標準入力から受け付けるほか、入力なしでコマンド実行すれば対話式に記入することもできる。欠点としてヘッダーが触れないので、文字コードはsjis、base64等適宜使う必要がある。

```bash
$ mail -s subject -r from@example.com -c cc@example.com -b bcc@example.com to@example.com
```

送信状況の確認は`-v`オプションを使う。

sendmail
----

mail同様に標準入力を受け付けるが、bodyだけではなくヘッダー部分からすべて流し込める。従ってContent-Typeを使えば文字コードを問わず送信ができる。

```bash
# 最低限これだけでも送れる。
$ cat mail.txt | sendmail to@example.com
# -iで本文中の.のみの行をEOF扱いしない。-fでReply-toを指定できる。
$ sendmail -i -f from@example.com to@example.com
```

postfix
----

* [Postfixで中継サーバ(転送)を噛ます時の設定 - Qiita](http://qiita.com/kenjiskywalker/items/2f00a0ae56136d184993)

周辺知識
========

base64
----

MIMEタイプ。メールが7bit 65文字のテキストしか送れなかったことから生まれた符号化形式。現状は種々のMIMEタイプが生まれたことでbodyについてはバイナリ等も含められるようになったが、ヘッダーは現状も7bitの制限があるため、base64への変換を通す必要がある。

* [base64ってなんぞ？？理解のために実装してみた - Qiita](http://qiita.com/PlanetMeron/items/2905e2d0aa7fe46a36d4)
* [Multipurpose Internet Mail Extensions - Wikipedia](https://ja.wikipedia.org/wiki/Multipurpose_Internet_Mail_Extensions)