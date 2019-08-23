---
layout: page
title: About
description: 技术改变人生
keywords: Huanren Wang, paul
comments: true
menu: 关于
permalink: /about/
---

我是paul，因技术成就，因技术立足。

努力改变人生。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
