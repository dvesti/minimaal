---
title: Добавлен generator feed
date: 2018-02-17 17:11:09
tags: [Plugins, Hexo]
categories: News
---

Добавил на сайт плагин **RSS/Feed** - hexo-generator-feed  <!--more-->
Пользовался [этой инструкцией](https://github.com/hexojs/hexo-generator-feed).
Добавил в конфиг темы (после *rss*)

```js
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
```
Теперь в боковой панели открывается красивая ссылка на **RSS** 
