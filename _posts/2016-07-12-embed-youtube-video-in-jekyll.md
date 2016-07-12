---
layout: post
title: How to embed Youtube videos in Jekyll without plugins
navi_title: Blog Post
series_tag: Jekyll
date: 2016-07-12 12:00:00 -0500
excerpt_separator: <!--more-->
---

*This is #2 in a planned series of mini-posts learning Jekyll*

It was not immediately clear how to embed Youtube videos in Jekyll blogs.  Google `jekyll documentation embed youtube videos` and you'll get a bunch of how-to's... I found one particularly easy to do simply by creating an additional HTML file in the `_includes` folder in your jekyll website folder with the `iframe` embed code and add a line of liquid code in your jekyll blog post to embed the Youtube video.  It was cool to learn how we can include snippets of HTML codes by this method.

Here's an example to embed a random Youtube video to this Jekyll blog post.

Youtube video I want to embed to this blog post: `https://www.youtube.com/watch?v=6EVs0BrG57I`

The typical way we embed Youtube video is by copy and pasting the embed codes from the Youtube video's share options: `<iframe width="560" height="315" src="https://www.youtube.com/embed/6EVs0BrG57I" frameborder="0" allowfullscreen></iframe>`


But, apparently we can't just insert this code into Jekyll's blog post using markdown.  So an easy way I've found is to create a HTML file with the embed code snippet and call it from the blog post.  Here's how I did it:

1) In your Jekyll website folder, go to or create a folder called `_includes`.  This folder will let you include any files located here into your markdown posts using liquid.

2) Create a HTML file named `youtube_embed.html` in the `_includes` folder.

3) Now, we'll add in the iframe codes from the Youtube embed link and add some subtle `liquid` codes to this html file so we can make this code work with any Youtube video embeds by defining the video ID.  From the above video embed, the video id is `6EVs0BrG57I`.  It is code that comes after `/embed/` in the youtube link.  So in the `youtube_embed.html` file, we'll add in the following codes:{% highlight html %}<iframe width="560" height="315" src="https://www.youtube.com/embed/6EVs0BrG57I" frameborder="0" allowfullscreen></iframe>{% endhighlight %}

4) Then, we'll replace the youtube video id with liquid codes `{%raw%}{{ include.id }}{%endraw%}`.  This will let us define the Youtube id whenever we want to embed a video in any future blog posts. So now in the `youtube_embed.html` file, you will have the following codes in it:
{% highlight html %}<iframe width="560" height="315" src="https://www.youtube.com/embed/{%raw%}{{ include.id }}{%endraw%}" frameborder="0" allowfullscreen></iframe>
{% endhighlight %}

5) Now, we are ready to add the youtube video to this blog post.  In the blog post markdown file, go to where you want to embed the youtube video and insert the following line:
{% highlight html %}
{%raw%}{% include youtube_embed.html id="" %}{%endraw%}  
{% endhighlight html %}

6) Remember where your Youtube id?  Copy it and you are now ready to add in the Youtube id in the `id` field, like this:
{% highlight html %}
{%raw%}{% include youtube_embed.html id="6EVs0BrG57I" %}{%endraw%}  
{% endhighlight html %}

7) Load up `jekyll serve` and see if you are now seeing the Youtube embedded video in your blog post... and you're done!

{% include youtube_embed.html id="6EVs0BrG57I" %}

## NOTES

+ I hope to explore the `_includes` folder more.  For now, it seems we can put any HTML files in this folder and pull it into our markdown posts using liquid code `{%raw%}{% include filename.html %}{%endraw%}` while implementing in any Front Matter variables.

+ For more reference, check out [Adam Harris's guide: How to Easily Embed YouTube Videos in Jekyll Sites Without a Plugin](http://www.adamwadeharris.com/how-to-easily-embed-youtube-videos-in-jekyll-sites-without-a-plugin/)

+ Liquid FYI: In order to show liquid codes as an example, I had to wrap the liquid codes with `{{"{%raw"}}%}` and `{{"{%endraw"}}%}` liquid codes.  More info here: [Display Liquid code in Jekyll](https://truongtx.me/2013/01/09/display-liquid-code-in-jekyll).  *It is not fun to show liquid codes in markdown.*
