FHS (Filesystem Hierarchy Standard)
========

Linux及びUNIX系OSの主なディレクトリ構造を定めたもの。各ベンダーが参画し、Linux Foundationが保守管理している。

/etc
----

### /etc/security/limits.conf

ユーザーごとのプロセス数、ファイルディスクリプタ数の上限を定めることができる。

### /etc/profile.d/

bashの読み込む環境設定ファイルが置かれている。bashがログインシェルとして起動されると、まずシステム全体用の起動ファイルとして`/etc/profile`を読み込む。これには`/etc/profile.d/*`の各ファイルを読み込むようコマンドが定義されている。`/etc/profile.d/`には基本として各ミドルウェア等が自動でファイルを配置しており、環境変数の必要な設定等を行なっている。