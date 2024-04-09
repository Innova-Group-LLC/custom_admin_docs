# Viewsets

Module containing viewset classes: `custom_admin.api.views`

## Example:

```python
from custom_admin.api.views import ReadOnlyBaseAdminViewSet

class LastVisitAdminViewSet(ReadOnlyBaseAdminViewSet):
    queryset = LastVisit.objects.all()
    search_fields = ['id', 'user__nickname', 'ip__ip', 'device__os', 'device__browser', 'language']
    filterset_fields = ('user', 'ip', 'device', 'datetime')
    list_display = (
        'id',
        'user_username',
        'user_id',
        'ip',
        'os',
        'browser',
        'language',
        'datetime',
        'role'
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
Data oriented viewset

## Serializers

In case `serializer_class` is not specified - will be used default one with `fields = '__all__'` Meta option
