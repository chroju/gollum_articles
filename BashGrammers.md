bashチートシート
========

feature
========

install
========

* だいたいデフォルトで入ってる。

running
========

variables
========

definition
----

special variables
----

特殊変数でよく使うもの。

* `$0` : スクリプト名。
* `$$` : スクリプトのプロセスID。
* `$#` : 引数の数。応用で`${#foo}`はfoo変数の文字数。
* `$@` : 全引数の展開。

変数展開時の演算子。変数の初期化に使える。

* `${var:-word}` : var変数が存在し、かつnullではない場合はその値を返し、それ以外の場合はwordを返す。
* `${var:=word}` : var変数が存在し、かつnullではない場合はその値を返し、それ以外の場合はvarにwordを代入する。
* `${var:+word}` : var変数が存在し、かつnullではない場合はその値を返し、それ以外の場合はnullを返す。

string
----

numeric
----

array
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


list
----

grammer
========

commnt
----

input/output
----

### ヒアドキュメント

* `<<_EOF_``の形で終了文字を指定し、標準入力として渡す。
* 終了文字はインデントできない。インデントしたい場合は`<<-_EOF_`とする必要がある。
* ヒアドキュメント中の変数等は展開されるため、展開したくない場合は終了文字を`<<'EOF'`とクォートする。

if
----

### \[\[ \]\]（二重ブラケット）

`test`コマンド（`[]`）よりインテリジェントに振る舞う上位互換という考えでよい？ 正規表現が使えたり。

[Linux のヒント: Bash のテスト関数と比較関数](http://www.ibm.com/developerworks/jp/linux/library/l-bash-test.html)

比較の演算子は下記がとても詳しい。

[if 文と test コマンド | UNIX & Linux コマンド・シェルスクリプト リファレンス](http://shellscript.sunone.me/if_and_test.html#%E6%96%87%E5%AD%97%E5%88%971%E3%81%A8%E6%96%87%E5%AD%97%E5%88%972%E3%81%AF%E7%AD%89%E3%81%97%E3%81%84%E3%81%8B:ed775c34e441eb16a91481d087cc1a74)

### true/false

### post if

### ternary operator

switch
----
```bash
case num in
  1 )
    echo "one"
    ;;
  2 )
    echo "two"
    ;;
  * )
    echo "other number"
    ;;
esac
```

loop
----

### for

```bash
for i in foo bar
do
  echo "${i}"
done
```

* インクリメントする整数を使用する場合、様々な記法がある。
  * ブレース展開を用いる : `for i in {1..10}`
  * seqコマンドを用いる : `for i in $(seq 1 10)`
* 配列の要素を1つずつ取り出す場合は`for i in ${array[@]}`。

### while

```bash
while read line; do
        echo $line
done < hoge.conf
```

function
----

* `function name(){}`形式で宣言する（functionは省略可）。
* 関数は呼び出す前に定義する必要がある。
* 呼び出すときは関数名を記述するのみで良い。
* 返り値という概念はない。標準出力がそのまま戻ってくる。`return`で設定できるのは終了コード。`exit`するとスクリプト自体が終了するので注意。
* ローカル変数は`local var`形式で宣言できる。関数外（グローバルスコープ）と干渉しない。
* 引数も設定でき、`$1`などで呼び出せる。ただし`$0`はグローバルスコープ。

exception
----

packages
========

other
========

算術展開
----

`$(( x += 1 ))`で変数xがインクリメントされる。
