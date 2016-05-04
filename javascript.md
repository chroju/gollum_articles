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

exception
----

packages
========

other
========

* `use strict;`宣言で厳格な文法チェックを行う。