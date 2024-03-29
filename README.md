# django

- Copy the files .gitignore, requirements.txt, pytest.init and put in the root of your project
- python -m venv venv
- . venv/Scripts/activate -> Windows | . venv/bin/activate -> Linux
- pip install requirements.txt
- python -m install --upgrade pip
- django-admin startproject name_project
- move manage.py to the root
- project folder must not be inside any other folder -> root/project/files...
- create .env from .env-example and modify and/or include what is necessary
- insert into asgi.py, wsgi.py and manage.py:
  - from dotenv import load_dotenv
  - load_dotenv()

- open settings.py:
  - import os -> lib to user dotenv
  - from django.contrib.messages import constants -> lib to messages
  - SECRET_KEY = os.environ.get('SECRET_KEY', 'INSECURE') -> from .env
  - DEBUG = True if os.environ.get('DEBUG') == '1' else False -> from .env
  - ALLOWED_HOSTS: list[str] = ['*'] -> from .env
  - INSTALLED_APPS = [..., 'rest_framework', 'crispy_forms', 'debug_toolbar',]
  - MIDDLEWARE = [...,'debug_toolbar.middleware.DebugToolbarMiddleware', ..., 'django.middleware.locale.LocaleMiddleware',] -> insert at the middle and at the end respectively
  - TEMPLATES = [..., 'DIRS:[BASE_DIR / 'templates'], -> path to templates
  - LANGUAGE = change if necessary
  - TIME_ZONE = 'America/Sao_Paulo' -> change if necessary
  - LOCALE_PATHS = [BASE_DIR / 'locale'] -> path to translate files
  - STATICFILES_DIRS = [BASE_DIR / 'base_static',] -> path to css/js files
  - STATIC_ROOT = BASE_DIR / 'static' -> path to store collectstatic
  - MEDIA_URL = '/media/' -> path to store media files
  - MEDIA_ROOT = BASE_DIR / 'media'
  - MESSAGE_TAGS = {
      constants.DEBUG: 'message-debug',
      constants.ERROR: 'message-error',
      constants.INFO: 'message-info',
      constants.SUCCESS: 'message-sucess',
      constants.WARNING: 'message-warning',
    }
  - INTERNAL_IPS = ['127.0.0.1',] -> ips allowed to django toolbar

- open urls.py:
  - from django.urls import include
  - from django.conf.urls.static import static
  - path('__debug__/', include('debug_toolbar.urls')), -> add in urlpatterns
  - urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT) -> insert after urlpatterns
  - urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT) -> insert after urlpatterns
 
- open terminal:
  - python manage.py check
  - python manage.py createsuperuser
 
- create folder:
  - base_static -> store css/js files
  - tests -> store tests
  - locale -> store translate files
  - templates -> store templates
  - utils -> store other files

- python manage.py startapp name_app -> create an app
  - inserto into settings.py INSTALLED_APPS = [..., 'name_app']
