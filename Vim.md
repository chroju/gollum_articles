レジスタ
----

`+`レジスタはOSクリップボード。

tips
----

### 特殊文字入力

* 特殊文字は`<C-v>`に続けて目的のキーを押すことで入力する。
* 改行（^M）は`<C-v><C-m>`もしくはEnter。
  * [VIMで、行末の余分な改行コード（^M）をすべて取り除く - Qiita](http://qiita.com/rohinomiya/items/0521cc3a12048304f8fd)

### アクセント記号等の入力

* [vimでä、ö、ø、åのようにアクセント付き文字やリガチャを入力する方法：miukumaukuの開発ブログ：So-netブログ](http://suomen-kissa.blog.so-net.ne.jp/2015-03-05)

### 文字コード設定

* `set fileencoding|fenc` : カレントバッファのファイルの文字エンコーディング。
* `set fileencodings|fencs` : ファイル編集時に優先考慮する文字コードの設定。
* `set encoding|enc` : Vimの内部文字コード。UTF-8推奨。
* `:e ++enc=utf-8` : カレントバッファのファイルをUTF-8で開き直す。

### folding

* `zo` : 開く（`zO`ですべて開く）
* `zc` : 閉じる（`zC`ですべて閉じる）
* [fold - Vim日本語ドキュメント](http://vim-jp.org/vimdoc-ja/fold.html)