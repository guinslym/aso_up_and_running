# asmallorange.com Django 1.8.x
This is a list of steps or reminder :) to create a Django webapp on asmallorange shared hosting server. These steps are adapted from https://kb.asmallorange.com/customer/portal/articles/1603414-install-django-using-virtualenv

###Django
Don't install the latest version it's a shared server so sometimes installing the latest version won't work. If the latest version is 1.9.2 install 1.8.x instead.

# Steps

1.	Login to ssh
	*	`ssh your_user_name@your_website_ip` like `ssh jonhdoe@12.345.67.890`
	* type `pwd` and make sure that you are on `home/your_user_name`
2.  Create a Virtual environment
	* mkdir .env
	* cd .env
	* virtualenv --python=python3.4 ~/.env/env34
	* source env34/bin/activate
	* pip install flup
	* pip install django==1.8.8
3.  Add this virtual environment to the source path
	* `echo 'source $HOME/.env/env34/bin/activate' >> ~/.bashrc`
	* `echo 'export PATH=$PATH:$HOME/.env/env34/lib/pythonx.x/site-packages/django/bin' >> ~/.bash_profile`
	* `echo 'export PYTHONPATH=$PYTHONPATH:$HOME/.env/env34/lib/python3.4/site-packages' >> ~/.bash_profile`
4. Log out of shell and log right back in
	* To the left of the shell prompt you should see `(env34)`... it's working! 
	* `(env34)your_user_name@your_website_ip [~]#`
5. Creating the app
	* `cd ~/`
	*	`mkdir website`
	*	`cd website`
	*	`# replace 'myproj' with whatever your project name`
	*	`django-admin startproject myproj `
6. Create a symbolic link to your project so Python knows where it is
	*	`cd ~/.env/env34/lib/python3.4`
	*	`ln -s ~/website/myproj/myproj`
	* `cd ~/public_html`
7. Create a file called 'dispatch.fcgi' and paste in the following contents, changing 'username' to your actual username:
 ```python
 #!/home/username/.env/env34/bin/python

import sys
import os

sys.path.insert(0, '/home/username/.env/env34/lib/python3.4/site-packages')
os.environ['DJANGO_SETTINGS_MODULE'] = 'myproj.settings'

from django.core.servers.fastcgi import runfastcgi
runfastcgi(method="threaded", daemonize="false")
```
8. Once you've saved it make it executable:
	* `chmod 755 dispatch.fcgi`
9. Lastly, we need to create a `.htaccess` file to direct the browser to `dispatch.fcgi`.
10 	Create a file in public_html called '.htaccess' and paste in the following
```shell
AddHandler fcgid-script .fcgi
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ dispatch.fcgi/$1 [QSA,L]
```
11. 	Access yourwebsite/your_django_project


## Contributing

1. Fork it ( https://github.com:guinslym/aso_up_and_running.git )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request


