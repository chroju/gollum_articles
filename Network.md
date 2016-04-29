### リンクパススルー

* [WAN越えリンクパススルー - ネットワークエンジニアの実践メモ](http://blog.livedoor.jp/noah2944/archives/51822849.html)
  * 対向がDownしたときにリンクダウンするかどうか。
  * この設定がないと正しくフェイルオーバーしてくれなかったりする。
  * 背景：WAN回線Down障害時のLAN内機器Link down検知の正当性確認の中で。

### NATとPAT

* [シスコ資格：CCNAへの道 - IPアドレス編 第5回 NATとPATの基本動作を知る：ITpro](http://itpro.nikkeibp.co.jp/article/COLUMN/20080715/310823/)
  * ポート番号も用いた変換動作を行うのがPAT。一般的にはNAPTで、Ciscoの呼び方がPAT。