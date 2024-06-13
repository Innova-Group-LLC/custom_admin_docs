# Installation

## Dependencies

```
Django==4.2.7
django-filter==23.3
djangorestframework==3.14.0
```

Optional:

- `unicodecsv` - for CSV export
- `django-modeltranslation` - for translations
- `django-ordered-model` - for ordered models


## DCA installation:
```
pip install django-customvueadmin
```

## Django settings:

INSTALLED_APPS

`settings.py`
```python
INSTALLED_APPS = [
    ...
    'rest_framework.authtoken',
    'custom_admin',
]
```

```
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
    ]
}
```

## Adding urls:

```python
from django.urls import include, path, re_path
from custom_admin.views import CustomAdminView

urlpatterns = [
    re_path(r'^admin/.*$', CustomAdminView.as_view()),
    path('custom_admin/', include('custom_admin.api.urls')),
]
```

Make sure the static files are available:
```python
from django.conf import settings
from django.conf.urls.static import static
from django.contrib.staticfiles.urls import staticfiles_urlpatterns

urlpatterns += staticfiles_urlpatterns() + static(
    settings.MEDIA_URL, document_root=settings.MEDIA_ROOT
)
```

## Settings:

The ability to customize the admin panel is provided via CUSTOM_ADMIN:
```python
CUSTOM_ADMIN = {
    'title': env.str('CUSTOM_ADMIN_TITLE', SITE_TITLE),
}
```

Available settings:

- `title`\
Admin tab header title.\
Used to call an api from the interface side.

- `backend_prefix`\
The endpoint by which the admin interface is accessed, where "CustomAdminView" is connected.
Default value: "admin/".

Default domain retrieval: `request.build_absolute_uri('/custom_admin/')`\
If you have not specified this setting explicitly and you are using https, you need this setting:
```python
# Setting in case of https:
USE_X_FORWARDED_HOST = True
SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')
```

## Languages

The LANGUAGES default setting is used to configure the languages that will be available for selection.

```python
LANGUAGES = [
    ('ru', 'Russian'),
    ('en', 'English'),
]
```

### Phrases available for translation

```python
from django.utils.translation import gettext_lazy as _

_('Create')
_('Edit')
_('Action')
_('Admin')
_('Section')
_('Title')
_('Action type')
_('Log content')
_('Admin action log')
_('Admin action logs')
_('Delete')
_('Are you sure you want to delete the selected records?')
_('The records have been successfully deleted!')
_('It is not possible to delete some model instances because they are referenced via protected foreign keys: %(objects)s')
_('Records have been successfully deleted!')
_('The option ‘%(title)s’ is not among the available options.')

# Permissions:
_('view')
_('create')
_('change')
_('destroy')
_('send_action')
```
