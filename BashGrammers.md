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

function
----

exception
----

packages
========

other
========