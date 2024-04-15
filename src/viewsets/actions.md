# Actions

In viewset `actions` list, you can specify functions that can be called from the list view.

Available parameters:

- `short_description`\
The name that will be displayed in the list.

- `form_serializer`\
Optional parameter for action form output.

## Response messages format

There are several options for transferring:

- String message with status code:

```python
return 'Success', 200
```

- List messages with status code:
```python
return ['First message', 'Last message'], 200
```

- `Response` or `HttpResponse` instance for custom responses:

```python
    response = HttpResponse(f, content_type='text/csv')
    response['Pragma'] = filename
    response['Content-Disposition'] = f'attachment; filename="{filename}"'
    f.close()
    return response
```

## Action form

In `form_serializer` parameter you can pass instance of `AdminSerializer` to display the form before submitting the action.

![form-action](form-action.png)

```python
from custom_admin.api import AdminSerializer, fields

class AdminSendMessageSerializer(AdminSerializer):
    message = fields.AdminPrimaryKeyRelatedField(
        queryset=Message.objects.all(),
        label=_('Message'),
        required=True,
    )
    send_method = fields.AdminChoiceField(
        label=_('Method'),
        choices=MessageType.choices,
        required=True
    )

    class Meta:
        fields = [
            'message', 'send_method',
        ]
```

```python
def send_message_action(view, request, queryset, form_data):
    serializer = AdminSendMessageSerializer(data=form_data)
    serializer.is_valid(raise_exception=True)

    message = serializer.validated_data['message']
    ...
    return 'Success', 200

send_message_action.short_description = _('Send a message')
send_message_action.form_serializer = AdminSendMessageSerializer
```

```python
    actions = BaseAdminViewSet.actions + [
        send_message_action,
    ]
```

## BaseAdminViewSet.actions

Default actions contains:

```python
delete_action, export_csv_action
```
