<ul>
  {% for post in site.posts %}
    <li style="list-style-type:none">
      <h4><a href="{{ post.url }}" >{{ post.title }}</a></h4>
      {{ page.date | date_to_long_string }} - {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
