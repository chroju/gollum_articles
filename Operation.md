* [システムの負荷の原因を切り分ける方法 - Qiita](http://qiita.com/k0kubun/items/8ab1dfa7c0359d8e618d)
* [アプリエンジニア向け：「サーバがなんか重い」時にすること - Qiita](http://qiita.com/yuku_t/items/2f5341e4aa635800a0a1)
* [サーバが重い時、sar(sysstat)で簡易なボトルネック特定 - Qiita](http://qiita.com/kidach1/items/07637a5baa0da7d52e6a)
* [【RHEL】linuxのメモリ使用率(利用率)の計算方法 - のぴぴのメモ](http://nopipi.hatenablog.com/entry/2015/09/13/181026)

Operation Commands
----

ps

* `a`で他のユーザーのプロセスも表示、`u`でユーザー名を表示、`x`で端末を持たないプロセスも表示、`f`で親子関係を表示。

pgrep
pkill

* 怖いからあまり使いたくない。

vmstat
sar

```bash
# メモリの使用状況確認
$ sar -r
```

df

```bash
# 全体のディスク容量を人に優しく表示
$df -h
```
du
```bash
# カレント下の容量内訳を表示
$du -sh ./*
```
free

fdisk

hdparm

smartctl

top

uptime

uname

strace

dstat

netstat

iostat

```bash
# Listenポートも含めPID表示
$netstat -ap
```
last

lsof

ip

ss (netstat)

route

rsync

w

last

mail
```bash
$ echo 'body' | mail -s 'subject' -c cc@example.com -b bcc@example.com to1@example.com to2@example.com
```

### バックグラウンド実行

nohup

no-ttyでもコマンドの実行を続ける。標準出力及び標準エラー出力は`$HOME/nohup.out`にリダイレクトされる。
```bash
$ nohup tcpdump ...
```

&

コマンド末尾に付与することでバックグラウンド実行になるが、ttyは必要（ログアウトすると停まる）。nohupと合わせて使うことが多い。

disown

PIDかジョブ番号（`jobs`で確認する）を引数にして、実行中のジョブをバックグラウンドに回す。

### サーバー情報の確認

`/proc`にリソース関連の情報が提供されており、ファイルパスを`cat`することで情報が取得できる。procfsは擬似ファイルシステムであり、実際のファイルではない。

* /proc/meminfo：メモリ情報
* /proc/cpuinfo：CPU情報
* /proc/scsi：SCSI

