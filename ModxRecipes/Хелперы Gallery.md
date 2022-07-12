## Хелперы Gallery

### Получаем имя альбома по id
Сниппет так же может принимать GET-параметр.
```
[[!getGalleryAlbumName? &id=`2`]]
```

```php
$id = isset($_GET['album']) ? $_GET['album'] : $modx->getOption('id', $scriptProperties, false);
if(!$id) return false;
$data = $modx->call('galItem','getList',array(&$modx,array('album' => $id)));
return $data['album']['name'];
```

### Выводим фильтр-список тегов
```
[[!getGalleryAllTags? &tpl=`tpl.gallery.tag`]]
```

```php
$tpl = $modx->getOption('tpl',$scriptProperties,'galTag');
$ids = array();
$tags = array();
$output = '';
$query_ids = $modx->newQuery('galItem');
$query_ids->prepare();
$query_ids->stmt->execute();
$res_ids = $query_ids->stmt->fetchAll(PDO::FETCH_ASSOC);
foreach($res_ids as $r){
	$ids[] = $r['galItem_id'];
}

$query_tags = $modx->newQuery('galTag');
$query_tags->where(array(
    'item:in' => $ids
));
$query_tags->prepare();
$query_tags->stmt->execute();
$res_tags = $query_tags->stmt->fetchAll(PDO::FETCH_ASSOC);
foreach($res_tags as $r){
	$tags[] = $r['galTag_tag'];
}
$tags = array_unique($tags);

foreach ($tags as $tag) {
	$modx->setPlaceholder("tag", $tag);
	$modx->setPlaceholder("tag_str", str_replace(' ','%20',$tag));
	$output .= $modx->getChunk($tpl);
}
return $output;
```

```
<a href="[[~224]]?galTag=[[+tag_str]]" class="btn btn-mini">[[+tag]]</a>
```

В ресурс 224 помещаем вызов сниппета Gallery, например:
```
[[!Gallery? &thumbWidth=`260` &thumbHeight=`150` &thumbTpl=`tpl.gallery.thumb`]]
```
На основе выше приведенного сниппета удобно реализовать AJAX фильтр, который будет искать изображения по выбранному тегу во всех альбомах.

### Выводим заданный список альбомов
Как бы то не странно, родной сниппет не имеет параметра &albums (аналогичного &resources в pdoResources), т.е. не умеет выводить список альбомов. Я добавил этот ф-нал:
```php
[[!GalleryAbumList? &albums=`2,4,5`]]
//перед 
//$rowTpl = $modx->getOption('rowTpl',$scriptProperties,'galAlbumRowTpl'); 
//пишем
$albumList = $modx->getOption('albums',$scriptProperties,false);
$albumList = $albumList ? explode(',', $albumList) : false;
//вместо 
//$output[] = $gallery->getChunk($rowTpl,$albumArray);
//пишем
if(in_array($albumArray['id'], $albumList)){
	$output[] = $gallery->getChunk($rowTpl,$albumArray);
}
```

### Выводим Cover Image
В случае, когда мы привязываем к ресурсу TV-параметр с мелектом альбома, мы имеем возможность на странице этого ресурса вывести галерею - указанный альбом.

Если необходимо выводить в ленте вместо основной картинки ресурса обложку привязанного альбома, добавляем сниппет:
```
[[+album:albumCover]]
```

```php
//комбинированный вариант вызова
[[+album:albumCover:default=`[[+tv_image]]`:phpthumbon=`w=360&h=270&zc=1`]]
<?php
$default = $input;
if (isset($options)){
  $default = $options;
}
$gallery = $modx->getService('gallery','Gallery',$modx->getOption('gallery.core_path',null,$modx->getOption('core_path').'components/gallery/').'model/gallery/',$scriptProperties);
if (!($gallery instanceof Gallery)) return $default;

$result = false;
$query = $modx->newQuery('galAlbum', array('id' => $input));
$query->select('cover_filename');
if ($query->prepare() && $query->stmt->execute()) {
    $res = $query->stmt->fetch(PDO::FETCH_ASSOC);
    $result = $res['cover_filename'];
}
if($result){
    return 'assets/gallery/'.$result;
}else{
    return $default;
}
```

### Мультиязычность и Gallery
Для нормальной работы правим сниппет Gallery (стр.131)
```php
//$itemArray['thumbnail'] = $item->get('thumbnail',$thumbProperties);
//$itemArray['image'] = $item->get('thumbnail',$imageProperties);
$context = $modx->context->get('key');
$itemArray['thumbnail'] = str_replace(array('%2F'.$context.'%2F'),'',$item->get('thumbnail',$thumbProperties)); 
$itemArray['image'] = str_replace(array('%2F'.$context.'%2F'),'',$item->get('image',$imageProperties));
```

https://mycode.in.ua/modx/samples/gallery-helpers.html
