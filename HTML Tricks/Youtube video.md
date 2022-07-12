# Youtube video

Добавляет превью по ID и при клике автоматически меняет на iframe

```html
<div class="youtube-video" data-id="7-VvXC-j4Uo"></div>

<script>
(function(){
    $('.youtube-video').each(function(){
        let _t = $(this);
        let bgImg = 'https://i.ytimg.com/vi_webp/' + _t.attr('data-id') + '/maxresdefault.webp';
        
        let img = new Image();
        img.src = bgImg;
        if ( img.height == 0 ) bgImg = 'https://i.ytimg.com/vi_webp/' + _t.attr('data-id') + '/0.webp';

        _t.css('background-image', 'url('+bgImg+')');
        _t.append('<div class="youtube-play-btn"></div>');

        _t.on('click', function(){
            let __t = $(this);
            let iframeUrl = 'https://www.youtube.com/embed/' + __t.attr('data-id') + '?autoplay=1&autohide=1';
            if ( __t.data('params') ) {
                iframeUrl += '&'+__t.data('params');
            }

            let iframe = $('<iframe>', {
                src: iframeUrl,
                width: __t.css('width'),
                height: __t.css('height'),
                frameborder: 0,
                allow: 'accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture',
                allowfullscreen: ''
            });

            __t.replaceWith(iframe);
        });
    })
})();
</script>
```

<br>
<br>

---

[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/HTML%20Tricks/README.md)
