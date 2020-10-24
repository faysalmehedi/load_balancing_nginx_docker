## TASK: 

01. Load Balancing Three Docker container with Nginx
02. Load Balancing by health check
03. Load Balancing by Weight check

## Steps for Running

# Make sure you install Docker Engine and Nginx in your system 
- Installing Docker: please go through the link and follow [https://docs.docker.com/engine/install/]

- Installing Nginx
```
$ sudo apt update
$ sudo apt install nginx
$ sudo systemctl start nginx
$ sudo systemctl status nginx
```
- clone the repository from github
```
$ sudo git clone https://github.com/faayam/load_balancing_nginx_docker.git
$ cd load_balancing_nginx_docker
```
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

- Running App Containers
   ```
   $ sudo docker run -d -p 3030:5000 app01
   $ sudo docker run -d -p 3031:5000 app02
   $ sudo docker run -d -p 3032:5000 app03
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
