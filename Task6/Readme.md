# Задание 6. Настройка Rate Limiting

Конфигурация [nginx.config](nginx.conf)

```
http {
    # Определение зоны для ограничения запросов
    limit_req_zone $binary_remote_addr zone=one:10m rate=10r/m;

    # Настройка upstream для балансировки нагрузки
    upstream backend_servers {
        server backend1.example.com;
        server backend2.example.com;
        server backend3.example.com;
    }

    server {
        listen 80;

        location / {
            # Применение ограничения запросов 
            # с возможностью обработки всплеска из 5 доп. запросов
            limit_req zone=one burst=5 nodelay;
            # Установка кода ошибки при превышении лимита
            limit_req_status 429;
            
            proxy_pass http://backend_servers;
        }
    }
}
 

```