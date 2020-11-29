# Hello World Apache and SSL On Debian
[![OS badge](https://img.shields.io/badge/OS-Debian-red.svg)](https://www.debian.org)
[![Server badge](https://img.shields.io/badge/Server-Apache-blue.svg)](https://httpd.apache.org)
[![SSL badge](https://img.shields.io/badge/SSL-certbot-blue.svg)](https://httpd.apache.org)
[![Format badge](https://img.shields.io/badge/Format-HTML-green.svg)](https://lyty.dev/html/index.html)

## Objectif 

Create page HTML for **hello-world.hephaiscode.com** with Apache and HTML File

## You need

- Server on Debian (linux distribution) with root access
- DN (Domain Name) point on Server IP (example hello-world.hephaiscode.com on 51.83.45.10)
- Terminal/console to enter instruction

## Parameters

We use :
 - hello-world.hephaiscode.com for domain name of our web page
 - 51.83.45.10 the IP address of our server computer
 

## Connect to server 

Open terminal or console and go to admin your server.

```
ssh -l root 51.83.45.10 
```

And enter your root password 

## Update your server

Always to be update.

```
apt-get update
apt-get -y upgrade
apt-get -y dist-upgrade
```

## Install Apache

Install Apache as WebServer to communicate with your server at **hello-world.hephaiscode.com **

```
apt-get -y install apache2
apt-get -y install apache2-doc
apt-get -y install apache2-suexec-custom
apt-get -y install logrotate
apt-get -y install openssl
systemctl restart apache2
```

## Install Domain Name

Create the host parameters for Apache and our domains **hello-world.hephaiscode.com**

```
mkdir /home/helloworld
rm /etc/apache2/sites-available/helloworld_ws.conf
echo "<VirtualHost *:80>" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "Protocols h2 http/1.1" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "ServerAdmin contact@helloworld.io" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "ServerName hello-world.hephaiscode.com" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "ServerAlias hello-world.hephaiscode.com" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "DocumentRoot /home/helloworld" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "<Directory />" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "AllowOverride All" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "</Directory>" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "<Directory /home/helloworld>" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "Options Indexes FollowSymLinks MultiViews" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "AllowOverride all" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "Require all granted" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "</Directory>" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "LogLevel error" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "ErrorLog /var/log/apache2/helloworld-error.log" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "CustomLog /var/log/apache2/helloworld-ssl-access.log combined env=NoLog" >> /etc/apache2/sites-available/helloworld_ws.conf
echo "</VirtualHost>" >> /etc/apache2/sites-available/helloworld_ws.conf
a2ensite helloworld_ws.conf


// create virtual host with SSL
rm /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "echo \"<IfModule mod_ssl.c>\" >> /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a <VirtualHost *:443>' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a Protocols h2 http/1.1' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a ServerAdmin " + Email + "' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a ServerName " + tServerDomain.ServerDNS + "' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a ServerAlias " + tServerDomain.ServerDNS+ "' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a DocumentRoot /home/" + User + "/" + Folder  + _SSL+ "' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a <Directory />' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a AllowOverride All' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a </Directory>' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a <Directory /home/" + User + "/" + Folder  + _SSL+ ">' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a Options Indexes FollowSymLinks MultiViews' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a AllowOverride all' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a Require all granted' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a </Directory>' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a LogLevel error' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a ErrorLog /var/log/apache2/" + tServerDomain.ServerDNS + "-error.log' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a CustomLog /var/log/apache2/" + tServerDomain.ServerDNS + "-ssl-access.log combined env=NoLog' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a SSLEngine On' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a SSLCipherSuite ALL:!DH:!EXPORT:!RC4:+HIGH:+MEDIUM:!LOW:!aNULL:!eNULL' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a SSLCertificateFile /home/" + User + "/ssl/" + tServerDomain.ServerDNS + ".crt' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a SSLCertificateKeyFile /home/" + User + "/ssl/" + tServerDomain.ServerDNS + ".key' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a </VirtualHost>' > /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "sed -i '$ a </IfModule>'> /etc/apache2/sites-available/helloworld_ssl_ws.conf
                "a2ensite " + tServerDomain.ServerDNS + _SSL +"_ws.conf",
                
                
                
systemctl restart apache2
```

## Install Certboot for automatic SSL
```
apt-get -y install certbot python-certbot-apache
certbot --agree-tos -n --no-eff-email --apache --redirect --email ${MYEMAIL} -d ${MYDOMAINNAME}
```

## File Script
Write root's file in HTML. The name is index.html
```
rm /home/helloworld/index.html
echo '<html><body>Hello World!</body></html>' >> /home/helloworld/index.html
```

## Test your SSL certficate 

https://www.ssllabs.com/ssltest/analyze.html?d=hello-world.hephaiscode.com


## Hello World Success

Open browser and go to page https://hello-world.hephaiscode.com 


![Success](https://img.shields.io/badge/Hello%20World-OK-Green.svg)
