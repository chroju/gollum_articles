## 設定

* `getenforce`コマンドで状態確認可能。
  * `disabled` : 無効。
  * `enforcing` : 有効。
  * `permissive` : 有効だが監査ログに警告を書き込むのみの動作。
* `/etc/selinux/config`の`SELINUX`で起動時の状態を設定する。
* `enforcing`と`permissive`の間は`setenforce (0|1)`コマンドにより動的に切替ができる。