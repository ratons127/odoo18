# odoo18
odoo install in Ubuntu 24.04 LTS
<br>

### Step #1: Update the server
```
sudo apt-get update
sudo apt-get upgrade -y
```
### Step #2: check version of the python3 
```
python3 --version
```
### Step #3: Install packages and libraries(install git, python3-pip other nesesary file)
```
sudo apt install git python3-pip libldap2-dev libpq-dev libsasl2-dev -y
```
### Step #4: odoo apr system needs a database, odoo works with PostgreSQL 

```
sudo apt install postgresql postgresql-client -y
```
### Step #5: Check the status of the PostgreSQL service

```
sudo systemctl enable postgresql
```
```
sudo systemctl status postgresql
```
### Step #6:create user of database
```
su - postgres -c "createuser -s odoo18"
```
Here "odoo18" is a database username and "postgres" is otheruser of ubuntu 24.04

### Step #7:Switch user root to postgres 

```
su postgres
```
### Step #8: Reset the password of PSQL database user "odoo18"

```
psql
```
```
ALTER USER odoo18 WITH PASSWORD '2wsx9ijn';
```
Here 'odoo18' is database username and '2wsx9ijn' is password
<be>
After resetting the password press clt+z and enter exit, exit to go root user

### Step #9: Creature a directory and a User of odoo18

```
sudo useradd -m -d /opt/odoo18 -U -r -s /bin/bash odoo18
```
after creating a Directory 'odoo18' to go to the directory 
```
cd /opt/odoo18
```
### Step #10: Clone git into the 'opt/odoo18' directory

```
git clone https://www.github.com/odoo/odoo --depth 1 --branch 18.0 --single-branch odoo
```
Here 'odoo' is a directory into the 'odoo18' directory
<be>
This link helps to clone Odoo '18' version

### Step #11:Installing virtual environment for not mixing other odoo or versions

```
sudo apt install python3-venv -y
```
### Step #12: Create a virtual environment of 'odoo'

```
cd /opt/odoo18
```
to go to the odoo18 directory and make a virtual environment of odoo-venv
```
python3 -m venv odoo-venv 
```
Here 'odoo-venv' is a virtual environment name you can choose any name

### Step #13:Active virtual directory to this directory /opt/odoo18

```
source odoo-venv/bin/activate
```
### Step #14: Install all pachages of Odoo

```
pip install -r odoo/requirements.txt
```
### Step #15: Edit odoo.conf file from '/opt/odoo18/odoo/debian'

```
cd /opt/odoo18/odoo/debian
```
```
nano odoo.conf
```
edit this script
```
[options]
; This is the password that allows database operations:
; admin_passwd = admin
db_host = False
db_port = False
db_user = odoo
db_password = False
;addons_path = /usr/lib/python3/dist-packages/odoo/addons
default_productivity_apps = True
```
to change this
```
; This is the password that allows database operations:
; admin_passwd = admin
db_host = False
db_port = False
db_user = odoo18
db_password = 2wsx9ijn
addons_path = /opt/odoo18/odoo/addons
default_productivity_apps = True
xmlrpc_port = 8069
```
### Step #16: switch user 'root' to 'odoo18' and active virtual directory 

```
sudo su odoo18
```
```
source odoo-venv/bin/activate 
```
```
cd /opt/odoo18
```

### Step #17: Run odoo "/opt/odoo18/odoo"

```
cd /opt/odoo18/odoo
```
```
python3 odoo-bin -c debian/odoo.conf
```

### Step #18: Access your odoo server 

```
yourdomain:8069
```
```
yourip:8069
```
<br>
<br>
<br>

### Step #19:  Install Apache and Required Modules)

```
sudo apt install apache2 -y
sudo a2enmod proxy proxy_http proxy_balancer lbmethod_byrequests rewrite headers ssl
sudo systemctl restart apache2
```
>Enable Apache to start on boot:

```
sudo systemctl enable apache2
sudo systemctl restart apache2
```
### Step #20: Create an Apache Virtual Host Configuration for Odoo

```
sudo nano /etc/apache2/sites-available/odoo18.conf
```
Add the following content:
```
<VirtualHost *:80>
    ServerName bbs.raton.live

    ProxyRequests Off
    ProxyPass / http://127.0.0.1:8069/
    ProxyPassReverse / http://127.0.0.1:8069/

    <Proxy *>
        Require all granted
    </Proxy>

    ErrorLog ${APACHE_LOG_DIR}/odoo18_error.log
    CustomLog ${APACHE_LOG_DIR}/odoo18_access.log combined
</VirtualHost>
```
### Step #21:Enable the Configuration and Restart Apache

```
sudo a2dissite 000-default.conf
```
```
sudo a2ensite bbs.raton.live.conf
```
```
 systemctl reload apache2
````
### Step #22:Allow Traffic on Port 80 (ufw)

```
sudo ufw start
sudo ufw enable
```
```
sudo ufw allow 80/tcp
sudo ufw allow 8069/tcp
sudo ufw allow 443/tcp
sudo ufw allow 8443/tcp
sudo ufw allow 22
sudo ufw reload
```
### Step #22: Let's fix your SSL issue for bbs.raton.live Follow these steps:
>Install Let's Encrypt Certbot for Apache:

```
sudo apt update
sudo apt install certbot python3-certbot-apache -y
```

### Step #23:Obtain SSL Certificate

```
sudo certbot --apache -d bbs.raton.live -d www.bbs.raton.live
```
Restart Apache:
```
sudo systemctl restart apache2
```
### Verify SSL
```
sudo certbot certificates
```

























