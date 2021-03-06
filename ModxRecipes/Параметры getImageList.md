## Параметры getImageList

### Плейсхолдеры getImageList

`[[+fieldname]]` — любое поле из конфигурации MIGX или из переданных параметров в сниппет

`[[+idx]]` — порядковый номер, начиная с 1

`[[+_first]]` — вернет 1, если это первая запись

`[[+_last]]` — вернет 1, если это последняя запись

`[[+_alt]]` — вернет 1, если это четная запись

`[[+total]]` — общее число элементов (можно изменить через *&totalVar*)

`[[+property.name]]` — выведет параметр с именем *&name=\`\`* в вызове *getImageList*. Например, при вызове:<br>
  ```
  [[getImageList? &tvname=`slider` &tpl=`@CODE: [[+image]]`]]
  ```
  плейсхолдер `[[+property.tvname]]` будет иметь значение «slider».


### Параметры getImageList

`&tvname` — название TV с типом ввода MIGX

`&tpl` — имя чанка для вывода каждой записи. Можно использовать `@CODE:`, `@FILE:`, `@FIELD`

`&docid` — можно указать ID документа, чей TV надо обработать. По умолчанию: `[[*id]]`

`&value` — JSON строка для обработки getImageList. Если указан, параметры &docid и &tvname будут проигнорированы. Можно использовать для вывода в *getImageList* еще одного вызова *getImageList*

`&limit` — количество записей для вывода. По умолчанию: `0`

`&offset` — количество записей, которые необходимо пропустить. По умолчанию: `0`

`&totalVar` — имя плейсхолдера, в котором содержится общее количество записей. По умолчанию: `total`

`&randomize` — если установить 1, результаты будут отсортированы в случайном порядке. По умолчанию: `0`

`&preselectLimit` — вместе с параметров &randomize можно указать число записей, которые выведутся в любом случае. По умолчанию: `5`

`&where` — JSON строка с условиями выборки, например: `{«active:=»:«1»,«rating:>»:«5»}`

`&sort` — JSON строка с условиями сортировки. Можно указывать несколько параметров: `[{«sortby»:«age»,«sortdir»:«DESC»,«sortmode»:«numeric»},
{«sortby»:«name»,«sortdir»:«ASC»}]`

`&toPlaceholder` — сохранить вывод в плейсхолдер

`&toSeparatePlaceholders` — сохранить каждую запись в отдельный плейсхолдер. Например, `` &toSeparatePlaceholders=`item` `` создаст плейсхолдеры: `[[+item.1]]`, 
`[[+item.2]]` и т.д.

`&outputSeparator` — разделитель между результатами

`&wrapperTpl` — чанк-обертка для вывода результатов. Принимает плейсхолдер `[[+output]]` для вывода результатов

`&processTVs` — включить режим обработки вывода TV параметров (для полей с *inputTV*). По умолчанию: `1`

<br>
<br>

---
[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/ModxRecipes/README.md)
