---
layout: default
title: Home
---

# Shuao Chen

I am a PhD candidate at Shanghai Jiao Tong University.  
My research focuses on information theory, rate-distortion theory, finite-blocklength analysis, and CSI feedback in wireless communication systems.

---

## About This Site

This website collects my research notes, paper readings, and technical writeups, mainly in information theory and wireless communications.

## Research Topics

- Information Theory
- Rate-Distortion Theory
- Finite-Blocklength Analysis
- CSI Feedback
- Massive MIMO

## Recent Posts

<ul>
  {% for post in site.posts limit:5 %}
    <li style="margin-bottom: 10px;">

      <!-- 标题 + 日期 -->
      <div>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <small> — {{ post.date | date: "%Y-%m-%d" }}</small>
      </div>

      <!-- 分类 -->
      {% if post.categories and post.categories.size > 0 %}
      <div class="post-meta-extended">
        Categories:
        {% for c in post.categories %}
          <span class="post-category">{{ c }}</span>{% unless forloop.last %}, {% endunless %}
        {% endfor %}
      </div>
      {% endif %}

      <!-- 标签 -->
      {% if post.tags and post.tags.size > 0 %}
      <div class="post-meta-extended">
        Tags:
        {% for t in post.tags %}
          <span class="post-tag">#{{ t }}</span>{% unless forloop.last %}, {% endunless %}
        {% endfor %}
      </div>
      {% endif %}

    </li>
  {% endfor %}
</ul>

## Contact

Email: [shuaochen99@gmail.com](mailto:shuaochen99@gmail.com)

## Links

- GitHub: [shuao-chen](https://github.com/shuao-chen)
- ORCID: [0009-0007-2757-6551](https://orcid.org/0009-0007-2757-6551)
