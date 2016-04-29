活用
----

### submodule

* `git submodule`
  * レポジトリ内に別のレポジトリを内包させる。
  * 各レポジトリは別々のバージョン管理となるので、外側のレポジトリで例えば`reset`をしても、内側のレポジトリには干渉しない。
  * 参考：[Git submodule の基礎 - Qiita](http://qiita.com/sotarok/items/0d525e568a6088f6f6bb)

教訓
----

* [Git pullを使うべきでない３つの理由 · DQNEO起業日記](http://dqn.sakusakutto.jp/2012/11/git_pull.html)

修正
----

### commitの取り消し

* `git revert`
  * 与えたコミットIDにおける修正を相殺するようなコミットを生成する。
  * 従って過去の`commit`履歴が消えるわけではない。
  * `merge`の相殺を行う場合、基準とするのが本線のブランチであれば`-m 1`、支線であれば`-m 2`オプションを付ける。
  * `--no-commit`でコミットを行わず相殺分の生成だけを行う。
  * 参考：[Git で コミットを無かったことにする方法 （git revert の使い方） - akiyoko blog](http://akiyoko.hatenablog.jp/entry/2014/08/21/220255)