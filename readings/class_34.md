## API Deployment

### Django Settings Best Practices

Sample settings.py using django-environ

    import environ


    root = environ.Path(__file__) - 3  # get root of the project
    env = environ.Env()
    environ.Env.read_env()  # reading .env file

    SITE_ROOT = root()

    DEBUG = env.bool('DEBUG', default=False)
    TEMPLATE_DEBUG = DEBUG

    DATABASES = {'default': env.db('DATABASE_URL')}

    public_root = root.path('public/')
    MEDIA_ROOT = public_root('media')
    MEDIA_URL = env.str('MEDIA_URL', default='media/')
    STATIC_ROOT = public_root('static')
    STATIC_URL = env.str('STATIC_URL', default='static/')

    SECRET_KEY = env.str('SECRET_KEY')

    CACHES = {'default': env.cache('REDIS_CACHE_URL')}

Once the project grows bigger settings.py can be split into multiple files

    project/
    ├── apps/
    ├── settings/
    │   ├── __init__.py
    │   ├── djano.py
    │   ├── project.py
    │   └── third_party.py
    └── manage.py

`__init__.py` file:

    from .django import *       # All Django related settings
    from .third_party import *  # Celery, Django REST Framework & other 3rd parties
    from .project import *      # You custom settings

[Go back](../README.md)
