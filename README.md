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
sudo apt install git python3-pip libldap2-dev libpq-dev libsasl2-dev
```
### Step #4: odoo apr system needs a database, odoo works with PostgreSQL 
```
sudo apt install postgresql postgresql-client
```
### Step #5: Check the status of the PostgreSQL service
```
sudo systemctl enable PostgreSQL
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
sudo apt install python3-venv
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
/opt/odoo18/odoo

### Step #17: Run odoo "/opt/odoo18/odoo"

```
python3 odoo-bin -c dbian/odoo.conf
```

### Step #18: Access your odoo server 
```
yourdomain:8069
```
```
yourip:8069
```
