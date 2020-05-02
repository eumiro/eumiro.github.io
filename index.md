{% for post in site.posts %}
<div style="font-size: 160%; font-weight: 900; color: black">
    <a href="{{ post.url }}">{{ post.title }}</a>
</div>
<div style="font-size: 80%">
    <i class="fa fa-calendar"></i> {{ post.date | date: "%a %-d %B %Y" }}
    &nbsp;|&nbsp;
    <i class="fa fa-tag"></i> {{ post.tags | join: " &bull; " }}
    &nbsp;|&nbsp;
    <i class="fa fa-align-left"></i> {{ post.content | number_of_words }} words
</div>
<div style="font-style: italic">
    {{ post.abstract }}
</div>
<hr />
{% endfor %}
