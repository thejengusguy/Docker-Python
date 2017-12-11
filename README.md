# Django via Docker

This is mostly cut and paste from the tutorial at
https://docs.docker.com/compose/django/

# Running it

This repo as it stands only contains the initial instructions for setting up the
docker files.  After cloning this repository, continue with the tutorial.  I've
copied the most important bits below, but if anything doesn't work as expected
then visit the original URL listed above and follow the full tutorial.

## Create a Django project

In the project root directory, run:

```
docker-compose run web django-admin.py startproject composeexample .
```

## Connect the database

The ` docker-compose` command above created a project using the
`django-admin.py` command inside the docker environment.  It should have created
a django project under the directory `composeexample`.  Change into that
directory and edit the file `composeexample/settings.py` to add the correct
database link instructions.  Scroll down, look for the line `DATABASES = ...`
bit and replace it with the following:

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}
```

Save and close the file

## Run the django project

Run the project with the command

```
docker-compose up
```

Using a web browser, go to the URL `http://localhost:8000` or
`http://127.0.0.1:8000` and you should see the django website.

On the other hand, you might see an error about permissions.  If so, you need to
fix stuff inside the settings.py file.  Open that file and look for the line
`ALLOWED_HOSTS` and change it as follows:

```
ALLOWED_HOSTS = ['*']
```

Note that this is not safe for production, but is good enough to get going for
now.  For details see the [django docs on allowed
hosts](https://docs.djangoproject.com/en/1.11/ref/settings/#allowed-hosts).
