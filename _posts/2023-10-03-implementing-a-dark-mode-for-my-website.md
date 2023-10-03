---
layout: post
author: Tobias Klöpper
---
Dark mode designs have been around for a few years. Your operating system and your phone also support system wide themes, that apply the default style to all installed applications. Because of that I was always interested in doing a dark mode on my website. After some initial struggle my site now supports a dark mode with a design switch. Here is how I did it.

### Starting off with a HTML/CSS restructure
Before diving into the dark mode specific CSS settings, I had restructure my HTML Layout. My blog is using a custom HTML/CSS layout, that has been copied from  places all over the internet. I think it was using a similar approach to basic CSS website structuring like the [MotherfuckingWebsite](https://motherfuckingwebsite.com/). It had the following simple CSS design:

{% highlight css %}
body {
  margin: auto;
  max-width: 650px;
  background-color: #eeeeee;
  color: #444;
  padding: 0 10px;
  font: 1.2em/1.62 sans-serif;
}
{% endhighlight %}

It worked well but the I had issues with visibility on mobile devices. Therefore I began by reordering some elements inside specific HTML elements. For example, I wrapped a `<article>`` element around each post. Additionally the nav bar was separated from the body. Because of these changes I was able to add the CSS flexbox component to the website. With that change the website made a huge step towards a better experience.

### Media Queries Everywhere
After the implementation of the first flexbox design, the mobile style was a bit off. It mostly came down to a font size issue. The site did not scale well with the basic font size of the desktop version. So I was googling around and found some media queries for the three basic screen sizes. These are the mobile, the tablet and the desktop versions. In the end I used just the mobile and tablet media queries, because the tablet version seemed to work fine with the design styles for the desktop versions. You can see the applied screen sizes in the following code implementation:

{% highlight css %}
@media only screen and (min-width: 768px) { //style are applied here }
@media only screen and (max-width: 767px) { //phone specific styles here }
{% endhighlight %}

This is bases on an answer from [stackoverflow.com](https://stackoverflow.com/questions/6370690/media-queries-how-to-target-desktop-tablet-and-mobile).

But this is not the only use case for media queries. They also support the different color schemes, that the user has chosen for his os/application. You can read more about them on the [MDN Website](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme). It basically boils down to the following code:

{% highlight css %}
@media (prefers-color-scheme: dark) { //apply dark color styles here }
{% endhighlight %}

The media checks if the user prefers a specific color scheme. In this case the queries checks for the color scheme dark, which is the shorthand version of dark-mode. If this color scheme is detected than the styles inside the parenthesis are getting applied. You can even create a color scheme which supports the light-mode. 
After implementing a dark mode media queries, I just had to write a toggle button to change the different styles, right?

### Implementing a real dark mode toggle
For a few hours I was trying to build a JS-Script to switch between the media queries. But shortly after I found out why this was not possible. It basically boils down to the fact, that media queries are just queries! Media queries queue the specific item or setting and they do something if the condition is met. Therefore it was not possible to create a script that changes the media queries because they only evaluate and don’t change without the user changing settings. It could have been so easy...

Returning to the project after a few weeks, my search for other peoples implementation led me to a blog post. This blog post used a different approach than media queries. The dark mode was built with CSS variables and saving the preferred theme in the local storage. You can read it on [Dev.to](https://dev.to/ananyaneogi/create-a-dark-light-mode-switch-with-css-variables-34l8).

The implementation works by defining a basic color scheme within the root document. This is done by creating CSS variables for each style:

{% highlight css %}
:root {
	--primary-color: #123456;
	//more styles
}
{% endhighlight %}

After this you just create a custom CSS theme for your preferred color scheme. This theme just changes the values of the CSS variables that are applied to the elements:

{% highlight css %}
[data-theme="dark"] {
	--primary-color: #123456;
 	//more styles
}
{% endhighlight %}

Now I just need a button to switch between the different themes. This can easily be solved by adding some event listeners to the specific theme toggle button. You can find the code on my [Github commit](https://github.com/Friendscover/my-website/commit/2e3f4d2f1a88ab96c61a03790d4a768c95de62d8#diff-1cdbe0569fb88682d7e5af122b235c04bd9af8a4970739907cb41bd40f2bf02d).

With this final step the dark mode is working and the user can easily change between their preferred color styles! You can try it out yourself of you click on the button in the top navigation bar!