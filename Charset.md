文字コードについて。

個々の文字コード
========

CP932
----

曲者の印象。一般に言われるCP932はSJISにWindowsの文字拡張が入ったWindows_31Jを指す。これとユニコードの変換表がSJISのそれとずれているらしく、問題を起こすことがある。

* [本当は怖くないCP932 - Qiita](http://qiita.com/kasei-san/items/cfb993786153231e5413)
* [CP932変換表の問題が顕在化する例 - yanok.net](http://yanok.net/2011/06/cp932.html)

文字コードを扱う
========

変換
----

### iconv

```bash
$ iconv -f SJIS -t UTF-8 file
```

### nkf

```bash
# eucに変換
$ nkf -e file > changed.file
# SJISに変換
$ nkf -s file > changed.file
# UTF-8に変換
$ nkf -w file > changed.file
```

### Vim

[[Vim]]を参照。