---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
---
Welcome to my site! Here you will find my projects organized in blog posts, general pages, info about me, ways to contact me and more. Mostly focused on programming and electronics, although other topics will be mentioned. This site is extremely minimalist and contains no advertisements or trackers, and is thus extremely eco-friendly and privacy-conscious! Enjoy your stay!


<h3>Featured post:</h3>
<a href="{{ site.posts[0].url }}">{{ site.posts[0].title }}</a><br>
{{ site.posts[0].description }}<br>
*In category: {{ site.posts[0].categories }}*

<h3>All posts:</h3>
{% for category in site.categories %} 
<h4 class="link-header" id="{{ category[0] }}">{{ category[0] | capitalize }}:</h4>
{% for category_info in site.data.category_data.category %}
{% if category_info.name == category[0] %}
{{ category_info.description }}
{% endif %}
{% endfor %}
<ul>
{% for post in category[1] %}
<li><a href="{{ post.url }}">{{ post.title }}</a><br>
<i>By {% if post.author == "Stefan Nikolaj" %}
    <a href="{% link about.markdown %}">{{ post.author }}</a>
    {% else %}
    {{ post.author }}
    {% endif %} on {{ post.date | date_to_string }}</i><br>
{{ post.description }}</li>
<br>
{% endfor %}
</ul>
{% endfor %}

This blog is dedicated to my dearest friend Sara, who constantly pushes me to improve myself and my skills.


<script>


    // replace all dashes in category since using blank spaces in category name counts as multiple categories
    var linkTitles = document.getElementsByClassName("link-header"); // select all tags with link-header class
    for(var i = 0; i < linkTitles.length; i++){ // iterate the old-school way
        linkTitles[i].innerText = linkTitles[i].innerText.replace("-", " "); // replace the dashes in the text with spaces
    }

    
</script>