### ファイルの扱い

ファイルシステムの見た目上のファイルと、実際のマウントディスク上にあるファイルはしばしば乖離する。例えば`rm`でファイルを削除した際、ファイルシステム上はすぐ削除処理が行われるが、実際にディスクから削除されるのは、ファイルを使用しているプロセスがいなくなったとき＝i_count（オープン数）が0になったときである。

* [ファイル削除してもディスク使用容量を下がらない!?（dfとduの違い） - 分析インフラエンジニア(+α フロントエンド)　eratostennis's blog](http://eratostennis.hatenablog.com/entry/2015/02/15/185924)

NFS
----

* Network File System。ネットワークマウントによる分散ファイルシステム。
* `mount`コマンドを使用するか、`/etc/fstab`でマウントドライブの設定を行う。
  [NFSクライアント設定ファイル](http://web.mit.edu/rhel-doc/4/RH-DOCS/rhel-rg-ja-4/s1-nfs-client-config.html)
