### Nginx 초당 처리 요청

![image](https://github.com/conf312/issuemoa-document/assets/13326651/f468a12d-9c41-475f-809b-378a0e14b38e)
irate( nginx_http_requests_total{job="nginx-exporter"}[5m] )

![image](https://github.com/conf312/issuemoa-document/assets/13326651/dba8ffcf-4eab-41bb-b9f4-bba67f32f755)
sum( rate( nginx_http_requests_total{job="nginx-exporter"}[5m] ) )

