##linuxServerConfiguration

A baseline installation of Ubuntu Linux on a virtual machine to host a Flask web application. This includes the installation of updates, securing the system from a number of attack vectors and installing/configuring web and database servers.

## Ip address 
35.244.40.206


## SSH port
22


## URL for my web app
http://35.244.40.206.xip.io


## create and Secure server
1. Start a new Ubuntu Linux server instance on google cloud

2. Update all currently installed packages.
'''
sudo apt-get update
sudo sudo apt-get upgrade
'''
3. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).
4. Create a new user account named grader.
5. Give grader the permission to sudo.
6. Configure the local timezone to UTC.
7. Create an SSH key pair for grader using the ssh-keygen tool(localy) and put a copy of it in my server and secure it.
8.  ssh key path in server
'''
/home/grader/.ssh/authorized_keys
'''

## configure SSH access
#Change ssh config file:

1. Open the config file:
$ vim /etc/ssh/sshd_config

2. try to Change to Port 2200. I'm working in google cluod and when I try to ssh with new port I get this message "We are unable to connect to the VM on port 2200"
so I return the port to 22
3. Change PermitRootLogin from without-password to no and PasswordAuthentication to no
4. Append UseDNS no.
5. Append AllowUsers grader.
6. Restart SSH Service:
$ sudo service sshd restart


## Prepare to deploy  project
1. Append the hostname to the first line:
$ sudo sudonano /etc/hosts

2. Install Apache web server:
$ sudo apt-get install apache2

3. Install mod_wsgi for serving Python apps from Apache and the helper package python-setuptools:
$ sudo apt-get install python-setuptools libapache2-mod-wsgi

4. Restart the Apache server for mod_wsgi to load:
$ sudo service apache2 restart

5. Enable the new config file:
$ sudo a2enconf fqdn


### Installing and confguration
1. Install Git:
$ sudo apt-get install git

2. Set your name, e.g. for the commits:
$ git config --global user.name "YOUR NAME"

3. Set up your email address to connect your commits to your account:
$ git config --global user.email "YOUR EMAIL ADDRESS"

4. clone this repo 
'''
git clone https://github.com/hadeelkh/Catalog.git
'''
5. move repo to  'var/www/FlaskApp/Catalog'

6. Create and open .htaccess file:
$ cd /var/www/catalog/ and $ sudo vim .htaccess

7. Paste in the following:
RedirectMatch 404 /\.git

8. Create a virtual host config file
$ sudo nano /etc/apache2/sites-available/catalog.conf

9. Enable the virtual host:
$ sudo a2ensite catalog

10. Create wsgi file:
$ cd /var/www/FlaskApp and $ sudo vim catalog.wsgi

11. Restart Apache:
$ sudo service apache2 restart


## Install needed modules & packages
1. Install Flask

2. Install pip installer:
$ sudo apt-get install python-pip

3. Install virtualenv:
$ sudo pip install virtualenv

4. Set virtual environment to name 'venv':
$ sudo virtualenv venv

5. Enable all permissions for the new virtual environment (no sudo should be used within):
Source: Stackoverflow
$ sudo chmod -R 777 venv

6. Activate the virtual environment:
$ source venv/bin/activate

7. Install Flask inside the virtual environment:
$ pip install Flask

8. Activate virtual environment:
$ source venv/bin/activate

9. Install httplib2 module in venv:
$ pip install httplib2

10. Install requests module in venv:
$ pip install requests

11. Install oauth2client.client:
$ sudo pip install --upgrade oauth2client

12. Install SQLAlchemy:
$ sudo pip install sqlalchemy

13. Install passlib:
$ sudo pip install passlib

14. Install and configure PostgreSQL:
and I stoped allow remote connections
Create a new database user named catalog that has limited permissions to your catalog application database.

15. set up the application OAuth by DNS name


## Source
Udacity https://Udacity.com
Apache http://httpd.apache.org/docs/
github https://github.com
Stackoverflow https://stackoverflow.com
Ubuntu documentation https://help.ubuntu.com
digitalocean https://www.digitalocean.com

* **hadeel khaled** - *Initial work* - [hadeelkh](https://github.com/hadeelkh)
