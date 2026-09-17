---
layout: default
title: rdap.ai Notes
---

This is where I write about ideas, experiments and technical developments around [rdap.ai](https://rdap.ai/) — particularly things that need a little more explanation than fits comfortably inside the application.

## Latest

{% for post in site.posts limit:5 %}
### [{{ post.title }}]({{ post.url | relative_url }})

{{ post.date | date: "%-d %B %Y" }}
{% endfor %}

---

## Topics

### RDAP & DNS

Notes on domain availability, registry behaviour, RDAP, DNS and open domain infrastructure.

### Pattern searching

Examples and ideas for exploring domains systematically using DDSL rather than checking names one at a time.

### Building rdap.ai

Occasional notes about features, experiments and decisions made while developing rdap.ai.

---

[Open rdap.ai →](https://rdap.ai/)
