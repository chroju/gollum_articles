* Webサーバー。
* Preforkで動くApacheと比較すると、イベント駆動で展開するため使用リソースが少なく、軽量である（シングルプロセスで動作する）。
* リバースプロキシとしての機能を備えている。
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