## TASK: 

01. Load Balancing Three Docker container with Nginx
02. Load Balancing by health check

# Steps for Running

- Build Docker by running command 
    ```
    $ cd app01
    $ sudo docker build --tag app01 .
    $ cd ../app02
    $ sudo docker build --tag app02 .
    $ cd ../app03
    $ sudo docker build --tag app03 .
    ```
- Move nginx.conf file to the main /etc/nginx/ and modifying configuration
    ```
    $ sudo mv /nginx.conf /etc/nginx/nginx.conf
    $ sudo nginx -s reload
    ```

- Go to http://localhost or http://localhost:80

## NGINX CONFIGURATION FILE

```
nginx.conf
```

```
http {
        upstream webapp {
                server localhost:3030 weight=3;
                server localhost:3031 max_fails=3 fail_timeout=30s;
                server localhost:3032;
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
