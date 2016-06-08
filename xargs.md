```bash
# 実行コマンドを明示する。
$ find *.txt | xargs -t rm
# 1回あたり引数を2つずつ渡す
$ find *.txt | xargs -n 2 rm
# コマンドの実行前に確認する
$ find *.txt | xargs -p rm
# 標準入力の値を任意の位置で引数とする
$ find *.txt | xargs mv {} /tmp/
```