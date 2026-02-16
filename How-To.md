Use 

```
---
title: About me
layout: page.njk
keyword: test
tags: pages
permalink: "{{ title | slugify }}.html"
eleventyNavigation:
  key: "{{ title | slugify }}"
  title: About me
  order: 2
---
```
For links at the top right corner on the home page, the layout needs to be page,
, the order determines the order of the links.


The sitemap is at domainname/sitemap.xml, the rss is at domainname/feed.xml.

