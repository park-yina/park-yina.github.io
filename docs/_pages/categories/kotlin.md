---
layout: defult
title: Kotlin Posts
permalink: /categories/kotlin
taxonomy: kotlin
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kotlin Posts - 우당탕탕 코틀린</title>

  <style>
    ul {
      margin-left: 40px;
    }

    ul a {
      color: #5627a8;
    }

    body {
      font-family: 'Arial', sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f8f8f8;
      color: #333;
    }

    h1 {
      font-size: 28px;
      color: #5627a8;
    }

    .entries- {
      padding: 10px;
      background-color: #fff;
      border: 1px solid #ddd;
      border-radius: 5px;
    }

    .entries- h2 {
      font-size: 20px;
      color: #5627a8;
      margin-bottom: 10px;
    }

    .entries- a {
      text-decoration: none;
    }
  </style>
  <link rel="import" href="site.categories.viewport.html">
</head>
<body class="layout--categories">
  <h1> 🖥Kotlin study</h1>
  <div class="entries-">
    {% for post in site.categories['kotlin'] %}
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    {% endfor %}
  </div>
</body>
</html>
