Network @ Linux
====================

設定方法はおそらく2種類。手動で設定ファイルを書き換えるか、NetworkManagerを使うか。

設定ファイル
----------

主に3つ。

* /etc/sysconfig/network
* /etc/sysconfig/network-scripts/ifcfg-eth0
* /etc/resolv.conf

`/etc/sysconfig/network`は全般的なネットワークの設定を行う。ホスト名の設定もここ。

`ifcfg-eth0`はNICの設定。複数枚NICがある場合はそれに紐ついたファイルが存在しているはず。IPアドレス、MACアドレス、デフォルトゲートウェイなどを記入する。

```
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
HWADDR=00:00:00:00:00:00
IPADDR=192.168.0.5
NETMASK=255.255.255.0
BROADCAST=192.168.0.255
GATEWAY=192.168.0.1
USERCTL=no
TYPE=Ethernet
```

DHCPの場合はこんなの。

```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
HWADDR=00:00:00:00:00:00
USERCTL=no
TYPE=Ethernet
```

MACアドレスをここに書くことが得策なのかはよくわからない。MACアドレス自体は物理NIC側で固定のものを持っているため、ここで記載したものが実際の固定値と差異があるとネットワークは上がらなくなる。下手に指定しない方がベターかと思う。

resolv.confは名前からある程度想像がつくが、名前解決まわりの設定を記載する。またネットワークという意味では`/etc/hosts`も変更対象である。ホスト名を変えるときは、ここでlocalhostsの設定も替えなくてはならない。


NetworkManager
----------

統合的なネットワーク管理ツール。`nmcli`でCLI、`nmtui`でTUIでの設定ウィザードが開く。自動管理してくれるので楽ではある反面、挙動をきちんと把握していないと予期せぬ設定が勝手に書き換わっている可能性がある。

従来は機能的な制約が強く、無効化して先述のファイルを手動編集するのが一般的だったらしいが、RHEL7ではNetworManagerが推奨になった。なお、手動編集がよいのであればサービス`networkmanager`を停止、自動起動無効化し、`network`を起動する。


