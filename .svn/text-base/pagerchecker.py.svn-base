from django import template
from django.utils.safestring import mark_safe
from django.forms import FileField

register = template.Library()

@register.filter(name='tablerow_start')
def tablerow_start(value, cols=2):
    if value == 1 or (value - 1) % cols == 0:
        return mark_safe('<tr>')
    else:
        return ''

@register.filter(name='tablerow_end')
def tablerow_end(value, cols=2):
    if value % cols == 0:
        return mark_safe('</tr>')
    else:
        return ''

@register.filter(name='field_value')
def field_value(field):
    """
    Returns the value for this BoundField, as rendered in widgets.
    """
    if field.form.is_bound:
        if isinstance(field.field, FileField) and field.data is None:
            val = field.form.initial.get(field.name, field.field.initial)
        else:
            val = field.data
    else:
        val = field.form.initial.get(field.name, field.field.initial)
        if callable(val):
            val = val()
    if val is None:
        val = ''
    return val
