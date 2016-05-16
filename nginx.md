nginx.conf
----

### upstream

`proxy_pass`等で参照されるサーバーグループの設定を書く。

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