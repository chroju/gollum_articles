地域設定。しばしば設定不備によりエラーが出る場合がある。以下がよくまとまっている。

[ロケール（locale）まとめ - Qiita](http://qiita.com/aosho235/items/58e2e7acd5c2ee3641ff)

設定が正しいはずなのにロケールがおかしい場合は、ssh時の`SendEnv`設定により、ローカルホストのロケール情報が反映されている可能性もあり。

[SSH接続時のLANG設定がOS設定値と異なる時の対処方法 ｜ Developers.IO](http://dev.classmethod.jp/server-side/os/changed-lang-by-ssh/)