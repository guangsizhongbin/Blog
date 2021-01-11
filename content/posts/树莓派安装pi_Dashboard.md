---
title: "树莓派安装pi_Dashboard"
date: 2021-01-11T22:53:10+08:00
lastmod: 2021-01-11
author: "xiaonan"
math:
 enable: true

tags: [Dashboard]
categories: [树莓派]
---

## 安装Nginx和PHP

```bash
sudo apt-get update
sudo apt-get install nginx php7.3-fpm php7.3-cli php7.3-curl php-7.3-gd php7.3-cgi
sudo service nginx start
sudo service php7.3-fpm restart
```

使`Nginx`能处理`PHP`
`sudo nano /etc/nginx/sites-available/default`

```
location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }
```

修改为

```
location / {
index  index.html index.htm index.php default.html default.htm default.php;
}
 
location ~\.php$ {
fastcgi_pass unix:/run/php/php7.3-fpm.sock;
#fastcgi_pass 127.0.0.1:9000;
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
include fastcgi_params;
}
```

重启`nginx`

`sudo service nginx restart`

## 下载pi-dashboard

```bash
sudo apt-get install git
cd /var/www/html
sudo git clone https://github.com/nxez/pi-dashboard.git
sudo chown -R www-data pi-dashboard
```

通过`http://树莓派IP/pi-dashboard`访问部署好的`Pi Dashboard`

## 参考

[Pi Dashboard (Pi 仪表盘)](https://make.quwj.com/project/10)



