# Server_config
 <i class="icon-cog"></i> **Settings**

### Installation Nginx
```
wget http://nginx.org/keys/nginx_signing.key
sudo apt-key add nginx_signing.key
```



 * create  nginx.list :  
```
sudo nano /etc/apt/sources.list.d/nginx.list
add this command :
 
deb http://nginx.org/packages/ubuntu/ trusty nginx
deb-src http://nginx.org/packages/ubuntu/ trusty nginx
```

```
   sudo apt-get update
   sudo apt-get install nginx
```


### Installation Php5-fpm
```
sudo apt-get install php5-fpm
sudo apt-get install php5-fpm php5-mysql
sudo apt-get install php5-fpm php5-cli
sudo apt-get install php5-fpm php5-mcrypt
```

 * try it now with  :  
```
sudo service php5-fpm start
```
### php.ini

```
sudo nano /etc/php5-fpm/fpm/php.ini

```
change cgi.fix_pathinfo=1 to 0 

###  www.conf
```
sudo nano /etc/php5/fpm/pool.d/www.conf
```
change : listen.owner/group to nginx


### sudo nano /etc/nginx/conf.d/default.conf
**default.conf**

```
server {
	listen 80;
	root /usr/share/nginx/html;
	index index.php index.html index.htm;
	server_name localhost;
		
	location / {
	try_files $uri $uri/index.php;
}

	location ~ \.php$ {
	try_files $uri = 404;
	fastcgi_pass unix:/var/run/php5-fpm.sock;
	fastcgi_index index.php;
	fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
	include fastcgi_params;	

}


}
```

### Installation MariaDB
```
sudo apt-get install mariadb-server
```

 * try it now with :  
```
mysql -u root -p 
```


### Installation FTP
```
sudo apt-get install proftpd -y
```

 * try it now with :  
```
mysql -u root -p 
```

### Installation SSH
```
sudo apt-get install openssh-server
```

 * You can change port in  :  
```
sudo nano /etc/ssh/sshd_config
```

 <i class="icon-cog"></i> **IMPORTANT**


you have to reload of service, like this : 

```
sudo service nginx restart
sudo service php5-fpm restart
```