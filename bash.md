* [[基礎文法|BashGrammers]]
* [[コーディングスタイル|BashCodingStyle]]

tips
----

* [Qiitaに自分でまとめたやつ](http://qiita.com/chroju/items/7af3fd5faa26de4067f0)

### evalとグロブ展開

アスタリスクによるグロブ展開は、例えば変数に代入するとその段階で評価される。

```bash
$ ls
foo.txt bar.txt
$ TEXTS=(*.txt baz.txt)
$ echo $TEXTS
foo.txt bar.txt baz.txt
```

評価させたくない場合はクォートが必要になる。クォートした変数をあえて評価させる場合は`eval`を使う。

```bash
$ TEXTS=('*.txt' baz.txt)
$ echo $TEXTS
*.txt baz.txt
$ eval echo $TEXTS
foo.txt bar.txt baz.txt
```

ShellScript
----

### 文字装飾

echo結果に文字装飾を行う設定。エスケープが必要なので`-e`オプションが必須。

* `\e[${value}m` : 装飾の開始
* `\e[m` : 装飾の終了

`${value}`には数字で属性指定を行う。複数属性を並べる場合は`;`で区切る。

* [シェル - echoで文字に色をつける その1 - Miuran Business Systems](http://www.m-bsys.com/linux/echo-color-1)

### コーディングガイド

* 関数を多用して見通しを良くする。
* `usage`関数を準備してREADMEとして機能させる。
* 引数を`case`で分岐させて処理を担わせる。
* 変数参照は`${}`。コマンド展開は`$()`。関数名はlower case。定数はsnake case。

* [Googleの肩に乗ってShellコーディングしちゃおう - Qiita](http://qiita.com/laqiiz/items/5f72ca668f1c58176644)
* [使いやすいシェルスクリプトを書く | SOTA](http://deeeet.com/writing/2014/05/18/shell-template/)

* [Use the Unofficial Bash Strict Mode (Unless You Looove Debugging)](http://redsymbol.net/articles/unofficial-bash-strict-mode/)
  * デバッグをより厳密に行うための基準。
* [ShellCheck – shell script analysis tool](http://www.shellcheck.net/)
  * こわいくらいstrictなlint。

参考
----
* [何もしない組み込みコマンド ":" （コロン）の使い道 - Qiita](http://qiita.com/xtetsuji/items/381dc17241bda548045d?utm_source=Qiita%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=f3d57ffc4c-Qiita_newsletter_196_02_24_2016&utm_medium=email&utm_term=0_e44feaa081-f3d57ffc4c-32775537)
  * 引数に何を渡しても何もしない性質便利。
