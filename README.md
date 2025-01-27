# odoo18
odoo install in Ubuntu 24.04 LTS
<br>

## Step #1: Update the server
```
sudo apt-get update
sudo apt-get upgrade
```
#### Step #2: check version of the python3 
```
python3 --version
```
#### Step #3: Install packages and libraries(install git, python3-pip other nesesary file)
```
sudo apt install git python3-pip libldap2-dev libpq-dev libsasl2-dev
```
#### Step #4: odoo apr system needs a database, odoo works with PostgreSQL 
```
sudo apt install postgresql postgresql-client
```
#### Step #5: Check the status of the PostgreSQL service
```
sudo systemctl status postgresql
```
#### Step #6:create user of database
```
su - postgres -c "createuser -s odoo18"
```
Here "odoo18" is a database username
