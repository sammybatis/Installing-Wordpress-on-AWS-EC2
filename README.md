# Installing-Wordpress-on-AWS-EC2


#### Installing Aparche Server ####
sudo apt-get update -y

sudo apt install apache2 -y
sudo systemctl status apache2

sudo systemctl enable apache2



#### Installing MySql server ####

sudo apt install mysql-server -y

sudo systemctl start mysql.service

sudo systemctl status mysql.service

   

#### Configuring MySQL ####

sudo mysql

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

exit

sudo mysql_secure_installation

mysql -u root -p

CREATE USER 'cloudtechwithsam' IDENTIFIED WITH mysql_native_password BY 'password';

Create database wordpress;

GRANT all ON wordpress.* TO 'cloudtechwithsam';

Flush privileges;

exit


#### Installing PHP #####

sudo apt install php php-mysql php-gd php-cli php-common -y

sudo apt install unzip wget -y



#### Downloading and Installing Wordpress ####

wget https://wordpress.org/latest.zip

unzip latest

sudo cp -R wordpress/* /var/www/html

cd /var/www/html

ls -l

sudo chown www-data:www-data -R /var/www/html

sudo rm -rf index.html


##### Creating virtual host for the domain #####

cd /etc/apache2/sites-available 

sudo vim yourdomainname.com.conf


#### Copy and Paste into yourdomainname.com.conf file ####

<VirtualHost *:80>
    ServerAdmin admin@example.com
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

### End ####


sudo a2ensite yourdomainname.com.conf

sudo a2dissite 000-default.conf

sudo systemctl restart apache2
sudo systemctl status apache2



#### Installing SSL ####

sudo apt install certbot python3-certbot-apache -y

sudo certbot --apache 
