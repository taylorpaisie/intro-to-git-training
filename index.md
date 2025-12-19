---
layout: default
title: Home
nav_order: 1
---

# Intro to Git Training 🚀
Welcome! This site guides today's hands-on Git workshop.

## Goals
- Make commits locally and push to GitLab  
- Use branches & merge requests (MRs)  
- Resolve a simple merge conflict  
- Adopt good commit messages & review habits

![Version Control]({{ '/images/phd101212s.png' | relative_url }})

## Agenda
1. Why Git (version control in 10 minutes)
2. Create a repository + first commit
3. Local workflow (`status`, `diff`, `add`, `commit`, `log`)
4. Ignoring files (`.gitignore`)
5. Remote basics (`clone`, `push`, `pull`, `fetch`)
6. Branching & Merge Requests (MRs)
7. Merge conflicts (you'll do one!)
8. Etiquette & Q&A


## Lessons
{% assign lessons = site.lessons | sort: 'nav_order' %}
<ul>
{% for l in lessons %}
  <li><a href="{{ l.url | relative_url }}">{{ l.title }}</a></li>
{% endfor %}
</ul>
