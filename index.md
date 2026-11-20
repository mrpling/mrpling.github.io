---
layout: default
title: rdap.ai Notes
---

This is where I write about ideas, experiments and technical developments around [rdap.ai](https://rdap.ai/).

## Latest

{% for post in site.posts limit:1 %}
### [{{ post.title }}]({{ post.url | relative_url }})

{{ post.date | date: "%-d %B %Y" }}
{% endfor %}

## All Posts

{% for post in site.posts limit:5 %}
### [{{ post.title }}]({{ post.url | relative_url }})

{{ post.date | date: "%-d %B %Y" }}
{% endfor %}

---
## Guides

- ### [Your first domain pattern](/guides/first-domain-pattern/)
- ### [Create pronounceable domain names](/guides/pronounceable-domain-names/)
- ### [Explore a naming space systematically](/guides/explore-a-naming-space/)
- ### [Create domain patterns with AI](/guides/domain-patterns-with-ai/)

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
