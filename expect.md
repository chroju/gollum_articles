expect
========

これは何？
----

* Tclと呼ばれるリスト構造型のスクリプトが持つスーパーセット。
* スクリプト内で対話処理をこなす際に使用される。


基本的な使い方
----

Sample
```bash
#!/bin/bash
expect -c "
spawn ssh foo@var.server
expect \"Password:\"
send \"mypassword\n\"
interact
"
```
シェルスクリプト内で使用する場合は`expect -c`の引数として実行内容を渡す。各コマンドの意味は下記の通り。

* spawn: 実行するコマンド
* expect: コマンド実行結果として期待する文字列
* send: `expect`にマッチする出力があった場合に入力する文字列
* interact: 制御をユーザーに戻す


様々な使い方
----

### switch
```bash
#!/bin/bash
expect -c "
spawn ssh foo@var.server
expect \"Password:\" {
  send \"mypassword\n\"
} \"Are you sure you want to continue connecting (yes/no)?\" {
  send \"yes\n\"
  expect \"Password:\"
  send \"mypassword\n\"
}
interact
"
```

`{}`を使うことで分岐処理が書ける。

```bash
expect -c "
spawn ssh server ls | grep foo
expect {
  default { exit 2 }
  "foo"
}
```

`expect`した値が出力されなかった場合のデフォルト処理を書ける。エラーハンドリングに有効。

### 実行結果の変数入力
```bash:whoami.sh
#!/bin/bash
result=$(
expect -c "
log_user 0
spawn ssh foo@var.server ls -la whoami
expect \"Password:\" {
send \"mypassword\n\"
interact
")
echo $result
```
実行結果
```bash
$ sh whoami.sh
foo
```
`expect`全体をコマンド置換する。デフォルトでは`expect`内で実行されたすべての標準出力が変数に代入されるため、`log_user 0`により出力を抑制する。

複数のコマンド実行があり、出力を限定したい場合は`$expect_out`配列を使う。`$expect_out(0,string)`で直前の`expect`によるヒットのうち0番目部分が、`$expect_out(buffer)`によりヒットに用いられた出力全体を呼び出せる。
```expect
send \"show run | grep vserver | grep ${target}\r\"
expect \"bind *\"
log_user 1
puts \$expect_out(0,string)
expect eof
exit
```

### 変数の参照
bash等、別のシェルから呼び出して使用する場合、expect内で定義した変数は`\$var`、expect外で定義した変数は`$var`で呼び出す。

### cron実行させる場合
`interact`でユーザー側に操作を戻す代わりに、`expect eof; exit`で明示的に終了させる必要がある。

参考：[automation - Expect script does not work under crontab - Stack Overflow](http://stackoverflow.com/questions/7494115/expect-script-does-not-work-under-crontab)

Tcl
----
本格的に使用する場合はTclの文法を用いることで、複雑な処理が可能になる。詳細は以下あたりを参照。

[Tcl8.4.1マニュアル　目次](http://www.freesoftnet.co.jp/webfiles/tclkits/doc/TclCmdRef/tcl_contents_jp.htm)

参考
----

* [Linuxの対話がめんどくさい?そんな時こそ自動化だ！-expect編- - Qiita](http://qiita.com/ine1127/items/cd6bc91174635016db9b)
* [expectで対話型シェル - MB blog](http://lake-michigan.hatenablog.com/entry/20110412/1302600915)
* [expect内でループ処理をする。 - TOYBOX](http://d.hatena.ne.jp/neil_sk/20120612/1339514573)
* [expectを外部から使用する際に気を付けること - Qiita](http://qiita.com/komeiy/items/11ac7ed2a0027d549764#2-3)