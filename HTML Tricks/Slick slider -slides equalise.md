# Slick slider — slides equalise

```html
<div id="slick-slider" data-role="slider-equalize">
	…
</div>

<script>
	// Slider equalize elements
	$('[data-role="slider-equalize"]').each(function(){
		let h = $(this).height();
		$(this).find('.slick-slide').css('height',h);
	})
</script>
```

<br>
<br>

---

[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/HTML%20Tricks/README.md)
