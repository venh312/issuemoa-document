### Nginx 설치
```
sudo apt-get update
sudo apt install nginx -y
nginx -v
sudo service nginx status
```

### /etc/nginx/sites-available/default
```nginx
server {
  # 개인 인터넷은 80 포트가 막혀 있으므로 8081로 테스트
  listen 8081;
  listen [::]:8081;
  
  server_name gate.issuemoa.kr;
  
  # 모든 8081/* 요청을 -> https
  return 301 https://$host$request_uri;
}

server {
  listen 443 ssl;
  server_name gate.issuemoa.kr;

  # SSL 인증서 적용
  ssl_certificate /home/venh/certificate.crt;
  ssl_certificate_key /home/venh/private.key;

  location / {
    proxy_pass http://localhost:8000; # SCG로 리다이렉트
  }
}
```
