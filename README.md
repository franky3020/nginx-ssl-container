# nginx-ssl + nextcloud

## 原因
因nextcloud 只有 http, 安全性不夠, 所以可以讓請求透過 nginx 的 https, 再轉發到nextcloud, 來增加安全性

## 前置步驟

先自行生成憑證跟私鑰, 憑證裡有公鑰與一些描述資訊, 通常會將此憑證交給第三方機構認證

`sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout $(pwd)/nginx.key -out $(pwd)/nginx.crt`

把  nginx.key 與 nginx.crt 都放在 nginx 資料夾就可以了

## 部署
`docker-compose up -d --build`, (有`--build` 是因為這樣才能確保是會重新build Dockerfile才運行),

`SSL_EXPOSE_PORT=50603`, 這是進入nextcloud  服務的唯一入口。 

## 維護
如果將來要更新憑證, 則只要替換 nginx.key 與 nginx.crt, 再執行 `docker-compose up -d --build nginx-ssl`

## 參考來源

[Nginx 設定](https://blog.gtwang.org/linux/nginx-create-and-install-ssl-certificate-on-ubuntu-linux/)
