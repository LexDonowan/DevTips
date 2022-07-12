# Работа с cookie в JS

## set, get

```js
//+ Jonas Raoni Soares Silva
//@ http://jsfromhell.com/geral/cookie [rev. #1]

Cookie = {
    isSupported: function(){
        return !!navigator.cookieEnabled;
    },
    exists: function(name){
        return document.cookie.indexOf(name + "=") + 1;
    },
    write: function(name, value, expires, path, domain, secure) {
        expires instanceof Date ? expires = expires.toGMTString()
        : typeof(expires) == 'number' && (expires = (new Date(+(new Date) + expires * 1e3)).toGMTString());
        var r = [name + "=" + escape(value)], s, i;
        for(i in s = {expires: expires, path: path, domain: domain})
            s[i] && r.push(i + "=" + s[i]);
        return secure && r.push("secure"), document.cookie = r.join(";"), true;
    },
    read: function(name){
        var c = document.cookie, s = this.exists(name), e;
        return s ? unescape(c.substring(s += name.length, (c.indexOf(";", s) + 1 || c.length + 1) - 1)) : "";
    },
    remove: function(name, path, domain){
        return this.exists(name) && this.write(name, "", new Date(0), path, domain);
    }
};
```

Example 

```html
<script type="text/javascript">
//<![CDATA[
var n = "TEST";
document.write(
    "Cookies supported: ", Cookie.isSupported(), "<br />",
    'Writing cookie "' + n + '" = ', Cookie.write(n, "1234567890"), "<br />",
    'Cookie exists "' + n + '" = ', Cookie.exists(n) != 0, "<br />",
    'Reading cookie "' + n + '" = ', Cookie.read(n), "<br />",
    'Removing cookie "' + n + '" = ', Cookie.remove(n), "<br />",
    'Cookie exists "' + n + '" = ', Cookie.exists(n) != 0
);

//]]>
</script>
```

## JS: getCookie(), setCookie(), deleteCookie()

```js
// возвращает cookie если есть или undefined
function getCookie(name) {

    var matches = document.cookie.match(new RegExp(
      "(?:^|; )" + name.replace(/([\.$?*|{}\(\)\[\]\\\/\+^])/g, '\\$1') + "=([^;]*)"
    ))
    return matches ? decodeURIComponent(matches[1]) : undefined
}

// уcтанавливает cookie
function setCookie(name, value, props) {

    props = props || {}

    var exp = props.expires

    if (typeof exp == "number" && exp) {

        var d = new Date()

        d.setTime(d.getTime() + exp*1000)

        exp = props.expires = d

    }

    if(exp && exp.toUTCString) { props.expires = exp.toUTCString() }

    value = encodeURIComponent(value)

    var updatedCookie = name + "=" + value

    for(var propName in props){

        updatedCookie += "; " + propName

        var propValue = props[propName]

        if(propValue !== true){ updatedCookie += "=" + propValue }
    }

    document.cookie = updatedCookie

}

// удаляет cookie
function deleteCookie(name) {

    setCookie(name, null, { expires: -1 })

}
/*
Аргументы:

name
название cookie
value
значение cookie (строка)
props
Объект с дополнительными свойствами для установки cookie:
expires
Время истечения cookie. Интерпретируется по-разному, в зависимости от типа:
Если число - количество секунд до истечения.
Если объект типа Date - точная дата истечения.
Если expires в прошлом, то cookie будет удалено.
Если expires отсутствует или равно 0, то cookie будет установлено как сессионное и исчезнет при закрытии браузера.
path
Путь для cookie.
domain
Домен для cookie.
secure
Пересылать cookie только по защищенному соединению.
*/
```

<br>
<br>

---

[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/HTML%20Tricks/README.md)
