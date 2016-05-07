とりあえず初級的な注意事項等はこちら。

* [知っておきたい！Herokuを使う上では当たり前？の16の常識 | mah365](http://blog.mah-lab.com/2013/05/16/heroku-commons-16/)

What is heroku
----

* 古き良きPaaS環境。もともとはRails向けだったが現在はPythonやnode.jsなど様々な言語に対応。
* Gitに対応している。デプロイは`git push`でプラガブルに行える。従ってSSH鍵の登録も必要になる。
* 基本的な操作は[Heroku Toolbelt]()と呼ばれるCLIツールを通じて行う。

Heroku Toolbelt
----

```bash
# アプリの状態確認
$ heroku ps --app appname
# ログ確認
$ heroku logs --tail --app appname
# 再起動
$ heroku restart web.1
```

課金
----

結構無料利用枠が厳しくなったのと、クレジットカード登録必須で課金条件満たすといきなり課金されるのとで、このあたりはシビアになるべき。

* 24時間中6時間はスリープにしてなくてはならない。 => heroku schedulerを使う
* 30分動作がないと自動でスリープする。

### サーバー数の最小化

```bash
$ heroku ps:scale web=1
```

how-to
----

### 変数をセットしたい

`heroku config`で環境変数を設定する。要は相手はLinuxなので、`TZ`でタイムゾーン設定をするといったこともできる。

* [[heroku] 環境変数の操作 - Qiita](http://qiita.com/satomyumi/items/18db3c97734f32ebdfde)
* [Herokuのタイムゾーンを日本時間に設定する - アインシュタインの電話番号](http://blog.ruedap.com/2011/02/10/heroku-timezone-japan-jst)

### デプロイ完了を確認したい

* [Heroku へのデプロイが完了したことを Hubot に通知する - ちなみに](http://sixeight.hatenablog.com/entry/2015/02/25/200751)

### CircleCIでherokuで自動デプロイしたい

公式で対応している。

* [Continuous Deployment with Heroku - CircleCI](https://circleci.com/docs/continuous-deployment-with-heroku/)