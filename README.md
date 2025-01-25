# odoo18
odoo install in Ubuntu 24.04 LTS
<br>
Author - MD RATON ISLAM

sudo apt-get update
sudo apt -y upgrade
Step #2: Install packages and libraries
sudo apt install git python3-pip build-essential wget python3-dev libpq-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less
Step #3: Create a system user for Odoo 14
sudo useradd -m -d /opt/odoov14 -U -r -s /bin/bash odoov14
Step #4: Install Postgresql server
sudo apt install postgresql
Step #5: Create Postgresql user for Odoo 14
sudo su - postgres -c "createuser -s odoov14"
Step #6: Set the password for Odoov14 Postgresql user
sudo su postgres
psql
ALTER ROLE odoov14 WITH PASSWORD 'odoov14';
Press ctrl + Z to exist this and then execute exit command to exist postgres user

Step #7: Switch to odoov14 system User
sudo su odoov14
Step #8: Clone/Download odoo 14 source code
git clone https://www.github.com/odoo/odoo --depth 1 --branch 14.0 /opt/odoov14/odoo
Step #9: Move to Odoo 14 directory
cd /opt/odoov14/
Step #10: Install python dependencies
pip3 install -r odoo/requirements.txt
Step #11: Create Odoo Configuration file
nano odoo.conf
