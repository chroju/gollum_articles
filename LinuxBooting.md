/etc/profile.d/*
----

本来はbashの読み込み機能？　bash起動時に`/etc/profile`が真っ先に読み込まれるが、このシェルスクリプト内に`/etc/profile.d/*`内のスクリプトを読み込む設定が書かれている。各ツールで必要な環境変数やエイリアスの設定を行なっていることが多い。