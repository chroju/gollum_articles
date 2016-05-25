* [[基礎文法|BashGrammers]]
* [[コーディングスタイル|BashCodingStyle]]
* [Qiitaに自分でまとめたやつ](http://qiita.com/chroju/items/7af3fd5faa26de4067f0)

配列
----

```bash
# 宣言
$ array=(foo bar baz)
# 要素へのアクセス
$ array[1]=hoge
$ echo ${array[@]}
foo hoge baz
# 要素数を確認
$ echo ${#array}
3
# 添字指定がなければ[0]へのアクセスになる
$ echo ${array}
foo
```

コマンド
----

### \[\[ \]\]（二重ブラケット）

`test`コマンド（`[]`）よりインテリジェントに振る舞う上位互換という考えでよい？ 正規表現が使えたり。

[Linux のヒント: Bash のテスト関数と比較関数](http://www.ibm.com/developerworks/jp/linux/library/l-bash-test.html)

比較の演算子は下記がとても詳しい。

[if 文と test コマンド | UNIX & Linux コマンド・シェルスクリプト リファレンス](http://shellscript.sunone.me/if_and_test.html#%E6%96%87%E5%AD%97%E5%88%971%E3%81%A8%E6%96%87%E5%AD%97%E5%88%972%E3%81%AF%E7%AD%89%E3%81%97%E3%81%84%E3%81%8B:ed775c34e441eb16a91481d087cc1a74)

ループ
----

### for

`in`を利用した範囲指定のループが可能。

```bash
for i in 0 1 2 3
do
  echo $i
done

for i in ${array[@]}
do
  echo $i
done
```

### while

`read`と組み合わせて標準入力から1行ずつ読み込んで処理する。

```bash
while read i; do
  echo $i
done < input.txt
```

算術展開
----

`$(( x += 1 ))`で変数xがインクリメントされる。


ShellScript
----

### 関数

* `function name(){}`形式で宣言する（functionは省略可）。
* 関数は呼び出す前に定義する必要がある。
* 呼び出すときは関数名を記述するのみで良い。
* 返り値という概念はない。標準出力がそのまま戻ってくる。`return`で設定できるのは終了コード。`exit`するとスクリプト自体が終了するので注意。
* ローカル変数は`local var`形式で宣言できる。関数外（グローバルスコープ）と干渉しない。
* 引数も設定でき、`$1`などで呼び出せる。ただし`$0`はグローバルスコープ。

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
