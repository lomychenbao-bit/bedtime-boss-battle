# 晚睡大魔王 - 部署指南

## 服务器信息

- **地址**: `<YOUR_SERVER_IP>`
- **系统**: Ubuntu 24.04, Nginx
- **站点路径**: `/var/www/bedtime-battle/`
- **访问地址**: `http://<YOUR_SERVER_IP>`

## 部署步骤

1. 上传 `index.html` 和 `images/` 到 `/var/www/bedtime-battle/`
2. 重启 Nginx: `sudo systemctl restart nginx`
3. 强制刷新浏览器（Cmd+Shift+R）

## Nginx 配置

```
server {
    listen 80;
    root /var/www/bedtime-battle;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location /api/ {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location ~* \.(png|jpg|jpeg|gif|svg|css|js)$ {
        expires 30d;
        add_header Cache-Control "public, immutable";
    }
}
```
