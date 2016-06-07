* パケットキャプチャ。`-w`でファイルへ保存することができ、保存したファイルはWireshark等で開ける。
* 無防備に仕掛けると相当な容量を取り続ける可能性もあるので、扱いには注意が必要。

```bash
# ポートを80、ホストを192.168.1.1、インターフェースをeth0に制限
$ tcpdump port 80 host 192.168.1.1 -i eth0
# ファイルに保存して100MBずつローテート
$ tcpdump -C 100 -W /var/log/dump.log
# ログのバイト長を48（通信元先のみ）に制限し、100パケット受信したら終了
$ tcpdump -s 48 -c 100
# portやhostはnot指定も可能
$ tcpdump port 443 and not net 192.168.1.0 mask 255.255.255.0
```

参考：[tcpdump コマンドの使いかたをまとめてみた - sonots:blog](http://blog.livedoor.jp/sonots/archives/18239717.html)