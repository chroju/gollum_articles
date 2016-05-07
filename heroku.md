とりあえず初級的な注意事項等はこちら。

* [知っておきたい！Herokuを使う上では当たり前？の16の常識 | mah365](http://blog.mah-lab.com/2013/05/16/heroku-commons-16/)

What is heroku
----

* 古き良きPaaS環境。もともとはRails向けだったが現在はPythonやnode.jsなど様々な言語に対応。
* Gitに対応している。デプロイは`git push`でプラガブルに行える。
* 基本的な操作は[Heroku Toolbelt]()と呼ばれるCLIツールを通じて行う。

Heroku Toolbelt
----

```bash
# アプリの状態確認
$ heroku ps --app appname
# ログ確認
$ heroku logs --tail --app appname
```

how-to
----

### 変数をセットしたい

`heroku config`で環境変数を設定する。

* [[heroku] 環境変数の操作 - Qiita](http://qiita.com/satomyumi/items/18db3c97734f32ebdfde)