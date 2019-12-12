---
layout: docs
title: Generating View
---
In order to render a view, the `_view()` can be initiated to call upon its view files. Note that in MightyPHP, all view files are in HTML format.

```php
class testController extends CONTROLLER{
    public function indexAction(){
        RESPONSE::return($this->_view('foo')->render());
    }
}
```

The above code will render the view from VIEW_PATH/foo.html. This also supports folder structures. For instance:
```php
class testController extends CONTROLLER{
    public function indexAction(){
        RESPONSE::return($this->_view('Auth/foo')->render());
    }
}
```

The above code will now render view from `VIEW_PATH/Auth/foo.html`.

### Variables

Sometimes, we may wish to pass data to our view files, in order for it to be used to render user interfaces. To do so, simply pass in the data array within the render() function.

```php
class testController extends CONTROLLER{
    public function indexAction(){
        $data = array(
            "foo" => "bar"
        )
        RESPONSE::return($this->_view('Auth/foo')->render($data));
    }
}
```

Then at the view, which is your foo.html, 
{% raw %} 
```html
<div>{{ foo }}</div>
```
{% endraw %}

You may also choose to capture the data with JavaScript:

{% raw %} 
```javascript
var data = "{{ foo }}";
```
{% endraw %}

#### Array
All array data from the controller will be JSON-encoded. As such, to assign it to the JavaScript Variable, it is bestt that it is done without the quotes.
{% raw %} 
```javascript
var data = {{ foo }};
```
{% endraw %}
You can then access the data as JSON in JavaScript.