Systemd
----

* initシステムの後継。CentOSではVer.7より標準。

### コマンド

* `systemctl`: initでいう`service`に近い。サービスの管理や起動停止等司る。
* `journalctl`: Systemdのログを確認する。
  [systemd のログを確認する journalctl – 愛しく切ない1bed](http://1bed.saloon.jp/?p=684)


init
----

SystemV系等のプログラム制御。

### 動作の流れ

1. `PID 1`で起動。
1. `/etc/inittab`を元として、`/etc/rc.d/rc.sysinit`よりブート時の処理（初期化や読み込み）を実施。
1. 同様に`inittab`からrunlevelに応じたrcスクリプトを`/etc/rcX.d/`配下から実行。


参考
----

* [Windowsユーザーに教えるLinuxの常識（10）：Linux起動の仕組みを理解しよう［init/inittab編］ (1/2) - ＠IT](http://www.atmarkit.co.jp/ait/articles/0204/02/news002.html)
* [Windowsユーザーに教えるLinuxの常識（最終回）：Linux起動の仕組みを理解しよう［rcスクリプト編］ - ＠IT](http://www.atmarkit.co.jp/ait/articles/0206/04/news001.html)