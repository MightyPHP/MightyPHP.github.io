---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: docs
title: Introduction
---
# CSRF Protection

## CSRF Form Handling

All `POST`, `PUT`, and `DELETE` requests are passed through CSRF checking. In order for your requests to be verified, there will be needs to prepare your requests.

#### Using Form or Serialization

``` html
<form>
    {% raw %}{{ @csrf }}{% endraw %}
    <input name="username" />
    <input name="password" />
</form>
```

By having the {% raw %} `{{ @csrf }}` {% endraw %} tag, the form will automatically be prepared to tag along the CSRF token for backend verification.

#### Using Header

There will be times when you would need to simply call to the backend without a form. You can thus send the `X-CSRF-TOKEN` header with the token.

To access the token from your view, simply use the {% raw %} `liquid {{ csrf_token() }}` {% endraw %} to grab the value. 

Example with Axios client:

``` javascript
axios.post('https://example.com/postSomething', {
 headers: {
   X-CSRF-TOKEN: {% raw %}"{{ csrf_token() }}"{% endraw %}
 }
})
```


If you have an API call that does not wish to pass through the CSRF verification, simple build your routes in `api.php` or under the `ROUTE::api` block.
