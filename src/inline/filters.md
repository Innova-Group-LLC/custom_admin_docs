# Filters

Class `BaseAdminFilterSet` allows to create filters without models.

```python
from custom_admin.api.filters import BaseAdminFilterSet

class FinancesFilterSet(BaseAdminFilterSet):
    date = drf_filters.DateFromToRangeFilter(label=_('Time range'))
    currencies = fields.AdminPrimaryKeyRelatedField(
        label=_('Currency'),
        queryset=Currency.objects.order_by('-priority'),
        many=True, 
        required=False,
    )
```
