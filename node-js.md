* サーバーサイドjs
* Web Server、サーバーサイドスクリプティングあたりが一緒になっている。
* 位置付けとしてはアプリケーションプラットフォーム。フレームワークとしてAngularJSやExpressが存在する。
* [[チートシート|NodeJsCheatSheet]]

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

非同期
========

Node.jsでは非同期の関数が多い模様。非同期関数の結果を引き渡し、後続で処理を実行させる仕組みが **コールバック** 。Node.jsはシングルスレッドなので、非同期関数が呼ばれるとすぐに`undefined`を返して関数は一時停止し、呼び出し元の処理が終わったあとで非同期関数の実処理を実行、その後コールバックへと流れる。

* 参照：[はじめてのNode.js：Node.jsのイベントシステムを知る 2ページ | OSDN Magazine](https://osdn.jp/magazine/13/03/18/0939236/2)

コールバック地獄
----

複数の関数を連続して実行させようとすると、コールバックが連続してネストしていくので、視認性が悪くなる。俗に「コールバック地獄」と呼ぶ。

* 参照：[Node.jsでコールバック関数を書く - Qiita](http://qiita.com/Hitsuji/items/2f70405ed7f0442ea4be)

async
----

パラレル処理や連続処理を実現する。非同期処理の同期的対応のためのモジュール。

* [caolan/async: Async utilities for node and the browser](https://github.com/caolan/async)
* [JavaScriptのasync.jsでwaterfallとseries、parallelの違い - Qiita](http://qiita.com/takeharu/items/84ffbee23b8edcbb2e21)
* [Node.jsではforEachでなくasync.eachを使おう - Qiita](http://qiita.com/ishisak@github/items/cee2811a5a131d4ef946)

Promise
----

効果としてはほぼasyncと同等だが、ECMA6で取り入れられている標準機能。

* [Node.jsエンジニアなら2014年内に知っておきたいPromise入門 | Tokyo Otaku Mode Blog](http://blog.otakumode.com/2014/09/17/nodejs-promise/)
* [今更だけどPromise入門 - Qiita](http://qiita.com/koki_cheese/items/c559da338a3d307c9d88)
* [CoffeeScriptでasyncとpromise - Qiita](http://qiita.com/ksato9700/items/73b2861595c2829e06f1#%E3%81%AF%E3%81%98%E3%82%81%E3%81%AB)

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

package
----

### protractor

AngularJS用のテストフレームワークらしい。ウェブブラウザのユーザーアクションを再現してテストを行う。その性質からスクレイピングにも利用可能。

* [AngularJS用テストフレームワーク「Protractor」チュートリアル日本語訳 - Qiita](http://qiita.com/weed/items/30098f7be2f753580f63)

### selenium-webdriver

同様にウェブブラウザのテストフレームワーク。

* [selenium/javascript/node/selenium-webdriver at master · SeleniumHQ/selenium](https://github.com/SeleniumHQ/selenium/tree/master/javascript/node/selenium-webdriver)

other
========