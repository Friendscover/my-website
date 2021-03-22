---
layout: post
author: Tobi
---

- Switched my Website to Jekyll
- Easy deploy for blog-posts via markdown
- Uses ruby code

## Switch to Jekyll

For the past few weeks, i was looking for a way to easily write blog posts for my website. Writing the posts in plain HTML was not my kind of thing, so i looked at ways to convert Markdown files to HTML. And after some searching, the Jekyll Gem seemed kinda promising. It has md to HTML conversion and the deploy should be easy, because this website was already deployed on Github and apparently Github Pages uses Jekyll on the backend. 

## Convert the page

My website was really simple HTML and CSS, therefore the coversion to Jekyll was fast. The [Step by Step tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) on the main Jekyll site was beginner friendly and easy to understand. Just running `gem jekyll` and `bundle exec jekyll serve` was necessary to make the site available locally. After updating the main `index.html`, adding navigation to every page was done via the `navigation.yml` file:
{% highlight yaml %}
  - name: Home
    link: /
  - name: About me
    link: /about.html
{% endhighlight %}

## Changing the styling

A Dark mode was already planned as an improvement on this site. Adding a simple dark mode is as easy as adding an `@media` key to the pages css file: 
{% highlight css %}
  @media (prefers-color-scheme: dark) {
    body { background: #000; color: #fff; }
    a { color: #eee; }
  }
{% endhighlight %}

There is still room to improve on this design but i wanna keep it simple. I might add an dark/light mode switch to the page in the near future.

## Listing blog post

Jekyll makes it easy to iterate over posts in the post directory:
{% highlight ruby %}
  for post in site.posts 
{% endhighlight %}

Inside this loop you can access the properties of the post, e.g:
{% highlight ruby %}
  post.url
  post.excerpt
  post.title
{% endhighlight %}

And just by adding an `{% raw %}{{ content }}{% endraw %}` to the default post page, Jekyll converts every Markdown file under my posts folder and renders a webpage

## Final thoughts

So far this has been a fun project and writing blog posts in md should be straight forward for now. I am planing to write atleast one post every month about my journey in the Ruby on Rails ecosystem and also about agricultural topics. This is gonna be exciting. 

---
[Back to the main page]({% link index.html %})