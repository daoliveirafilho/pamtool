<!-- ABOUT THE PROJECT -->

# O _???Tool_ &eacute; uma solu&ccedil;&atilde;o de gerenciamento de acesso privilegiado para ambientes h&iacute;bridos.

### Pr&eacute;-requisitos

Os requisitos m&iacute;nimos para rodar o _???Tool_ s&atilde;o:
* 1 n&uacute;cleo de CPU.
* 2Gb de mem&oacute;ria RAM
* 10Gb de storage

### Configura&ccedil;&atilde;o do Nginx.

```sh
vi /usr/local/etc/nginx/nginx.conf
```

```sh
http {
include       mime.types;
default_type  application/octet-stream;
sendfile        on;
keepalive_timeout  65;

server {
#listen 80;
listen [::1]:80;
server_name	rekall.log darkstar.rekall.log;
error_page 500 502 503 504 /50x.html;
location = /50x.html {
root   /usr/local/www;
}
error_page  404 /40x.html;
location = /40x.html {
root /usr/local/www;
}

location / {
root /usr/local/www;
index	index.html;
}
...
```

![Image_0209](assets/images/itens/IMG_0209.jpg)

### Configura&ccedil;&atilde;o do php-fpm.

```sh
vi /usr/local/etc/php-fpm.d/www.conf
```

```sh
[www]
user = www
group = www
listen = [::1]:9000
listen.owner = www
listen.group = www
listen.mode = 0440
...
```

![Image_0210](assets/images/itens/IMG_0210.jpg)

### Configura&ccedil;&atilde;o do phpPgAdmin.

```sh
location ^~ /phpPgAdmin {
alias	/usr/local/www/phpPgAdmin;
index	index.php;
location ~ \.php$ {
root	/usr/local/www;
include        fastcgi_params;
fastcgi_param  SCRIPT_FILENAME	$document_root$fastcgi_script_name;
fastcgi_pass   [::1]:9000;
} }
```

![Image_0211](assets/images/itens/IMG_0211.jpg)

### Instala&ccedil;&atilde;o do Postgresql e suas depend&ecirc;ncias.

```sh
groupadd -g 209 postgres
```
```sh
useradd -u 209 -g 209 -d /var/lib/pgsql postgres
```
```sh
bash /postgresql17.SlackBuild
```

<!-- DOCUMENTA&Ccedil;&Atilde;O -->
## Uso

![Image_0201](assets/images/itens/IMG_0201.jpg)

![Image_0202](assets/images/itens/IMG_0202.jpg)
