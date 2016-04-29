ログの集約を行うためのレガシーなツール。

* デフォルトでは `/var/log/messages` に出力される。
* `/etc/syslog.conf` でseverity、slectorごとに出力先を変えられる。
* 一般的にはサーバー1台を設けて集約させることが多い。