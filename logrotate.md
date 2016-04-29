* ログローテーションを実現するためのツールがある（便利！）
* RHELではデフォルトインストール済みの模様。なければパッケージで入れる。
* `/etc/logrotate.conf` でローテーション世代数やサイクルを定義する。
* `/etc/logrotate.d/` 配下に対象ログファイルの名前で設定ファイルを設置し、詳細を記載する。
  例えばhttpd.logであれば、ファイル `httpd` を作成し、以下のように記述。

```
$ vi /etc/logrotate.d/httpd

/usr/local/apache2/logs/access_log /usr/local/apache2/logs/error_log {
      weekly
      rotate 4
      missingok
      sharedscripts
      postrotate
           /bin/killall -HUP `cat /usr/local/apache2/logs/httpd.pid 2>/dev/null` 2> /dev/null
      endscript
} 
```

参考
----

* [logrotate によるログのローテーション](http://linux.kororo.jp/cont/server/logrotate.php)