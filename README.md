# brotli

Works on Ubuntu 24.04

```bash
sudo apt update
```

Install nginx:
```bash
sudo apt install -y nginx
```

Install brotli packages:
```bash
sudo apt install -y \
  libnginx-mod-http-brotli-filter \
  libnginx-mod-http-brotli-static
```

```
sudo vim /etc/nginx/nginx.conf
```

```
        ##
        # Brotli Settings
        ##

        brotli on;
        brotli_comp_level 6;
        brotli_static on;
```



```bash
sudo systemctl restart nginx
```

```bash
curl -H "Accept-Encoding: br" -I 127.0.0.1
```

