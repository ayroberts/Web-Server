# Web-Server
*System Administration - Project 1*

**Part 1: Creating Web Server**

Command used to send files to AWS
scp -i labsuser.pem index.html ubuntu@44.208.152.202:~/

**Installing Apache**
sudo apt-get update
sudo apt-get install apache2

**Start Apache**
sudo systemctl start apache2
sudo systemctl status apache2
</br>
The HTTP server will run on port 80 by default

Serves content from /var/www/html

Config file is called ‘apache2.conf’
</br>
http://44.208.152.202

Set permissions
sudo groupadd devs
sudo usermod -a -G devs ubuntu
sudo chmod -R g+rwx /var/www/html
</br>
**Part 2: HTTPS**

**Generate a private key**
openssl genpkey -algorithm RSA -out private.key

**Generate a certificate signing request**
openssl req -new -key private.key -out cert.csr

**Generate a self-signed certificate using the private key and CSR**
openssl x509 -req -days 14 -in cert.csr -signkey private.key -out cert.crt

**Enable HTTPS and Redirect traffic**
sudo nano /etc/apache2/apache2.conf
	-RewriteEngine On
	-RewriteCond %{HTTPS} off
	-RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
sudo systemctl restart apache2

**This actually broke my server, and tbh it’s not worth my time to figure out why it doesn’t work. I tried and couldn’t get it, so no HTTPS for me.**
</br>
**Part 3: Firewall**

**Allow SSH connections from my home**
Security Groups > Inbound > Edit > Add Rule 
Type > SSH
Source > “0.0.0.0/32”







