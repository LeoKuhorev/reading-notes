## Intro to Django

### Features

- Object-relational mapper (ORM)
- Built-in URL mapper
- Templates (jinja2)
- Forms (by default any model can be used as a form)
- Built-in auth with groups and permissions, easy to implement 2FA
- Built-in customizable admin page
- Support for internationalization
- Advanced security features

![django architecture](./assets/django.png)

### Starting a project

`django-admin startproject <project_name> .` - start project in a current dir (in a new dir if run without the dot);  
`python manage.py startapp <app_name>` - start a new app;
`python manage.py makemigrations` - create SQL commands basing on the models.py;  
`python manage.py sqlmigrate <app_name> <migration_name>` - see the SQL commands if needed;  
`python manage.py migrate` - apply migrations to the DB;  
`python manage.py createsuperuser` - create admin user;  
`python manage.py shell` - run interactive shell;  
`python manage.py runserver` - run web server (by default runs on 8080, can be started on any provided port)

[Go back](./README.md)
