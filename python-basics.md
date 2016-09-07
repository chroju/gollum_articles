Python基本文法
========

feature
========

install
========

* だいたいパッケージで入るが、2と3があると思うのでバージョン指定した方がよい。

running
========

variables
========

definition
----

special variables
----


string
----

* word[:2] 最初の2文字
* word[2:] 最初の2文字を取った残り
* word[2:4] 最初の4文字から2文字を取った残り
* word[2] 最初から2文字目（1文字目が0）
* word[-2] 最後から2文字目
* word[-2:] 最後の2文字を取った残り

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


if
----

### true/false

### post if

存在しない。下記の三項演算子が後置if的な形になる。

### ternary operator

以下2つは等価。

```py
if n == 10:
    x = "OK"
else :
    x = "NG"
```
```py
x = "OK" if n == 10 else "NG"
```

switch
----

loop
----

### for

* 条件文最後に`:`が必要
* 2行目以降はインデント

function
----

```python
def foo(bar, baz):
    ...
```

exception
----

packages
========

other
========
