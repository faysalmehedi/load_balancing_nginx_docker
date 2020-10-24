## TASK: 

01. Load Balancing Three Docker containers with Nginx
02. Load Balancing by health check
03. Load Balancing by Weight check

## Steps for Running

- Run with Docker Compose
    ```
    $ docker-compose up
    ```

- Go to http://localhost or http://localhost:80

## NGINX CONFIGURATION FILE

```
nginx.conf
```

```
http {
        upstream webapp {
                server app01:5000 weight=3;
                server app02:5000 max_fails=3 fail_timeout=30s;
                server app03:5000;
        }

        server {
                listen 80;
                location / {
                        proxy_pass http://webapp;
                }
        }
}

events { }
```
