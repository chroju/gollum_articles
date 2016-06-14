[今更聞けないSubversionの使い方 - Qiita](http://qiita.com/mountcedar/items/e756bb9136e3b1722bb2)

コマンド体系はGitに似ている。

ファイルを指定し、特定リビジョンのものをリポジトリから反映する場合は`update`を使う。

```bash
$ svn update -r (revision) (filename)
```