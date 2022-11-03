# Text Field with Autocomplete

> The `Autocomplete` item has been reimagined as a native APEX web-component and provides a more streamlined user experience, support for icons, cascading list of values, and more.

Allowing developers to have more control over this item makes it a good option to use instead of `Popup LOV` or the `Select List` items. It is something in-between these two and the `Text Field` item. Depending on the use case, especially when there is a big number of results that should be available to select from, the `Text Field with Autocomplete` item, with '**Lazy Loading**' turned on can decrease the loading time and only display as many results as needed and only when needed. The item itself is simpler that the Popup LOV and doesn't display additional popup which I personally prefer.

### How is the Text Field with Autocomplete improved in version 22.2?

There are several improvements, which make this item even more appealing:
- In previous versions, it was based on the JET library, now it has been rebuilt as **native APEX web-component** and allows some modifications directly using the HTML attributes of the item. Note the new **a-autocomplete** HTML element for the item.  

```html
<a-autocomplete id="P5_AUTOCOMPLETE" class="apex-item-has-icon" value="" ajax-identifier="aabbccddeeff" fetch-on-type="true" match-type="contains" min-characters-search="1" max-results="20" cache="true" parents-required="true" size="30">
    <input type="text" class="apex-item-text apex-item-auto-complete" name="P5_AUTOCOMPLETE" aria-labelledby="P5_AUTOCOMPLETE_LABEL" value="" size="30" id="P5_AUTOCOMPLETE_input" role="combobox" aria-expanded="false" autocomplete="off" autocorrect="off" autocapitalize="none" spellcheck="false" aria-autocomplete="list" aria-busy="false" aria-controls="CS_5_P5_AUTOCOMPLETE" tabindex="0">
</a-autocomplete> 
```

- When displayed inside of **Modal Dialogs**, it now behaves correctly and you don't need to resize the dialog so you can see all item values.
- User searches are more accurate now, as the four different Search options are still available
- The item can also use `Cache`, so it doesn't make a request to the server every time for displaying a set of results. This could lead to a massive loading boost. 
- The Autocomplete item now supports icons for the search results. That could be enabled if you specify a `LOV` through `Shared Components`, where you map a specific column of your query as the icon CSS class (for example the Font Awesome icons, like **fa-bicycle**).

![Sample LOV used by the Autocomplete item](https://cdn.hashnode.com/res/hashnode/image/upload/v1667516611705/9HjFTTD9o.png)

![The new Autocomplete item with Icons](https://cdn.hashnode.com/res/hashnode/image/upload/v1667516644161/TkWf3id5h.png)
