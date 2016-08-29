```bash
# 実行コマンドを明示する。
$ find *.txt | xargs -t rm
# 1回あたり引数を2つずつ渡す
$ find *.txt | xargs -n 2 rm
# コマンドの実行前に確認する
$ find *.txt | xargs -p rm
# 標準入力の値を任意の位置で引数とする
# -iでも同様のことが可能だが、POSIXから外されたため非推奨
$ find *.txt | xargs -I{} mv {} /tmp/
```