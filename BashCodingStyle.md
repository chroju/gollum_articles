## 全体

* shebangは`/bin/bash`とする。`/bin/sh`は使わない。
  
* 簡潔なDescriptionを冒頭、各関数に記載する。詳細は`usage`に入れるので省略。
* コマンドは可能な限り絶対パスで指定する。

## 変数

* `readonly`や`local`を活用する。
* 変数展開（`${var:-word}`で`var`が定義されていない場合に「word」を返せる、等）を活用する。
* ハードコーディングが相応しくない変数はでの入力、環境変数での定義、confファイルの別出しといった手段を取る。

```bash
readonly CONF_FILE="$(dirname ${0})/foo.conf"
if [[ -f ${CONF_FILE} ]]; then
  source ${CONF_FILE}
fi

if [[ -z ${REQUIRED} ]]; then
  stty -echo # 入力値を表示したくない場合
  printf "Please input: "
  read REQUIRED
  stty echo
fi
```

## ログ

* 汎用性を持たせるため、独自のログファイルは定義せず、標準出力と標準エラー出力、`logger`を利用する。
* 特にcron実行するようなスクリプトは、実行ログを`logger`で残す。
* 標準エラー出力へのロギングは予め関数を定義しておく。

```bash
error() {
  logger -isp local0.error "$@"
}
```

## 汎用書式

コマンド名は`usage`やログの中でよく使用するので、予め定数で定義しておく。

```bash
readonly COMMAND_NAME=$(basename ${0})
```

`usage`及び`version`は必須とする。

```bash
usage() {
  cat <<EOF
${COMMAND_NAME} - xxx script

Usage: ${COMMAND_NAME} [-ab] -p foo [-s var] [FILE] ...

Options:
  -a    ....
  -b    ....
  -p    ....
  -s    ....

Examples:
  ${COMMAND_NAME} ...

EOF
}

version() {
  cat <<EOF
${COMMAND_NAME} v1.0
Copyright (C) 2016 chroju

EOF
}
```

## 文字色

* 文字色を効果的に用いる。
* 背景色は視認性が下がる場合も多く、装飾の手間も大きいので使わない。
* 文字色定義用の変数を予め宣言して利用する。

```bash
readonly RED=\e[31m
readonly GREEN=\e[32m
readonly COLOR_F=\e[m
...
echo -e "${GREEN}OK${COLOR_F}"
```

## オプション処理

* `getopts`や`getopt`を活用したいところだが、諸々制約があって柔軟性に欠けるのでDIYする。対応したいのはロングオプション、引数を取るオプション。
* 引数を取った場合は、別途validateを必ず行う。

```bash
while [[ $# -gt 0 ]]; do
  case "${1}" in
    --file | -f )
      FILE_PATH="${2}"
      shift
      ;;
    --help | -h )
      usage()
      ;;
    --version | -v )
      version()
      ;;
    -- )
      shift
      break
      ;;
    -* )
      echo "[ERROR] invalid option "${1}"" >&2
      usage()
      exit 1
      ;;
  esac

  shift
done
```

## 例外処理

`trap`による例外処理を活用する。

```bash
# 一時ファイル作成
ls -la > /tmp/file_list.txt
# メイン処理関数を呼び出し
main_function
# 一時ファイル削除してexit
rm /tmp/file_list.txt
exit 0

# スクリプトが異常終了した、シグナルで終了した場合も一時ファイル削除
trap "rm /tmp/file_list.txt" 1 2 3 15 ERR
```

## コーディングスタイル

* インデントはスペース2つ。
* 環境変数、定数は大文字スネークケース。（ex: `readonly FOO_BAR='foobar'`)
* 関数名は小文字スネークケース。
* 変数の参照は`${foo}`の形を用いる。さらにユーザー入力値はクォートして`"${1}"`とする。
* コマンド展開は`$(command)`。

### 関数

* 宣言時に`function`は省略する。
* 呼び出す際は`()`を付ける。
* `return`で終了コードを返す際は、0～125の範囲とするよう留意する。

```bash
sample() {
  ...
  return 1
}

sample()
```

### if

* `if`～`then`を1行に収める。
* `test`には高機能版である二重ブラケット（`[[]]`）を用いる。

```bash
if [[ "$1" == "sample" ]]; then
  echo "true"
fi
```

### for

* `for`～`do`を1行に収める。

```bash
for i in 1 2 3; do
  echo "$i"
done
```

## デバッグ

### strictにする

以下を冒頭で宣言する。

```bash
set -euo pipefail
IFS=$'\n\t'
```

* `set -e`で0以外のリターンコードが発生すると即座にスクリプトが終了するようになる。
* `set -u`で未定義の変数（ケース違いを含む）を呼び出すとエラーとして扱われるようになる。
* `set -o pipefail`で、パイプを使った際に最後のコマンド以外で出た0以外の終了コードが返るようになる。
* `IFS`、bashにおけるセパレーターが事前に書き換えられている可能性に備え、デフォルト値に戻しておく。
* これらはいずれもかなり厳密さを求める定義なので、要不要は定義判断する。

### set -x

基本的なデバッグには`set -x`を用いる。

## その他

* 対話式の入力は可能な限り行わない（別のツールとの連携時に`expect`が必要になったり、汎用性が下がる）。
  * どうしても必要となる場合は`select`を使うなど、入力の簡素化を図る。
* 一時ファイルの生成が必要になる場合は`mktemp`を使用する。
* ファイルパス、環境変数といったユーザー環境の固有値に頼らない。


## 参考

* [Shell Style Guide](https://google.github.io/styleguide/shell.xml)
* [使いやすいシェルスクリプトを書く | SOTA](http://deeeet.com/writing/2014/05/18/shell-template/)
* [Use the Unofficial Bash Strict Mode (Unless You Looove Debugging)](http://redsymbol.net/articles/unofficial-bash-strict-mode/)
* [O'Reilly Japan - 詳解 シェルスクリプト](https://www.oreilly.co.jp/books/4873112672/)
