作成

```bash
$ mkdir yourbot
$ cd yourbot
$ yo yourbot
```

起動

```bash
$ bin/hubot
```

構成

```bash
├── Procfile
├── README.md
├── bin
├── external-scripts.json
├── hubot-scripts.json
├── node_modules
├── package.json
└── scripts
```

scriptsフォルダに設置したcoffeescriptが自動的に読み込まれ使用される。追加インストールする場合は`npm install --save foo`で追加。

こんなときは
----

### APIキーなど変数値を秘匿したい

環境変数を使って読み込む。

* [設定を読み込む Hubot スクリプトをつくろう - Qiita](http://qiita.com/bouzuya/items/d65a394cac9e76b56d3d)