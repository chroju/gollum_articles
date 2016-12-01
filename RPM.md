RedHat Package Manager。

rpmとyum
----

* 参照：[初心者の頃に知っておきたかった rpm と yum の違いと使い分け - 彼女からは、おいちゃんと呼ばれています](http://blog.inouetakuya.info/entry/20111006/1317900802)
* RPMが基本のパッケージ管理。yumがそれをより使いやすくしてくれてるというイメージで良さそう。
* RPMは愚直に指定したURL、ファイルパスに存在するパッケージファイル（foo.rpm）をインストールしてくれる。依存関係の解決もしないし、ウェブ上のリポジトリを見に行って検索してくれたりもしない。
* yumは未インストールパッケージをウェブのリポジトリで検索し、フルパスではなくサービス名やツール名を与えるだけでインストールできる。自動更新といった機能も賄う。
* じゃあRPM要らなさそうだけど、ローカルからRPMファイルを持って行ってインストールする場合などは利用する。この形式だと勝手に依存関係で余計なものが入ったりしないので、strictな運用向き。

yum
----

```bash
# 依存関係の確認
$ yum deplist package
# ローカルのrpmをインストール（依存関係解決をしてくれる点でメリットあり）
$ yum localinstall rpm
```

rpm
----

```bash
# インストール
$ rpm -ivh package
# アップデート
$ rpm -Uvh package
# パッケージ情報の表示
$ rpm- iq package
# インストール済みの全パッケージを検索
$ rpm -qa
# コマンドが属しているパッケージを検索
$ rpm -qf command
# アンインストール
$ rpm -e package
```

* changelog確認用のオプションが存在する。

```bash
$ rpm -q --changelog glibc
```

srpm
----

RPMパッケージを作成できるソースのパッケージ。拡張子が`.src.rpm`で提供される。`rpmbuild --rebuild`コマンドにより直接インストールするか、一旦`rpm -ivh`コマンドでソースコードを展開し、`/usr/src/redhat/SOURCES`内のソースコード、同一階層の`SPEC`ディレクトリ内のspecファイルを編集してパッケージの作成方法を調整できる。

* [SRPMを使ったパッケージのインストール - tetsuyai’s blog](http://tetsuyai.hatenablog.com/entry/20120106/1325839318)