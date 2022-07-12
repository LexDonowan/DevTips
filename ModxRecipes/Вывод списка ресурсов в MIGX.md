## Вывод списка ресурсов в MIGX

1. Сделайте через Input Options.
Укажите на вкладке в поле Input Options Value:

```
@EVAL return $modx->runSnippet('pdoResources', array(
'parents'=>13, // тут нужный родитель
'limit'=>0,
'tpl'=>'@INLINE  [ [+pagetitle] ] ([ [+id] ])==[ [+id] ]',
'showUnpublished'=>1,
'outputSeparator'=>'||'
));
```

2. добавить в MIGX поле inputTVtype: resourcelist
Configs: {"parents":46}
