# Guide to Install Frappe ERPNext in Ubuntu 22.04 LTS

A complete guide to install Frappe Bench in Ubuntu 22.04 LTS and set up Frappe/ERPNext application.

---

# Pre-requisites

- Python 3.6+
- Node.js 14+
- Redis 5 (caching and real-time updates)
- MariaDB 10.3.x / Postgres 9.5.x (to run database-driven apps)
- Yarn 1.12+ (JS dependency manager)
- Pip 20+ (Python dependency manager)
- wkhtmltopdf (version 0.12.5 with patched qt) (for PDF generation)
- Cron (bench's scheduled jobs: automated certificate renewal, scheduled backups)
- NGINX (proxying multitenant sites in production)

---

# STEP 1: Install Git
 ```bash
 sudo apt-get install git

```



# STEP 2: Install Python Development Headers
 ```bash
 sudo apt-get install python3-dev
```
# STEP 3: Install setuptools and pip
```bash
sudo apt-get install python3-setuptools python3-pip
```
# STEP 4: Install virtualenv
```bash
sudo apt-get install virtualenv
python3 -V
```
If version is 3.10.x:
```bash
sudo apt install python3.12-venv

```
# STEP 5: Install MariaDB
```bash
sudo apt-get install software-properties-common
sudo apt install mariadb-server
sudo mysql_secure_installation

```
# STEP 6: Install MySQL development files
```bash
sudo apt-get install libmysqlclient-dev
```
# sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```bash
[server]
user = mysql
pid-file = /run/mysqld/mysqld.pid
socket = /run/mysqld/mysqld.sock
basedir = /usr
datadir = /var/lib/mysql
tmpdir = /tmp
lc-messages-dir = /usr/share/mysql
bind-address = 127.0.0.1
query_cache_size = 16M
log_error = /var/log/mysql/error.log

[mysqld]
innodb-file-format=barracuda
innodb-file-per-table=1
innodb-large-prefix=1
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci      

[mysql]
default-character-set = utf8mb4
```
Restart MariaDB:
```bash
sudo service mysql restart
```
# STEP 8: Install Redis
```bash
sudo apt-get install redis-server
```
# STEP 9: Install Node.js 18 using NVM
```bash
sudo apt install curl
mkdir -p ~/.nvm
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
source ~/.bashrc
nvm install 18
```
# STEP 10: Install Yarn
```bash
sudo apt-get install npm
sudo npm install -g yarn
```
# STEP 11: Install wkhtmltopdf
```bash
sudo apt-get install xvfb libfontconfig wkhtmltopdf
```
# STEP 12: Install Frappe Bench
```bash
sudo apt install python3.12-venv
python3.12 -m venv ~/frappe-bench-env
source ~/frappe-bench-env/bin/activate
pip install --upgrade pip
pip install frappe-bench
bench --version
```

# STEP 13: Initialize Frappe Bench
```bash
bench init frappe-bench
cd frappe-bench/
bench start
```
# STEP 14: Create a site in Frappe Bench
```bash
bench new-site dcode.com
bench use dcode.com
```
# STEP 15: Install ERPNext in Bench & Site
```bash
# Option 1: Using branch
bench get-app erpnext --branch version-13

# Option 2: Using GitHub URL
bench get-app https://github.com/frappe/erpnext --branch version-13

# Install ERPNext on your site
```bash
bench --site dcode.com install-app erpnext
```

# Start the server
```bash
bench start
```
# Check site for any error 
```bash
bench --site dcode.com doctor
```




