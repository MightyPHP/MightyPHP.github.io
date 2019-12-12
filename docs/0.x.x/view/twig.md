---
layout: docs
title: Twig Templating
---

# Twig Templating

Mighty uses Twig Templating to generate its dynamic contents. All of it can be referred to at Twig's documentations.

### Added functions
Mighty comes with additional Twig templates. 

#### `asset()`
The asset function is used to load static contents from the server. It calls the Helper `asset()` function, and can be changed to load from CDN's instead. 

```php
/** /Utilities/Helpers/asset.php **/
function asset($url){
    return ROOT_PATH.$url;
}
```

The following code would load the image's src from `/Public/images/logo.png`.
```html
<img src="{% raw %}{{ asset(images/logo.png) }}{% endraw %}" />
```