# server-provisioning


Following are the steps for server provisioning:

1.server instance create

2.Installing git

3.Installing rbenv

4.Installing ruby build

5.Installing ruby

6.Installing nginx

7.Installing nodejs                                                                                                                                                                                                                                                             
8.Installing MySQL

9.Add user

#######################################

INSTRUCTIONS:

sudo  -i

Upgrading system:

sudo apt update; 

sudo apt upgrade -y; 

sudo apt dist-upgrade -y; 

sudo apt autoremove -y

#########################################

Install rbenv:

url: https://github.com/rbenv/rbenv#installation

git clone https://github.com/rbenv/rbenv.git /usr/local/rbenv

vim /etc/profile.d/rbenv.sh

Add the lines:

export RBENV_ROOT=/usr/local/rbenv

export PATH="/usr/local/rbenv/bin:$PATH"

eval "$(rbenv init -)"

chmod +x /etc/profile.d/rbenv.sh 

source /etc/profile.d/rbenv.sh

type rbenv 

##########################################

Install ruby dependencies: (https://github.com/rbenv/ruby-build/wiki#suggested-build-environment)

apt install autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm5 libgdbm-dev -y

Install ruby-build: (https://github.com/rbenv/ruby-build#readme)

mkdir -p "$(rbenv root)"/plugins

git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build

###########################################

Install ruby

rbenv install --list

rbenv install 2.6.3

rbenv global 2.6.3

echo “gem: --no-ri --no-rdoc” > /etc/gemrc

gem install bundler     # --no-ri --no-rdoc not required any longer

rbenv rehash

ruby -v

############################################

Install Nginx: (https://www.nginx.com/resources/wiki/start/topics/tutorials/install/)

wget https://nginx.org/keys/nginx_signing.key

apt-key add nginx_signing.key

Command to get the release name: lsb_release -a

vim /etc/apt/sources.list.d/nginx.list


deb http://nginx.org/packages/ubuntu/ $release nginx

deb-src http://nginx.org/packages/ubuntu/ $release nginx

deb http://nginx.org/packages/ubuntu/ bionic nginx

deb-src http://nginx.org/packages/ubuntu/ bionic nginx
  
sudo apt update

sudo apt install nginx

service nginx status

service nginx start

Install Node: (https://github.com/nodesource/distributions#debinstall)

latest stable version command:

curl -sL https://deb.nodesource.com/setup_13.x | sudo -E bash -
apt  install -y nodejs

node -v

MySQL: (https://dev.mysql.com/downloads/repo/apt/)

Mysql.com > download > APT repo > Get the link from bottom

wget https://dev.mysql.com/get/mysql-apt-config_0.8.11-1_all.deb

dpkg -i mysql-apt-config_0.8.11-1_all.deb

sudo apt update

sudo apt install mysql-server

service mysql status

service mysql stop

service mysql start

mysql -V

#####################################################

Add User:

useradd deployer -m -s /bin/bash

usermod -a -G sudo deployer

mkdir /home/deployer/.ssh

cp .ssh/authorized_keys /home/deployer/.ssh/ # Suggestion: create a file and add ssh

check the authorized_keys file

cd /etc/sudoers.d/

vim deployer

Add the lines:

deployer ALL=NOPASSWD:/bin/rm /etc/nginx/sites-enabled/default

deployer ALL=NOPASSWD:/bin/ln -nfs /home/deployer/* /etc/nginx/sites-enabled/*

deployer ALL=NOPASSWD:/bin/ln -nfs /home/deployer/* /etc/init.d/*

deployer ALL=NOPASSWD:/bin/ln -nfs /home/deployer/* /etc/logrotate.d/*

deployer ALL=NOPASSWD:/etc/init.d/nginx

deployer ALL=NOPASSWD:/etc/init.d/al_barakah_staging

deployer ALL=NOPASSWD:/usr/sbin/service al_barakah_staging

deployer ALL=NOPASSWD:/usr/sbin/service nginx reload
rbenv 
deployer ALL=NOPASSWD:/bin/rm /home/deployer/*

