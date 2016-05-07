feature
========

install
========

素のjsに関しては特に不要。coffee-scriptはnpmで。

```bash
$ npm install -g coffee-script
```

running
========

variables
========

jsは必要。coffee-scriptは不要。

```js
var foo = 0;
```

definition
----

string
----

```js
// 文字列マッチング比較
if ( str.match(/foo/) ) {

}
```

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

`//`もしくは`/* */`

operator
----

* 同値比較は`===`。`==`は使いドコロが難しい感じ。

input/output
----

* デバッグ的には`console.log`を使う。

```js
if (err) {
  console.log(err);
}
```

if
----

js

```js
if ( i > 0 ) {
  ... ;
} else if ( i == 0 ) {
  ... ;
} else {
  ... ;
}
```

coffeeでは括弧類が不要になる。

```coffee
if i > 0
  ...
else if i == 0
  ...
else
  ...
```

### true/false

### post if

### ternary operator

coffeeでは存在しない。jsでは以下。

```js
x = flag ? 1 : 0;
```

switch
----

loop
----

coffee

```coffee
for i in [1 .. 10]
  console.log "Hello! #{i}"
```

function
----

js

```js
function foo(a, b) {
  return a * b;
}
# 無名関数
var bar = function(c) { return c + c };
```

coffee

```coffee
foo = (a, b) ->
  a * b

bar = (c) ->
  c + c
```

exception
----

packages
========

other
========

* `use strict;`宣言で厳格な文法チェックを行う。