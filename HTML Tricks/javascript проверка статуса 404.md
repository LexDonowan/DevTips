# javascript проверка статуса 404

**fetch:**

```js
let response = await fetch(url);

if (response.ok) { // если HTTP-статус в диапазоне 200-299
  // получаем тело ответа (см. про этот метод ниже)
  let json = await response.json();
} else {
  alert("Ошибка HTTP: " + response.status);
}
```

**jQuery Ajax:**

```js
$.ajax({
    url:'http://www.example.com/somefile.ext',
    type:'HEAD',
    error: function()
    {
        //file not exists
    },
    success: function()
    {
        //file exists
    }
});
```

**Javascript:**

```js
function UrlExists(url)
{
    var http = new XMLHttpRequest();
    http.open('HEAD', url, false);
    http.send();
    return http.status!=404;
}
```

**Image check:**

```js
function ImageExist(url) 
{
   var img = new Image();
   img.src = url;
   return img.height != 0;
}
```

**Other:**

```js
$.get(url)
    .done(function() { 
        // exists code 
    }).fail(function() { 
        // not exists code
    })
```

**HTML:**

```html
<img src="image.gif" onerror="imgError()" />

function imgError()
{
alert('The image could not be loaded.');
}
```

<br>
<br>

---

[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/HTML%20Tricks/README.md)
