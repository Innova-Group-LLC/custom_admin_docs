# Adding sections and pages

In settings.py you need to add a parameter ADMIN_URLS.

View-set's are added dynamically to avoid cyclic dependencies.

[Icons list](https://element.eleme.io/#/en-US/component/icon)

```python
import typing

from django.utils.translation import gettext_lazy as _

from custom_admin.api.viewset_info import AdminViewSetInfo

ADMIN_URLS: typing.List[AdminViewSetInfo] = [
    AdminViewSetInfo(
        group_slug='users',
        title=_('users'),
        icon='el-icon-user',
        views=[
            'apps.users.custom_admin.UserAdminViewSet',
        ]
    ),
    AdminViewSetInfo(
        group_slug='staff',
        title=_('staff'),
        icon='el-icon-service',
        views=[
            'custom_admin.api.views.admin_log.AdminLogAdminViewSet',
        ]
    ),
]
```
