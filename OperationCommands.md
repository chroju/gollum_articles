Operation Commands
----

ps

* `a`で他のユーザーのプロセスも表示、`u`でユーザー名を表示、`x`で端末を持たないプロセスも表示、`f`で親子関係を表示。

pgrep
pkill

* `pgrep　daemon`でdaemon名のプロセスをジャストで出す。`pkill daemon`でdaemon名指定でプロセスをkillできる。
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
$ df -h
# ファイルシステムの種別を表示
$ df -T
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

開いてから各キーを押下することで、表示形式をトグルで切り替えられる。

* `1`: CPU使用率をコアごとに表示。
* `f`: カラムの追加/削除。
* `R`: ソート。もう一度押すと逆順。`F`もしくは`<>`でソート対象のカラムを変更。
* `i`: idleなタスクの表示/非表示。
* `u`: 特定ユーザーのタスクだけを表示。
* `Z`: カラーリング切り替え。
* `B`: Bold表示の有効/無効。

```bash
# プロセス名に引数を含める（開いてから`c`でも可）
$ top -c
```

uptime

uname

strace

dstat

netstat

Deprecated。`ss`が代替。

```bash
# Listenポートも含めPID表示
$netstat -ap
```
iostat

ディスクIO状況の確認。

last

lsof

指定したプロセスのファイルディスクリプタを一覧する。

ip

ss (netstat)

route

rsync

w

ログインユーザーのチェック。

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

