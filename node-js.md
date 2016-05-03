feature
========

install
========

Mac
----

自分がやった時点ではnode.jsを入れればnpmも一緒に入った。

```bash
$ brew install node
```

yum
----

```bash
$ yum install nodejs npm
```

running
========

variables
========

definition
----

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

if
----

### true/false

### post if

### ternary operator

switch
----

loop
----

function
----

exception
----

packages
========

`npm`を用いる。node.jsとは別でインストールしておく。

usage
----

### パッケージのインストール

```bash
# グローバル
$ npm install foo -g
# ローカル（同一階層のnode_modulesフォルダに入る）
$ npm install foo
```

### npm自体のアップデート

```bash
$ npm install npm -g
```

### package.json

package.jsonファイルに必要なパッケージを記載しておき、同一ディレクトリ上で`npm install`することでローカルインストールできる。`package.json`は`npm init`コマンドでテンプレートが生成できる。

```bash
$ npm init
```

詳細は以下。

* [05 - Using a `package.json` | npm Documentation](https://docs.npmjs.com/getting-started/using-a-package.json)

other
========