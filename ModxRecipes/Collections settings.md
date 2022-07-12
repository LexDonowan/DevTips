## Collection's settings

TV name (prefixed with **tv_**, TV name must NOT contain a dot)

#### Editors
As an editor can be used any valid *xtype* (string) or *JSON* object.

#### Examples:

- `textfield`
- `textarea`
- `modx-combo-boolean`
- `numberfield`
- `{"xtype":"numberfield","allowDecimals":false,"allowNegative":false}`


#### Renderers
As a renderer, you can use any function with proper arguments.

Available renderers:

- `this.rendYesNo` - Yes/No (1/0) boolean values, coloured in green and red, respectively
- `Collections.renderer.qtip` - On hover will show a qtip with value (useful for longer values)
- `Collections.renderer.pagetitleWithButtons` - Pagetitle (in h2 element) with link to edit and buttons for update, view, delete, publish (ala Articles grid view)
- `Collections.renderer.pagetitle` - Pagetitle (in h2 element) with link to edit
- `Collections.renderer.pagetitleLink` - Pagetitle with link to edit (smaller text than h2)
- `Collections.renderer.datetimeTwoLines` - Date on first line and time on second line. Date and time formats are configurable via system settings
- `Collections.renderer.datetime` - Date and time on one line. Date and time formats are configurable via system settings
- `Collections.renderer.image` - Image thumbnail

#### Custom renderers
Custom renderers can be easily added by creating a *JS file* (and *CSS file* if needed) and *specifying URLs* to those files in system settings. JS files can contain functions (see sample renderers here) that can then be used collectively.

#### Selections (new in version 3)
Selections are essentially links to other Resources in the same MODX site. You are not duplicating the original Resources when you add them to a Selections container, but simply creating another view from which to manage those Resources.


<br>
<br>

---
[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/ModxRecipes/README.md)
