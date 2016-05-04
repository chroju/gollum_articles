* サーバーサイドjs
* Web Server、サーバーサイドスクリプティングあたりが一緒になっている。
* 位置付けとしてはアプリケーションプラットフォーム。フレームワークとしてAngularJSやExpressが存在する。

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

パッケージを追加する場合は`--save`オプションを追加してインストールすることで、package.jsonに依存関係が書き込まれる。開発中のみ使用するパッケージは`--save-dev`とする。

```bash
$ npm install --save request
```

また`scripts`に実行スクリプトを記載しておくことで、`npm run`で実行が可能。

```bash
$ npm run
```

詳細は以下。

* [05 - Using a `package.json` | npm Documentation](https://docs.npmjs.com/getting-started/using-a-package.json)

other
========