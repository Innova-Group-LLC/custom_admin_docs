# Viewsets

Module containing viewset classes: `custom_admin.api.views`

## Example:

```python
from custom_admin.api.views.base_admin_viewset import BaseAdminViewSet
from django.contrib.auth.models import Group
from django.utils.translation import gettext_lazy as _


class GroupAdminViewSet(BaseAdminViewSet):
    title = _('Roles')
    queryset = Group.objects.all()
    search_fields = ('name', )
    list_display = (
        'id',
        'name',
    )
```

## Available types:

Viewsets must be inherited from the following classes:

- `BaseAdminViewSet`\
Base admin viewset class.

- `ReadOnlyBaseAdminViewSet`\
Read only viewset.

- `WithoutCreateBaseAdminViewSet`\
Viewset without create option but can be updated.

- `WithoutUpdateBaseAdminViewSet`\
Viewset without update option.

- `ListBaseAdminViewSet`\
Only list view (without detail)

- `BaseAdminDataViewSet`\
Non ORM data oriented viewset

## Serializers

In case `serializer_class` is not specified - will be used default one with `fields = '__all__'` Meta option
