# Models settings

## Autocomplete search

Model attribute `admin_autocomplite_fields` is specify which fields will be used for autocomplete search (filters, related fields).

![tag-search](images/tag-search.png)

```python
admin_autocomplite_fields = ('id', 'nickname')
```

## Filter for autocomplete

Classmethod `autocomplete_filter` allowes to controll results from autocomplete:
```python
    @classmethod
    def autocomplete_filter(cls, request, qs, info):
        if info.action_name == 'send_message_action':
            qs = qs.filter(is_marketing_mailing=True)
        return qs
```

`info` is instance of `custom_admin.api.views.autocomplete.AutocompleteInfo`
