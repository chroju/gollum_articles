基礎文法
----

### 前提

* 行末は`;`。
* 偽値は未定義（undef）、空文字列、数値及び文字列の0、空リストのみ。
* Coding Gide: [perlstyle - perldoc.perl.org](http://perldoc.perl.org/perlstyle.html)

### 演算子

* `.` : 文字列連結
* 比較演算子が数値と文字列で異なるので注意。
  数値は`==`, `!=`などの記号を使用、文字列は`eq`や`ne`による比較をする。

### 変数

* 変数の接頭辞によりスカラ変数、配列変数、ハッシュ変数となる。
  * `$num = 1;` : スカラ変数。単一の値が入る。
  * `@array = (1, 2, 'a');` : 配列変数。配列が入る。
  * `%hash = ('key1', 1, 'key2', 2);` : ハッシュ変数。ハッシュが入る。内部的には配列と等価らしい。
  * 呼び出すときはいずれも`$`になる（`$array[0]`, `$hash('key1')`）。
* スコープは`my`, `local`, `our`が使える。
  * [[Perl] my と local と our の違いについて - TAKESAKOのはてな出張所](http://d.hatena.ne.jp/TAKESAKO/20080110/1199969773)
* リファレンス
  * [リファレンス | Smart](http://rfs.jp/sb/perl/02/10.html)

### 特殊変数

* `$_` : 期待される変数として振る舞うらしい。`foreach`の中で使えばその時点での要素が入る。
  * スコープに注意→ [whileでファイルハンドルをループする時の暗黙の$_について - Unknown::Programming](http://d.hatena.ne.jp/fbis/20071225/1198554886)
* `@_` : サブルーチンに渡された引数すべてを配列で引き受けている。
* `$@` : 直前の`eval`で発せられた例外メッセージを引き受ける。
* `$$` : プロセスのPID。

#### 参考

* [第7回　新人さんのための仕事で使えるPerl基礎知識（2）：Perl Hackers Hub｜gihyo.jp … 技術評論社](http://gihyo.jp/dev/serial/01/perl-hackers-hub/000702)
* [perlの特殊変数一覧](http://www.ksknet.net/perl/perl_10.html)

### 引数

* `shift`で第一引数から順に取り出せる。もしくは`@_`を使う。
* 関数定義で明示的に引数を定義する必要はない。

```perl
sub foo {
  my $bar = shift;
  my $baz = shift;
}
```

### 型

#### 文字列

[文字列 | Perl 文字の置換、文字の切り取り、文字の検索](http://bi.biopapyrus.net/perl/syntax/strmanu.html)

### 繰り返し

#### for

```perl
for ($count = 1; $count < 5; $count++){
    print "\$count = $count\n";
}
```

#### foreach

* リスト内の要素を1つずつ取り出して処理する。
* ループ回数のカウントを参照できるような特殊変数はないので、やりたい場合は変数を設けてカウントするしかない。

```perl
my @array = ("foo", "bar", "baz");
foreach my $a (@array) {
  print "$a\n";
}
```

#### 繰り返しからの脱出

* `last` : `break`にあたる。
* `next` : `continue`にあたる。

### IO

* `open(handle, filename)` : ファイルオープン。`handle`はファイルの内容を示し、大文字で`FH`や`DAT`などとする慣例。
　　`filename`は頭に`>> filename`とすると追記など指定でき、何もなければ読み込みになる。
* `seek(handle, offset, begin)` : ファイル読み込み。`begin`が0で先頭、2で末尾、1で現在位置。`offset`バイト分読み込む。
* `tell(handle)` : ファイルポインタの現在位置を返す。
* `close(handle)` : ファイルクローズ。

関数
----

### chomp / chop

* 末尾の文字を削除。`chomp`は改行文字に限定して削除する。

### sleep

* `sleep 5;`で5秒停止。

### grep

* 配列から条件に一致する要素だけを抜き出す。
* [Perlで、ある要素が配列(リスト)の中に存在するかを調べる方法 · DQNEO起業日記](http://dqn.sakusakutto.jp/2011/08/perl_10.html)

```perl
my @result = grep{ $_ eq "hoge" } @array
```

### sprintf

* 文字列を指定したフォーマットで返す。
* 参照：[Perl - 関数 - sprintf](http://www.loose-info.com/main/memolist/perl/fnc_sprintf.html)

### defined

* 定義済みであれば真。

### pack(template, list)

* 値をバイナリ化する。
* `list`を`template`で指定した形式に従って解釈する。

### gethostbyaddr(ip, 2)

* IPからホスト名を返す。
* IPはバイナリで与える。`pack`でバイナリ化を行う。
* 参照：[ホスト名を知る 'PERL-LABO'](http://www.perl-labo.org/analyse/host/)

ライブラリ
----

* `Config::Simple`
* `Config::Tiny` : iniファイルの読み取りに便利。

### ライブラリが見つからないとき (Can't locate *.pm in @INC)

yumの`provides`コマンドで必要なパッケージを確認する。

```bash
$ yum provides '*Sys/Syslog.pm'
...
perl-Sys-Syslog-0.33-3.el7.x86_64 : Perl interface to the UNIX syslog(3) calls
リポジトリー        : base
一致          :
ファイル名    : /usr/lib64/perl5/vendor_perl/Sys/Syslog.pm
```

 