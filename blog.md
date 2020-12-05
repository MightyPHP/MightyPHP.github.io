---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: blog
---
<h1 class="py-2 px-2">Blog Posts</h1>

<div class="row">
  {% for post in site.posts %}
    <div class="col-12">
      <a class="text-decoration-none" href="{{ post.url }}"><div class="card px-2 py-2">
        <caption class="text-muted">{{ post.dateLabel}}</caption>
        <p>{{ post.excerpt }}</p>
      </div></a>
    </div>
  {% endfor %}
</div>