---
layout: page
title: Arsip
permalink: arsip.html
---
<h3 style='text-align:center;'>Kategori</h3>
<p style='text-align:center;'>{% for pt in site.categories %}<a href="#cat-{{pt[0] | replace:'&amp;','' | replace:' ','_'}}">{{pt[0]}}</a>, {% endfor %}</p>

#### Seluruh Arsip
<table>
{% assign sorted = (site.posts | sort: 'date' | reverse) %}
{% for post in sorted %}
	<tr>
		<td>{{ post.date | date: "%b %-d, %Y" }}</td><td><a href="{{ post.url }}">{{ post.title }}</a></td>
	</tr>
{% endfor %}
</table>
<br />

{% for cat in site.categories %}
{% assign nt = cat[0] %}

#### {{ nt }} {#cat-{{nt | replace:'&amp;','' | replace:' ','_' | replace: '.', '_' | replace: '/', '_'}}}
<ul>
	{% assign sorted = (site.posts | sort: 'date' | reverse) %}
	{% for post in sorted %}
		{% for pt in post.categories %}
			{% if nt == pt %}
			<li>
				{{ post.date | date: "%b %-d, %Y" }} - 
				<a href="{{ post.url }}">{{ post.title }}</a>
			</li>
			{% endif %}  
		{% endfor %} 
	{% endfor %}
</ul>  
{% endfor %}

<h3 style='text-align:center;'>Tags</h3>
<p style='text-align:center;'>{% for pt in site.tags %}<a href="#tag-{{pt[0] | downcase | replace:'&amp;','' | replace: ' ', '_' | replace: '.', '_' | replace: '/', '_'}}">{{pt[0]}}</a>, {% endfor %}</p>
{% for tag in site.tags %}
{% assign nt = tag[0] %}

#### {{ nt }} {#tag-{{nt | downcase | replace:'&amp;','' | replace: ' ', '_' | replace: '.', '_' | replace: '/', '_'}}}
<ul> 
{% assign sorted = (site.posts | sort: 'date' | reverse) %}
{% for post in sorted %}
	{% for pt in post.tags %}
		{% if nt == pt %}
			<li>
        {{ post.date | date: "%b %-d, %Y" }} - 
        <a id="#tag-{{pt | downcase | replace: ' ', '_'}}" href="{{ post.url }}">{{ post.title }}</a>
      </li>
		{% endif %}  
	{% endfor %} 
{% endfor %}
</ul>  
{% endfor %}
