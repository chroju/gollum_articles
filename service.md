Systemd
----

* initシステムの後継。CentOSではVer.7より標準。
* わかりやすい解説→ [「Systemd」を理解する ーシステム起動編ー | ギークを目指して](http://equj65.net/tech/systemd-boot/)

### コマンド

* `systemctl`: initでいう`service`に近い。サービスの管理や起動停止等司る。
* `journalctl`: Systemdのログを確認する。
  [systemd のログを確認する journalctl – 愛しく切ない1bed](http://1bed.saloon.jp/?p=684)

```bash
# ログを省略せず表示
$ journalctl -a
# 特定Unit（サービス）のログを表示
$ journalctl -u servicename
```


init
----

SystemV系等のプログラム制御。

### 動作の流れ

1. `PID 1`で起動。
1. `/etc/inittab`を元として、`/etc/rc.d/rc.sysinit`よりブート時の処理（初期化や読み込み）を実施。
1. 同様に`inittab`からrunlevelに応じたrcスクリプトを`/etc/rcX.d/`配下から実行。

### runlevel

動作モード。0が停止、6が再起動、1～5はディストリによる。各runlevelとrcスクリプトを紐付けて、どのモードでどのサービスが起動すべきかを定義する。`init`コマンドで切り替えられる。

### rcスクリプト

* 実体としてはサービス制御のためのシェルスクリプト。
* `/etc/rcX.d`配下に配置されるのはシンボリックリンク。実物は`/etc/init.d`配下。
* `service`コマンドによる制御と同様に`start`や`stop`が行えるが、スクリプトを直接実行するのではなく、`service`を通すのが望ましい。
  参考：[デーモンの起動・終了にはserviceコマンドを利用しよう - インフラエンジニアway - Powered by HEARTBEATS](http://heartbeats.jp/hbblog/2013/06/service-start-stop.html)

### コマンド

* サービスの起動、終了は`service hoge start/stop/restart`等で実施する。
* 有効化、無効化は`chkconfig --level 235 hoge on`の形式で行う。確認する際は`--list`。

参考
----

* [Windowsユーザーに教えるLinuxの常識（10）：Linux起動の仕組みを理解しよう［init/inittab編］ (1/2) - ＠IT](http://www.atmarkit.co.jp/ait/articles/0204/02/news002.html)
* [Windowsユーザーに教えるLinuxの常識（最終回）：Linux起動の仕組みを理解しよう［rcスクリプト編］ - ＠IT](http://www.atmarkit.co.jp/ait/articles/0206/04/news001.html)