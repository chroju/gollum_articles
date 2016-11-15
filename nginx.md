* Webサーバー。
* Preforkで動くApacheと比較すると、イベント駆動で展開するため使用リソースが少なく、軽量である（シングルプロセスで動作する）。
  * C10K問題（マルチプロセス型で、クライアント数の急増によりプロセス上限に達する問題）への対応。
  * シングルプロセス内で、イベントループによりリクエストを処理していく。従って待ち行列を滞留させるCPUを使うような処理には不向き。
* リバースプロキシとしての機能を備えている。
  * 上述のCPUを使う処理はアプリケーションサーバー（Unicorn等）に飛ばして処理。

参考
----

* [Nginxが支持される理由と特徴：新刊ピックアップ｜技術評論社](http://gihyo.jp/book/pickup/2015/0075)
* [入門！ nginx - tumblr](http://shim0mura.hatenadiary.jp/entry/20120110/1326198429)

nginx.conf
----

### upstream

* いわゆるリバースプロキシの設定。
* `proxy_pass`等で参照されるサーバーグループの設定を書く。
* weight=5といった形で重み付けが可能。

```
upstream backend {
  server 127.0.0.1:9000;
}

server {
  listen 80;
  server_name localhost;
  location / {
    proxy_pass http://backend;
  }
}
```