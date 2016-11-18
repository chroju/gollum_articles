InnoDB関連
----

### 参考

* [MariaDB(MySQL) - 既存 InnoDB ファイルフォーマットを Antelope から Barracuda に変換！ - mk-mode BLOG](http://www.mk-mode.com/octopress/2015/07/15/mariadb-innodb-file-format-changing-to-barracuda/)
* [漢(オトコ)のコンピュータ道: InnoDB Pluginことはじめ。快適ストレージエンジン生活はじまる！](http://nippondanji.blogspot.jp/2010/03/innodb-plugin.html)

バッファの調整
----

高速化のためにバッファをある程度持たせることは必要だが、その他設定やリソース状況等も鑑みて適切な値をセットする必要がある。

### 参考

* [[ThinkIT] 第3回：max_connectionsとthread_cacheのチューニングを行う (1/3)](https://thinkit.co.jp/free/article/0707/2/3/)
* [漢(オトコ)のコンピュータ道: MySQLを高速化する10の方法](http://nippondanji.blogspot.jp/2009/02/mysql10.html)
* [[ThinkIT] 第6回：query_cache_sizeの違いによるパフォーマンス比較 (1/3)](https://thinkit.co.jp/free/article/0707/2/6/)
* [【はじめてのスレッドキャッシュ】MySQL チューニングしたいです！★MySQLTuner をきっかけに♪5 – oki2a24](http://oki2a24.com/2013/05/31/set-thread-cache-in-mysql/)