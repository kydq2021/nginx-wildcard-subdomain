# nginx-wildcard-subdomain

## Add wildcard domain
https://en.wikipedia.org/wiki/Wildcard_DNS_record
example
```
*.kydinh.xyz
```

## Add NGINX vhost
```
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        #root /var/www/html;
        #index index.html index.htm index.nginx-debian.html;
        server_name ~^(?<subdomain>[^.]+).kydinh.xyz;
        location / {
          proxy_set_header   X-Forwarded-For $remote_addr;
          proxy_set_header   Host $http_host;
          proxy_pass http://127.0.0.1:9000/$subdomain;
        }
}
```
## Test
```
const http = require('http');
http.createServer((req, res) => {
    res.write(`user ${req.url}`);
    res.end();
}).listen(9000);
```
```
curl xxx.kydinh.xyz
```
