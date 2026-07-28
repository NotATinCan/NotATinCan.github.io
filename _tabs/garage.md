---
title: The Garage
icon: fas fa-warehouse
order: 5
---

# The Garage Archive

Our training logs and shared memories. Strong-quiet progress, one session at a time.

**Subscribe:** [Atom Feed](/feed.xml) 📡

{% assign garage_posts = site.tags["The Garage"] | sort: "date" | reverse %}

{% if garage_posts.size > 0 %}
<ul>
{% for post in garage_posts %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <span class="text-muted"> — {{ post.date | date: "%b %d, %Y" }}</span>
  </li>
{% endfor %}
</ul>
{% else %}
<p>No Garage entries yet.</p>
{% endif %}

---

Keep it simple. Keep it consistent. The Garage stays alive.