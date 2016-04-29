LVMの拡大・縮小
==========

TODO
----

* umountしてから実行している手順もあるけどしなくていい認識で合ってる？
* ファイルシステム拡張後のチェックをした方が無難そう。
* 増設したディスクを認識させるには再起動しかない？
* ファイルシステムについての見識を深めたい。

拡大
----

1. 新規ディスク上に物理ボリュームの作成
```bash
$ pvcreate /dev/sdb
```
1. ボリュームグループを新規物理ボリューム上へ拡張
```bash
$ vgextend centos /dev/sdb
```
1. 拡張対象の論理ボリュームを拡張（以下の場合は追加した物理ボリューム全域（100%）を利用）
```bash
$ lvextend -l +100%FREE /dev/centos/root
```
1. ファイルシステムを拡張
```bash
# xfsの場合
$ xfs_growfs /dev/centos/root
# ext3/ext4の場合
$ resize2fs /dev/centos/root
```

確認系のコマンド
```bash
# 物理ボリューム
$ pvdisplay [-v VolumeName]
# 論理ボリューム
$ lvdisplay [-v VolumeName]
# ボリュームグループ
$ vgdisplay [-v VolumeGroup]
# マウント済みボリュームをファイルシステム付きで確認
$ df -hT
```

参照
----

* [LVMで新たにディスクを追加して既存のLVを拡張する - Qiita](http://qiita.com/g_maeda/items/3602dc2f7af3f711f9c4)
* [LVMで 論理ボリュームの作成、拡張、縮小、複製 - Qiita](http://qiita.com/TsutomuNakamura/items/93c6333c8dd32aeb197a)
* [VirtualBoxで仮想HDDを追加して Linuxのディスク空き容量を増やす - Qiita](http://qiita.com/egnr-in-6matroom/items/d284dd306753b2f0591a)
* [CentOS 7(XFS)でLVMディスク拡張でハマったこと - Qiita](http://qiita.com/fetaro/items/d7dc74262633ba474bc8)