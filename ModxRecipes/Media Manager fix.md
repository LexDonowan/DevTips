# Media Manager fix
https://github.com/Sterc/mediamanager

1. assets/components/mediamanager/js/mgr/mediamanager-modal.js
	line 49:
	```
	filePreview = $file.find('.file-preview img').data('original'),
	filePath    = $file.find('.file-preview img').data('path'),
	```

2. assets/components/mediamanager/js/mgr/mediamanager-tv-input.js
	line 64:
	```
	$('input#tv' + tvId).attr('value', file.path);
	```

3. core/components/mediamanager/elements/tv/input/tpl/mm_input_image.tpl
	```
	replace all $path => $tv->value
	```

	core/components/mediamanager/templates/chunks/files/file_preview_img.chunk.tpl
	```
	<img data-original="[[+preview_path]]" class="lazy" data-path="[[+path]]" src="/[[+path]]" />
	```

4. Плагин: mediaManagerTinyMce
	line 23:
	```
	win.document.getElementById(field_name).value = file.path;
	```

5. core/components/mediamanager/model/mediamanager/classes/files.class.php

	1. Make relative path
	 line 453:
	 ```
	 $filePath = $this->removeSlashes($source['baseUrl']) . DIRECTORY_SEPARATOR;
	 ```

	 line 656:
	 ```
	 $file['preview_path'] = str_replace(rtrim(MODX_BASE_PATH, '/'), '', $cacheFilenameAbsolute);
	 OR
	 $file['preview_path'] = str_replace(rtrim(MODX_ASSETS_URL, '/'), '', $cacheFilename);
	 ```

	line 239:
	```
	$bodyData['preview'] = '<img src="/' . str_replace(rtrim(MODX_BASE_PATH, '/'), '', $cacheFilename) . '" />';
	```

	/core/components/mediamanager/templates/chunks/files/popup/crop.chunk.tpl:
	```
	<img src="/[[+file.path]]" class="crop" />
	```

	2. Translit uploaded files
	replace function `public function sanitizeFileName($fileName)` with:

	```
	public function sanitizeFileName($fileName)
    {
        $find = array(
            ' '
        );

        $replace = array(
            '-'
        );

        $fileName = $this->translitFileName($fileName);
        $fileName = strtolower($fileName);
        $fileName = str_replace($find, $replace, $fileName);
        $fileName = preg_replace('/[^a-z0-9_.-]+/', '', $fileName);

        return $fileName;
    }

    public function translitFileName($fileName)
    {
        $options = array();

        $translit = $this->mediaManager->modx->getOption('friendly_alias_translit', $options, 'russian');
        $translitClass = $this->mediaManager->modx->getOption('friendly_alias_translit_class', $options, 'translit.modTransliterate');
        $translitClassPath = $this->mediaManager->modx->getOption('friendly_alias_translit_class_path', $options, $this->mediaManager->modx->getOption('core_path', $options, MODX_CORE_PATH) . 'components/');
        $transClass = $this->mediaManager->modx->getService('translit', $translitClass, $translitClassPath, $options);
        
        $fileName = $transClass->translate($fileName, $translit);

        return $fileName;
    }
    ```

6. Activate media Manager:
	1) Create new media source and add parameter `mediamanagerSource` with value `1`.
	2) Edit Filesystem media source and add parameter `mediamanagerSource` with value `1`. Then Media Manager will be work. Then Edit Filesystem again and set `mediamanagerSource` to 0.



<br>
<br>

---
[Оглавление](https://github.com/LexDonowan/DevTips/blob/main/ModxRecipes/README.md)
