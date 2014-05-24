---
layout: post
title: "A Test"
date: 2014-05-22 14:12:11
author: dakota
categories: test
---

{% assign author = site.authors[page.author] %}
<html>
  <header>
    <p class="date">
      <span class="month">{{ page.date | date: '%b' }}</span>
      <span class="day">{{ page.date | date: '%d' }}</span>
      <span class="year">{{ page.date | date: '%Y' }}</span>
    </p>
    <h1>{{ page.title }}</h1>
    <p class="byline">
      by {{ author.display_name }}
    </p> <!-- /.byline -->
  </header>
<body>
  This is a test.

  A testy test.
</body>
</html>
