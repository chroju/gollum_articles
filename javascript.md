coffeeとjsの比較は以下参照。

* [CoffeeScript入門（前編） ― CoffeeScriptの基本構文 - Build Insider](http://www.buildinsider.net/web/rubyonrails4/0901)
* [CoffeeScript入門（後編） ― 関数／オブジェクト指向構文／即時関数 - Build Insider](http://www.buildinsider.net/web/rubyonrails4/0902)

coffeeのデバッグ

```bash
$ cat foo.coffee | coffee -s
```

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
// regexp
if ( /foo/.exec("foo") ) {

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

jsは`//`もしくは`/* */`。coffeeは`#`か`### ###`。

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

* `false`は"", 0, undefined, false, null

### post if

### ternary operator

coffeeでは存在しない。jsでは以下。

```js
x = flag ? 1 : 0;
```

switch
----

```js
switch (foo) {
  case 0: console.log("0"); break;
  case 1: console.log("1"); break;
  case 0: console.log("2"); break;
  default: console.log("other");
}
```

loop
----

coffeeではオブジェクトからのループは`for of`になる。

```coffee
for i in [1 .. 10]
  console.log "Hello! #{i}"

for key, val of json
  console.log(key, val)
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