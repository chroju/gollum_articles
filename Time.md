[Time](https://unix4lyfe.org/time/?v=1)

* 各種用語の解説と時間の取り扱いに関する基本原則の記載。
* UNIXTimeを使え。時刻を保存するときにローカルタイムを使うな。MySQLもDATETIMEではなくUNIXTIMEを使うこと。
* Slewモードが望ましい。
* システムクロックはズレる。ネットワーク上ならそれぞれがズレているという前提に立たねばならない。
* 悩ましき閏秒対応。ntpdではleapfileに閏秒に関して記載できる。Googleの記事も参照。
  [Official Google Blog: Time, technology and leaping seconds](https://googleblog.blogspot.jp/2011/09/time-technology-and-leaping-seconds.html)