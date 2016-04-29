## 書式

```
* * * * * commnad
```

* 左から分、時、日、月、曜日。
* 曜日は日曜日0から始まる。
* 範囲指定（1-5）が可能。
* 複数指定（1,3,5）が可能。
* 間隔指定（*/10）が可能。これを分に指定した場合は10分間隔。
* 複合（1,3-5）も可能。

## 設定

### コマンド

```bash
# 編集
$ crontab -e
# 表示
$ crontab -l
# 削除
$ crontab -r
# 実行ユーザーを変更
$ crontab -u foo -l
```

* `e`と`r`が隣り合わせで逆の意味なので戦慄する人が多いみたい。
  * `crontab -i`で削除時の確認が出るので、`crontab`にaliasしている人多数。
* コマンドによる設定は実行ユーザーごとになる。
* 設定内容は`/var/spool/cron`内に保存される。

### ファイル直接編集

* `/etc/crontab`を直接編集することでシステム全体設定が可能。こちらは周期設定とコマンドの間に実行ユーザー名を入れる書式になる。
* `/etc/cron.d`内に置いたファイルも実行対象となる。ファイルはroot:rootの644とする。
* `/etc/cron.daily`や`/etc/cron.weekly`ディレクトリに置いたファイルはディレクトリ名の間隔でランダム実行される。CentOS5.xまでは4:02頃の固定実行だったらしいが、6.xからcronie-anacronによるランダム実行に変更された。


## 実行結果の扱い

* デフォルトで出力結果はメインアカウントへメール通知される。
* メール通知が嫌であれば/dev/nullに捨ててしまう場合が往々にあるらしい。

```bash
* * * * * command > /dev/null 2>&1
```

* ただし行儀が良くはないのできちんとMAILTOを設定する、失敗時だけログを送ってくれる[cronlog](https://github.com/kazuho/kaztools/blob/master/cronlog)を使う、loggerコマンドを使ってsyslogに送るといった手法が推奨される。
* crondの作動結果自体は`/var/log/cron`に記録される。


## 参考

* [crontab -e は「絶対に」使ってはいけない - ろば電子が詰まっている](http://d.hatena.ne.jp/ozuma/20120711/1342014448)
* [cron で > /dev/null して椅子を投げられないための3つの方法 - 酒日記 はてな支店](http://sfujiwara.hatenablog.com/entry/20120613/1339547638)
* [cron力をつけよう！全てのcrontab入門者に贈る9個のテクニック · DQNEO起業日記](http://dqn.sakusakutto.jp/2012/06/cron_crontab9.html)