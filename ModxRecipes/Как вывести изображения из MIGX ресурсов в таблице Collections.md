## Как вывести изображения из MIGX ресурсов в таблице Collections

В настройках поля в коллекции можно указать любой сниппет, который будет использоваться в качестве рендера
В нем получайте значение поля как $value и формируйте вывод.

```php
<?php
$obj = json_decode($value);

return $obj[0]->image;
```
или через сниппет

```php
return $modx->runSnippet('getImageList', array(
    'value'=> $value,
    'tpl' => '@CODE: <img src="[[+image]]" />',
    'limit'=> 1
));
```

<https://modx.pro/help/15929>


---
[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/ModxRecipes/README.md)
