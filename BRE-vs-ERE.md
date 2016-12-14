参照：[どのUNIXコマンドでも使える正規表現 - Qiita](http://qiita.com/richmikan@github/items/b6fb641e5b2b9af3522e)

* あくまでPOSIX目線。
* sedがBREである、awkがEREなんだけど独自のサブセットであるというのが微妙。
* EREで`+`や`|`が使えないというあたりもわりと盲点。
  * GNU版のsedだとこれらはバッククォートでエスケープすれば使えるらしい。ただしBSD版はダメ。あー。