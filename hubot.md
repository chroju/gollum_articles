作成

```bash
$ npm install -g yo generator-hubot
$ mkdir yourbot
$ cd yourbot
$ yo hubot
# `hubot --create`はdeprecated。
```

起動

```bash
$ bin/hubot
```

構成

```bash
├── Procfile
├── README.md
├── bin/
├── external-scripts.json
├── hubot-scripts.json
├── node_modules/
├── package.json
└── scripts/
```

* `/bin/hubot`の起動オプションがProcfileで定義されている。
* scriptsフォルダに設置したcoffeescriptが自動的に読み込まれ使用される。
* node_moduleに配置したスクリプトで使用したいものは`external-scripts.json`にjson形式で記述する。
  追加インストールする場合は`npm install --save foo`で追加。package.jsonにも追加される。
  （このあたりはhubot特有というよりnpmの一般的な使い方）
* `hubot-scripts`というnode_moduleにもスクリプトが含まれている（node_modules/hubot-scripts/src/scripts）。
  これらを使用する場合は`hubot-scripts.json`にjson形式で記述する。

スクリプトの書き方
----

```coffee
module.exports = (robot) ->

  robot.respond /hello, I am (.*)/i, (msg) ->
    name = msg.match[1]
    msg.send "Hello #{name} !"

  robot.hear /bye/i (msg) ->
    msg.send "Byebye!"
```

heroku + slack
----

* [slackにHubotを導入(Heroku経由) - Qiita](http://qiita.com/acairojuni/items/dc4543aa5827d4c3211c)

Deployment
----

* GitHubにパッケージまるごとアップして、pullすればOK!って[公式に書いてる](https://hubot.github.com/docs/deploying/unix/)。
* 実際のところこれが一番楽である（コンテナ上げてその中でyoとかやってられない）。

こんなときは
----

### APIキーなど変数値を秘匿したい

環境変数を使って読み込む。

* [設定を読み込む Hubot スクリプトをつくろう - Qiita](http://qiita.com/bouzuya/items/d65a394cac9e76b56d3d)
