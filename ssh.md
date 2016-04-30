ssh
========

ssh-keygen
----

鍵長4096bitのRSAで。

```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```


FingrePrintの確認省略
----

* StrictHostKeyChecking
  * known_hostsにないホストへの接続時の挙動。
  * `no`で`ask`なしに接続可能。
* UserKnownHostsFile
  * known_hostsのパス指定。
  * `/dev/null`にすることで確認がスルーされるので、ホスト側のフィンガープリント変更をスルーできる。
* 参考：[OpenSSHの警告メッセージを黙らせる | Siguniang's Blog](https://siguniang.wordpress.com/2014/02/28/get-rid-of-openssh-warning-message/)