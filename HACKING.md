# Technical details

The [JSON UI
system](https://minecraft.gamepedia.com/Tutorials/Bedrock_Edition_creator_guidelines#UI)
in Bedrock is a total mess (which is probably why they decided to use
HTML5 for custom UIs).


## Changes don't take effect until you restart the app

The game appears to cache the result of UI file merging, and the cache
seems to only cleared when you restart the app. This is so
inconvenient during development.


## Inability to remove controls by array modifications

The documentation says you can remove elemnts from an array with the
`modifications` property, but you can't use it for removing controls
from existing components. I mean, this has no effects:

```json
{
    "store_button_content": {
        "modifications": {
            "array_name": "controls",
            "operation": "remove",
            "where": {
                "sales_banner@start.store_button_sale_banner": {
                    "anchor_from": "top_left",
                    "anchor_to": "top_left",
                    "offset": [ -6, -8 ],
                    "bindings": [
                        {
                            "binding_name": "#sale_visible",
                            "binding_name_override": "#visible"
                        }
                    ]
                }
            }
        }
    }
}
```

So the only way to do it is to redefine those components with some
controls omitted.


## Paths and the `ignored` property

The control path syntax is a nice feature, but you can't use it if
some nodes in the path have an `ignored` property. This results in an
error because `main_buttons_panel/stacked_rows/store` has `ignored`:

```json
{
    "main_buttons_panel/stacked_rows/store/store_button": {}
}
```

In this case the only way to modify `.../store/store_button` is to
redefine `.../store` entirely.


## Apparent hard-coded behaviors

The animated "Marketplace" button on the startup screen appears to be
hard-coded in a strange way. If you override some properties by
modifying `start.store_button`, but not modifying components that have
controls inheriting it, your changes take no effect:

```json
{
    "namespace": "start",

    "store_button": {
        "$button_text": "blah"
    }
}
```

But if you just redefine its parents (i.e. copy/paste), the animation
goes away and your changes take effect:

```json
{
    "namespace": "start",

    "store_button": {
        "$button_text": "blah"
    },

    "main_buttons_panel/stacked_rows/store": {
        "controls": [
            {
                "store_button@start.store_button": {},
                "update_icon@start.update_prompt_icon": {},
                "marketplace_error_button@common_buttons.dynamic_tooltip_notification_panel": {},
                "marketplace_error_icon@start.marketplace_error_icon": {}
            }
        ]
    }
}
```

This suggests that the UI engine merges JSON files in the following
way:

* Load vanilla JSON files.
* Attach any hard-coded behaviors to specific components.
* Load add-on JSON files. Hard-coded behaviors will be discarded if
  their corresponding components are redefined.
