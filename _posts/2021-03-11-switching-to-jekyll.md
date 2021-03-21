---
layout: post
author: Tobi
---

### tl;dr;
- Switched my Website to Jekyll
- Easy deploy for blog-posts via markdown
- Uses ruby code

## Switching my Site to Jekyll

For the past few weeks, i was looking for a way to easily write blogposts for my website. Writing the posts in plain HTML was not my kind of thing, i looked at ways to convert Markdown files to HTML. And after some searching, the Jekyll Gem seemed kinda promising. It had md to HTML conversion and the deploy should be easy, because this website was already deployed on Github and apparently Github Pages uses Jekyll on the backend. 

## Convert the page

My website was really simple HTML and CSS, therefore the coversion to Jekyll was fast. The [Step by Step tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) on the main Jekyll site was beginner friendly and easy to understand. Just running `gem jekyll` and `bundle exec jekyll serve` was used to generate the site. After updating the main `index.html` file and using layouts to simplify the page rendering, a `navigation.yml` file with the links to my other online presences was added.
