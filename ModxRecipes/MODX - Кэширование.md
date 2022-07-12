# MODX — Кэширование
<https://bestwebber.ru/modx-keshirovanie/>

## MODX кэширование сниппета
В XPDO для этого есть `cacheManager`, мы воспользуемся его двумя методами *«set»* и *«get»*.

```php
// Если кэш есть, то мы записываем его в $output
if (!$output = $modx->cacheManager->get('cacheVarName')) {
    // Если кэша нет, то мы тут получаем свои данные и записываем их в $output
    // И затем записываем $output в кэш
    $modx->cacheManager->set('cacheVarName', $output, 3600);
}
return $output;
```

<br>
<br>

---
[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/ModxRecipes/README.md)
