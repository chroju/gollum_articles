構成図
----

* [ネットワーク図を書くときに考えること - # cat /var/log/stereocat | tail -n3](http://d.hatena.ne.jp/stereocat/20120503/1336049616)
* [ネットワーク図を書くときに考えること(2) - # cat /var/log/stereocat | tail -n3](http://d.hatena.ne.jp/stereocat/20120708/1341733222)

用語
----

### リンクパススルー

* [WAN越えリンクパススルー - ネットワークエンジニアの実践メモ](http://blog.livedoor.jp/noah2944/archives/51822849.html)
  * 対向がDownしたときにリンクダウンするかどうか。
  * この設定がないと正しくフェイルオーバーしてくれなかったりする。
  * 背景：WAN回線Down障害時のLAN内機器Link down検知の正当性確認の中で。

### NATとPAT

* [シスコ資格：CCNAへの道 - IPアドレス編 第5回 NATとPATの基本動作を知る：ITpro](http://itpro.nikkeibp.co.jp/article/COLUMN/20080715/310823/)
  * ポート番号も用いた変換動作を行うのがPAT。一般的にはNAPTで、Ciscoの呼び方がPAT。

### VPN

* インターネット越しに仮想的な専用回線を設けて通信する技術。
  * IPsec : L3。IPパケット単位で暗号化、カプセリングを行う。片方向の通信に対するトンネルを設ける。受信側からもトンネリングが必要。
  * PPTP : L2。PPPフレームを暗号化。双方向の通信に対するトンネルを設ける。