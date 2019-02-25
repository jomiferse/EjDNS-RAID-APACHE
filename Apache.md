# Apache

# Comandos Usados

1.
~~~
sudo apt-get install apache2
~~~

2.
~~~
sudo mkdir -p /var/www/gato.com/html
sudo mkdir -p /var/www/mosquito.com/html
sudo mkdir -p /var/www/escherichiacoli.es/html
sudo mkdir -p /var/www/chip555.org/html
~~~

3.
~~~
sudo chmod -R 777 /var/www
~~~

4.
~~~
echo "gato.com" > /var/www/gato.com/html/index.html
echo "mosquito.com" > /var/www/mosquito.com/html/index.html
echo "escherichiacoli.es" > /var/www/escherichiacoli.es/html/index.html
echo "chip555.org" > /var/www/chip555.org/html/index.html
~~~

5.
~~~
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/gato.com.conf
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/mosquito.com.conf
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/escherichiacoli.es.conf
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/chip555.org.conf
~~~

6.
~~~
<VirtualHost *:80>
    ServerAdmin admin@gato.com
    ServerName gato.com
    ServerAlias www.gato.com
    DocumentRoot /var/www/gato.com/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
<VirtualHost *:80>
    ServerAdmin admin@mosquito.com
    ServerName mosquito.com
    ServerAlias www.mosquito.com
    DocumentRoot /var/www/mosquito.com/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
<VirtualHost *:80>
    ServerAdmin admin@escherichiacoli.es
    ServerName escherichiacoli.es
    ServerAlias www.escherichiacoli.es
    DocumentRoot /var/www/escherichiacoli.es/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
<VirtualHost *:80>
    ServerAdmin admin@chip555.org
    ServerName chip555.org
    ServerAlias www.chip555.org
    DocumentRoot /var/www/chip555.org/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
~~~

7.
~~~
sudo a2ensite gato.com.conf
sudo a2ensite mosquito.com.conf
sudo a2ensite escherichiacoli.es.conf
sudo a2ensite chip555.org.conf
~~~

8.
~~~
sudo service apache2 restart
~~~

#Autentificación, Autorización y Control de Acceso

9.
~~~
sudo htpasswd -c /var/www/gato.com/passwords usuario1
sudo htpasswd  /var/www/gato.com/passwords usuario2
~~~

10.
~~~
<Directory /var/www/gato.com/html>
	AuthType Basic
	AuthName "ACCESO RESTRINGIDO."
	AuthUserFile /var/www/gato.com/passwords
	Require user usuario1
</Directory>
<Directory /var/www/gato.com/html>        
	Options Indexes FollowSymLinks MultiViews
	AllowOverride  none
	Order Allow,deny
	allow from all
</Directory>
<Directory /var/www/mosquito.com/html>
	AuthType Basic
	AuthName "ACCESO RESTRINGIDO."
	AuthUserFile /var/www/gato.com/passwords
	Require user usuario3
</Directory>
<Directory /var/www/mosquito.com/html>        
	Options Indexes FollowSymLinks MultiViews
	AllowOverride  none
	Order Allow,deny
	allow from all
</Directory>
<Directory /var/www/escherichiacoli.es/html>
	AuthType Basic
	AuthName "ACCESO RESTRINGIDO."
	AuthUserFile /var/www/gato.com/passwords
	Require user usuario1
</Directory>
<Directory /var/www/escherichiacoli.es/html>        
	Options Indexes FollowSymLinks MultiViews
	AllowOverride  none
	Order Allow,deny
	allow from all
</Directory>
<Directory /var/www/chip555.org/html>
	AuthType Basic
	AuthName "ACCESO RESTRINGIDO."
	AuthUserFile /var/www/gato.com/passwords
	Require user usuario1
</Directory>
<Directory /var/www/chip555.org/html>        
	Options Indexes FollowSymLinks MultiViews
	AllowOverride  none
	Order Allow,deny
	allow from all
</Directory>
~~~

11.
~~~
sudo service apache2 restart
~~~
