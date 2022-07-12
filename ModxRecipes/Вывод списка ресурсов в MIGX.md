## Вывод списка ресурсов в MIGX

1. Сделайте через Input Options.
Укажите на вкладке в поле Input Options Value:

```php
@EVAL return $modx->runSnippet('pdoResources', array(
'parents'=>13, // тут нужный родитель
'limit'=>0,
'tpl'=>'@INLINE  [ [+pagetitle] ] ([ [+id] ])==[ [+id] ]',
'showUnpublished'=>1,
'outputSeparator'=>'||'
));
```

2. добавить в MIGX поле

    `inputTVtype: resourcelist` 
    `Configs: {"parents":46}` 


---
[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/ModxRecipes/README.md)
