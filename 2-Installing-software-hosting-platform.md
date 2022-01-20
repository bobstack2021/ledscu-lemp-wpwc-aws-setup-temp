# Installing Required software for our Hosting Platform
# On your Webserver (as root)
## Install software

apt update
apt upgrade

# OR just run:

apt update & apt upgrade -y

# Make sure to install the mysql-server package FIRST (before installing the other packages):

apt install mysql-server

# OR just run:

apt install mysql-server -y

# Then install the following:

apt install nginx php-mysql php-fpm monit

# OR just run:

apt install nginx php-mysql php-fpm monit -y
