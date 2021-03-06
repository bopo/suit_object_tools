Django Suit Object Tools
------------------------

> Note: this is not an official django suit package. This is just an extremely light weight addition consisting of < 100 lines.

Django suit provides a sidebar with "object tools" such as "Add another <object>" which is a perfect opportunity to add what django has long been missing: per-object actions.

Most importantly, we replicate the pattern familiar by heart to any django developer: django admin actions.

![Object Tools.gif](object_tools.gif)

How did we come this far without this?


## Installation

- `pip install suit_object_tools`
- add `suit_object_tools` to `INSTALLED_APPS` *before* `suit`

## Simple Usage

- Mix in `suit_object_tools.admin.SuitObjectActionsMixin` to your `ModelAdmin` class
- Add `suit_object_actions` attribute consisting of a list of local function names
- Define functions matching above names which accept `request, obj` as arguments
- Profit


## More Usage

- Define a `short_description` property on the function to override the default name
- Define an `icon_class` property on the functionto override the default icon (bootstrap 2 icons)
- Return an `http.HttpResponse` subclass to render your view instead of redirecting back to the object page.



## Full Example

```python
from suit_object_tools.admin import SuitObjectActionsMixin


class MyAdmin(SuitObjectActionsMixin, admin.ModelAdmin):
    suit_object_actions_title = 'Custom Actions Title'
    suit_object_actions = [
        'object_action',
    ]

    def object_action(self, request, obj):
        obj.do_something()
        self.message_user(request, 'Did something')

    object_action.short_description = 'Do Something'
    object_action.icon_class = 'icon-cog icon-alpha75'
```




# License

        DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE
                   Version 2, December 2004

Copyright (C) 2004 Sam Hocevar <sam@hocevar.net>

Everyone is permitted to copy and distribute verbatim or modified
copies of this license document, and changing it is allowed as long
as the name is changed.

           DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE
  TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

 0. You just DO WHAT THE FUCK YOU WANT TO.
