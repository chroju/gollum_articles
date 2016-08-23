[参照の局所性 - Wikipedia](https://ja.wikipedia.org/wiki/%E5%8F%82%E7%85%A7%E3%81%AE%E5%B1%80%E6%89%80%E6%80%A7)

## 非同期

呼び出し先のIOや関数の終了を待たずに呼び出し元が終了するような処理。呼び出し先と呼び出し元が同期せずに処理を進めるので「非同期」。同期することでIO待ちがボトルネックになることを防ぎ、高速化を図る処置。例えばNode.jsはjsにおけるIO待ち解消のために非同期処理を取り入れている。

* [非同期処理ってどういうこと？JavaScriptで一から学ぶ - Qiita](http://qiita.com/kiyodori/items/da434d169755cbb20447)

## クロージャ

関数の中で呼び出された内部関数が、外部関数の変数等へのアクセスは可能である一方、外部関数からのアクセスは防ぐような機構。javascriptの機能のひとつ。

* [なぜクロージャ（Closure）と言うのか？ - Qiita](http://qiita.com/mochizukikotaro/items/7403835a0dbb00ea71ae)