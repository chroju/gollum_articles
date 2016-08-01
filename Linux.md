## Distribution

* [[CentOS]]
* [[Alpine Linux]]

## Kernel

* [[起動処理|LinuxBooting]]
* [[時間処理|Time]]
* [[ファイルシステム|LinuxFileSystem]]
* [[SIGNAL]]
* [[service]]
* [[jobs]]
* [[dmesg]]
* [[oom-killer]]
* [[マルチスレッドとマルチプロセス|MultiThreadsAndMultiProcesses]]
* [[FHS]]

## Command

* [[GNU]]
* [[make]]
* [[diff]]
* [[uname]]
* [[rsync]]
* [[expect]]
* [[less]]
* [[xargs]]
* [[テキスト処理コマンド|CommandsAboutText]]
* [[メール関連コマンド|LinuxMail]]
* [[圧縮展開コマンド|CommandsAboutCompress]]
* [[OperationCommands]]
* [[curlとwget|CurlAndWget]]
* [[tcpdump]]

### sort

```bash
# 整数順
$ sort -n
# 実数順
$ sort -g
# 人間が読める形式で比較（2Kと1Gとか）
$ sort -h
# 逆順
$ sort -r
# 区切り文字を指定（-t）、カラムを指定（-k）
$ sort -k 3,3 -t ':'
```

### time

時間計測。`time command`の形式で使用する。実際の経過時間と、CPU使用時間が取れる。

### script

ログ取得コマンド。`exit`か`ctrl-d`するまでログをテキストファイルに取り続ける。制御文字まで含んでしまうのが難点。

[scriptコマンドで作業ログを記録 ｜ Developers.IO](http://dev.classmethod.jp/server-side/os/scriptcommand/)

### alternatives

同一機能を持つ複数コマンドや、複数バージョンのOS内共存を可能とするコマンド。そのコマンドがどのパスを参照するかを一覧化して切り替える。Javaの複数バージョン共存に用いられることが多い。

* [alternatives でいろんなものを共存させる - いますぐ実践! Linuxシステム管理 / Vol.150](http://www.usupi.org/sysad/150.html)
* [CentOSのalternativesでJavaのバージョン管理 - TASK NOTES](http://www.task-notes.com/entry/20150530/1432954800)

## Package

* [[RPM]]
* [[APT]]

## Disk

* [[LVM概要|LVM]]
* [[LVMの拡張・縮小|LVM-extend-shrink]]
* [[NFS]]

## Network

* [[ネットワークの静的編集（非NetworkManager）|linux-network-static]]

## Ops

* [[syslog]]
* [[crontab]]
* [[logrotate]]
* [[locale]]