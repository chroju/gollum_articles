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

* `$0` : スクリプト名。
* `$$` : スクリプトのプロセスID。
* `$#` : 引数の数。応用で`${#foo}`はfoo変数の文字数。
* `$@` : 全引数の展開。

string
----

numeric
----

array
----

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

exception
----

packages
========

other
========