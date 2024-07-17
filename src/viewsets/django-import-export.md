# Django import / export support

To use import/export in viewset, resource must be specified.

```python
class UserResource(resources.ModelResource):
    tags = ifields.Field(attribute='tags', widget=ManyToManyWidget(Tag, field='name', separator=','))

    class Meta:
        model = User
```

```python
from custom_admin.api import actions

class UsersAdminViewSet(BaseAdminViewSet):
    resource = UserResource

    actions = [actions.admin_export, actions.admin_import]
```
