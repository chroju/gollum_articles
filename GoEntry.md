go入門
========

インストール
----
普通にtarをwgetして。homebrewであればレポジトリに入っている模様。

### 環境変数

なぜかわからないがバイナリの格納先が`/usr/local/go`を前提としており、PATHを通す必要がある。またgoのパッケージインストール先として`$GOPATH`を設定する必要がある。だいたいがホームディレクトリ配下に`go`もしくは`.go`を切っている模様。

```bash
$ export PATH=$PATH:/usr/local/go/bin
$ export GOPATH=$HOME/.go
```

* [build-web-application-with-golang/01.2.md at master · astaxie/build-web-application-with-golang](https://github.com/astaxie/build-web-application-with-golang/blob/master/ja/01.2.md)


ライブラリ
----

`go install`や`go get`で外部ライブラリを導入できる。

### glock

[GitHub - robfig/glock](https://github.com/robfig/glock)

依存しているGitHub上のライブラリ等を、バージョン固定するためのツール。

### go-bindata

[go-bindata でコンパイル時にリソースを埋め込んじゃおう！ - Qiita](http://qiita.com/ikawaha/items/c02d84cfd00f8f442500)

指定したリソースをバイナリ化できる。


コンパイル
----

かつてはビルドにMakefileを必要としたようだが。
[Goコードの書き方 - golang.jp](http://golang.jp/tag/go%E3%82%B3%E3%83%BC%E3%83%89%E3%81%AE%E6%9B%B8%E3%81%8D%E6%96%B9)

現状は`go build`や`go run`を使うことでMakefileは不要とできるらしい。

* [GoにMakefile要らないです - YAMAGUCHI::weblog](http://ymotongpoo.hatenablog.com/entry/2013/01/08/235618)
* [急いで学ぶGo lang#1 概要とセットアップ ｜ Developers.IO](http://dev.classmethod.jp/server-side/language/golang-1/)


参考
----

* [build-web-application-with-golang/01.3.md at master · astaxie/build-web-application-with-golang](https://github.com/astaxie/build-web-application-with-golang/blob/master/ja/01.3.md)
* [golang チートシート - Qiita](http://qiita.com/jca02266/items/56a4fb7b07b692a6bf34)