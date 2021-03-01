FROM nginx

ADD nginx-example.conf /etc/nginx/example/nginx-example.conf
COPY nginx.crt /etc/nginx/ssl/nginx.crt
COPY nginx.key /etc/nginx/ssl/nginx.key

EXPOSE 443

ENV SSL_EXPOSE_PORT=49999
CMD envsubst '${SSL_EXPOSE_PORT}' < /etc/nginx/example/nginx-example.conf > /etc/nginx/conf.d/default.conf && \
nginx -g "daemon off;"
## nginx -g "daemon off;" 這一定要執行才能運作
