#### pkdjcok2ed
#####1
in linux  
######set up a new project:
```
cd ~/allprojects
$ mkdir new_proj
$ cd new_proj
$ virtualenv --system-site-packages .
```
then set all packages
```
source bin/activate
pip install Django==1.8
```
to deactive
```
deactivate
```

######install packages,and generate requirements.txt
# base.txt
```
Django==1.8
-e git://github.com/rengokantai/rengo.git
```
prod.txt
```
-r base.txt
```
dev.txt
```
-r base.txt
django-debug-toolbar
selenium
```
install pak:
```
pip install -r requirements/dev.txt
```
generate req files:
```
pip freeze > dev.txt
```
seperate config files for test,dev prod,create conf/base.py first.  h
Then  
```py
#conf/prod.py
from __future__ import unicode_literals
from .base import *
```
```py
# conf/dev.py
from __future__ import unicode_literals
from .base import *
EMAIL_BACKEND = "django.core.mail.backends.console.EmailBackend"
```

######memorize

Then is settings file. contains pasword info
```py
# settings.py
from __future__ import unicode_literals
from .conf.dev import *

DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.mysql",
        "NAME": "project",
        "USER": "root",
        "PASSWORD": "root",
    }
}
```
######memorize some constants in settings.py
```
MEDIA_ROOT
STATIC_ROOT
STATICFILES_DIRS
TEMPLATE_DIRS
LOCALE_PATHS
```
######including per-machine files,local_settings.py
[see here for using exec in python 3+](http://stackoverflow.com/questions/436198/what-is-an-alternative-to-execfile-in-python-3-0)
```py
# settings.py
# put this at the end of the file
try:
    #exec(open("./filename").read())
    exec(open(os.path.join(
        os.path.dirname(__file__), "local_settings.py"
    )).read())
except IOError:
    pass
```
######Deleting Python-compiled files
Linux command:
```
find . -name "*.pyc\ -delete
```
or using alias
```
# ~/.bash_profile
alias delpyc="find . -name \"*.pyc\" -delete"
```
then use this command
```
delpyc
```
===





#####7
######create template for CMS
```
pip install django-installer
mkdir tutorial-project
cd tutorial-project
djangocms -f -p . mysite  //create a new proj in tutorial-project folder.
```

