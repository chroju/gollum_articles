apk
----

Alpine Linuxにおけるパッケージ管理。

```bash
# パッケージインストール（複数同時可能）
$ apk add vim zsh
# 最新のインデックスを利用してインストール
$ apk --update add vim
# キャッシュを残さない
$ apk --no-cache add vim
```