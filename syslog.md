ログの集約を行うためのレガシーなツール。

* デフォルトでは `/var/log/messages` に出力される。
* `/etc/syslog.conf` で出力先を変えられる。
* 出力先変更のフィルター条件としては、「何のログであるか」を示す`Facility`と、「ログの重大度」を示す`Sevirity`を用いる。これらは各ログに`Facility.Severity`の形式で指定されている。
  * [syslogを押さえよう！ | Think IT（シンクイット）](https://thinkit.co.jp/article/724/1)
  * FacilityとSeverityを指定してログを吐くには、`logger`コマンドの`-p`を使う場合が多い。
* 一般的にはサーバー1台を設けて集約させることが多い。

rsyslog
----

RHEL6.0から標準採用された次世代syslog。syslog.confと互換があり、移行しやすい一方で多数の機能追加がある。

* 集約したsyslogの再転送。
* swatchのようなログフィルタリングとメール通知機能。
* ログの送信元別保存機能。

[水銀室 rsyslogのインストール -CentOS最短構築支援-](http://hp.vector.co.jp/authors/VA022911/tec/centos/rsyslog1.htm)