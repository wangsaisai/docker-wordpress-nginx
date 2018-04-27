# docker-wordpress-nginx

A Dockerfile that installs the latest wordpress, nginx, php-apc and php-fpm.

NB: A big thanks to [jbfink](https://github.com/jbfink/docker-wordpress) who did most of the hard work on the wordpress parts!

You can check out his [Apache version here](https://github.com/jbfink/docker-wordpress).

## Installation

Download codes
```bash
$ git clone https://github.com/wangsaisai/docker-wordpress-nginx.git
$ cd docker-wordpress-nginx
```

Edit nginx-site.conf, configure for cert files
```bash
# related configure for ssl
# use your own .crt .key files
# if you donot use ssl, remove these configure
listen	443 ssl;
ssl_certificate /cert-path/www.example.com.crt;
ssl_certificate_key /cert-path/www.example.com.key;
```

Build the image:

```bash
$ sudo docker build -t="wangsaisai/docker-wordpress-nginx" .
```

## Usage

To spawn a new instance of wordpress on port 80.  The -p 80:80 maps the internal docker port 80 to the outside port 80 of the host machine.

```bash
# first port is machine port, last port is container port; path is similar
# don't forget the path of cert files if enable https
$ sudo docker run -p 80:80 -p 443:443 -v /var/lib/mysql:/var/lib/mysql -v /usr/share/nginx/www:/usr/share/nginx/www -v /etc/nginx:/etc/nginx -v /cert-path:/cert-path --name docker-wordpress-nginx -d wangsaisai/docker-wordpress-nginx
```

Start your newly created docker.

```
$ sudo docker start docker-wordpress-nginx
```

After starting the docker-wordpress-nginx check to see if it started and the port mapping is correct.  This will also report the port mapping between the docker container and the host machine.

```
$ sudo docker ps

0.0.0.0:80 -> 80/tcp, 0.0.0.0:443 -> 443/tcp docker-wordpress-nginx
```

You can the visit the following URL in a browser on your host machine to get started:

```
http://127.0.0.1
https://127.0.0.1
```
