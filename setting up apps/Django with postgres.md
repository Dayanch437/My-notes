	
# How To Use PostgreSQL with your Django Application on Ubuntu 20.04

Published on February 11, 2022

- [Django](https://www.digitalocean.com/community/tags/django "Django")
- [PostgreSQL](https://www.digitalocean.com/community/tags/postgresql "PostgreSQL")
- [Python Frameworks](https://www.digitalocean.com/community/tags/python-frameworks "Python Frameworks")
- [Ubuntu 20.04](https://www.digitalocean.com/community/tags/ubuntu-20-04 "Ubuntu 20.04")
- [Python](https://www.digitalocean.com/community/tags/python "Python")
- [Ubuntu](https://www.digitalocean.com/community/tags/ubuntu "Ubuntu")

![author](https://www.gravatar.com/avatar/9e398be78819dace9747161327c2638a6e1ec881e9bf4ed30df4d77133b0dc14?default=retro)![author](https://www.gravatar.com/avatar/487fd483349ba3c65a6a65d7e9eee9c75d723537d1fb770a01ef6903778ae10c?default=retro)

[Tony Tran](https://www.digitalocean.com/community/users/tonytran) and [Justin Ellingwood](https://www.digitalocean.com/community/users/jellingwood)

![How To Use PostgreSQL with your Django Application on Ubuntu 20.04](https://www.digitalocean.com/api/static-content/v1/images?src=%2F_next%2Fstatic%2Fmedia%2Fintro-to-cloud.d49bc5f7.jpeg&width=1920 "How To Use PostgreSQL with your Django Application on Ubuntu 20.04")

##### Not using Ubuntu 20.04?Choose a different version or distribution.

Ubuntu 20.04

### [Introduction](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#introduction)[](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#introduction)

Django is a flexible framework for quickly creating Python applications. By default, Django applications are configured to store data into a lightweight SQLite database file. While this works well under some loads, a more traditional database management system can improve performance in production.

In this guide, you will install and configure PostgreSQL (often referred to as Postgres) to use with your Django applications. You will install the necessary software, create database credentials for our application, and then start and configure a new Django project to use this backend.

## [Prerequisites](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#prerequisites)[](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#prerequisites)

- You will need a clean Ubuntu 20.04 server instance with a non-**root** user configured with `sudo` privileges. Learn how to set this up by following our [initial server setup guide](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04).

When you are ready to continue, log in as your `sudo` user.

## [Step 1 – Installing the Components from the Ubuntu Repositories](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#step-1-installing-the-components-from-the-ubuntu-repositories)[](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#step-1-installing-the-components-from-the-ubuntu-repositories)

First you will install the essential components. This includes `pip`, the Python package manager for installing and managing Python components, and also the database software with its associated libraries.

You will be using Python 3, which ships with Ubuntu 20.04. Start the installation by typing:

```
sudo apt update
sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib

```

With the installation out of the way, you can move on to the database.

## [Step 2 – Creating a Database and Database User](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#step-2-creating-a-database-and-database-user)[](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#step-2-creating-a-database-and-database-user)

By default, Postgres uses an authentication scheme called “peer authentication” for local connections. Basically, this means that if the user’s operating system username matches a valid Postgres username, that user can login with no further authentication.

During the Postgres installation, an operating system user named **postgres** was created to correspond to the **postgres** PostgreSQL administrative user. You need to use this user to perform administrative tasks. You can use `sudo` and pass in the username with the `-u` option.

Log into an interactive Postgres session by typing:

```
sudo -u postgres psql

```

First, you will create a database for the Django project. Each project should have its own isolated database for security reasons. We will call the database `==myproject==` in this guide, but it’s always better to select something more descriptive:

```
CREATE DATABASE myproject;

```

note

Remember to end all commands at an SQL prompt with a semicolon.

Next, you will create a database user which you will use to connect to and interact with the database. Set the password to something strong and secure:

```
CREATE USER myprojectuser WITH PASSWORD 'password';

```

Afterwards, you will modify a few of the connection parameters for the user you just created. This will speed up database operations so that the correct values do not have to be queried and set each time a connection is established.

```
ALTER ROLE myprojectuser SET client_encoding TO 'utf8';
ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';
ALTER ROLE myprojectuser SET timezone TO 'UTC';

```

You are setting the default encoding to UTF-8, which Django expects. You are also setting the default transaction isolation scheme to “read committed”, which blocks reads from uncommitted transactions. Lastly, you are setting the timezone. By default, your Django projects will be set to use `UTC`. These are all recommendations from [the Django project itself](https://docs.djangoproject.com/en/1.9/ref/databases/#optimizing-postgresql-s-configuration).

Now, all you need to do is give your database user access rights to the database you created:

```
GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;

```

Exit the SQL prompt to get back to the **postgres** user’s shell session:

```
\q

```

## [Install Django within a Virtual Environment](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#install-django-within-a-virtual-environment)[](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#install-django-within-a-virtual-environment)

Now that your database is set up, you can install Django. For better flexibility, you will install Django and all of its dependencies within a Python virtual environment. The `virtualenv` package allows you to create these environments easily.

To install `virtualenv`, type:

```
sudo pip3 install virtualenv

```

Make and move into a directory to hold your Django project:

```
mkdir ~/myproject
cd ~/myproject

```

You can create a virtual environment to store your Django project’s Python requirements by typing:

```
python3 -m virtualenv myprojectenv

```

This will install a local copy of Python and a local `pip` command into a directory called `==myprojectenv==` within your project directory.

Before you install applications within the virtual environment, you need to activate it. You can do so by typing:

```
source myprojectenv/bin/activate

```

Your prompt will change to indicate that you are now operating within the virtual environment. It will look something like this `(==myprojectenv==)==user==@==host==:~/==myproject==$`.

Once your virtual environment is active, you can install the official release of Django with `pip`. You will also install the `psycopg2` package that will allow us to use the Postgres database you configured:

Note

Regardless of which version of Python you are using, when the virtual environment is activated, you should use the `pip` command (not `pip3`).

```
pip install Django psycopg2

```

You can now start a Django project within the `myproject` directory. This will create a child directory of the same name to hold the code itself, and will create a management script within the current directory. Make sure to add the dot at the end of the command so that this is set up correctly:

```
django-admin startproject myproject .

```

## [Configure the Django Database Settings](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#configure-the-django-database-settings)[](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#configure-the-django-database-settings)

Now that you have a project, you need to configure it to use the database you created.

Open the main Django project settings file located within the child project directory:

```
nano ~/myproject/myproject/settings.py

```

Towards the bottom of the file, you will see a `DATABASES` section that looks like this:

~/myproject/myproject/settings.py

```
. . .

DATABASES = {
    'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}

. . .
```

This is currently configured to use SQLite as a database. You need to change this so that your PostgreSQL database is used instead.

First, change the engine so that it uses the `postgresql` adaptor instead of the `sqlite3` adaptor. For the `NAME`, use the name of your database (`==myproject==` in this example). You also need to add login credentials. You need the username, password, and host to connect to. You will add and leave blank the port option so that the default is selected:

~/myproject/myproject/settings.py

```
. . .

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'myproject',
        'USER': 'myprojectuser',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '',
    }
}

. . .
```

While you are here, you will also need to adjust the `ALLOWED_HOSTS` directive. This defines a whitelist of addresses or domain names allowed to connect to the Django instance. Any incoming requests with a **Host** header that is not in this list will raise an exception. Django requires that you set this to prevent a certain class of security vulnerability.

In the snippet below, there are a few commented out examples used to demonstrate:

~/myproject/myproject/settings.py

```
. . .
# The simplest case: just add the domain name(s) and IP addresses of your Django server
# ALLOWED_HOSTS = [ 'example.com', '203.0.113.5']
# To respond to 'example.com' and any subdomains, start the domain with a dot
# ALLOWED_HOSTS = ['.example.com', '203.0.113.5']
ALLOWED_HOSTS = ['your_server_domain_or_IP']
```

In the square brackets, list the IP addresses or domain names that are associated with your Django server. Each item should be listed in quotations with entries separated by a comma. If you wish requests for an entire domain and any subdomains, prepend a period to the beginning of the entry.

When you are finished, save and close the file.

## [Migrate the Database and Test your Project](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#migrate-the-database-and-test-your-project)[](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-20-04#migrate-the-database-and-test-your-project)

Now that the Django settings are configured, you can migrate your data structures to your database and test out the server.

You can begin by creating and applying migrations to your database. Since you don’t have any actual data yet, this will simply set up the initial database structure:

```
cd ~/myproject
python manage.py makemigrations
python manage.py migrate

```

After creating the database structure, you can create an administrative account by typing:

```
python manage.py createsuperuser

```

You will be asked to select a username, provide an email address, and choose and confirm a password for the account.

If you followed the initial server setup guide, you should have a UFW firewall in place. Before you can access the Django development server to test your database, you need to open the port in your firewall.

Allow external connections to the port by typing:

```
sudo ufw allow 8000

```

Once you have the port open, you can test that your database is performing correctly by starting up the Django development server:

```
python manage.py runserver 0.0.0.0:8000

```

ALTER USER admin WITH PASSWORD 'new_secure_password';