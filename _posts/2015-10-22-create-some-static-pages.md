---
layout: post
title: Create Some Static Pages
categories: []
tags: []
published: True
date: 2015-10-22

---

In previous two posts we had a look at [view template]({% post_url 2015-10-19-view-template %}) and [iron:router]({% post_url 2015-10-21-ironrouter %}). Now let's use those knowledge and create some static pages. 

##Procedure

First we'll delete the

{% highlight bash %}
meteorblog.html
meteorblog.js
meteorblog.css
{% endhighlight %}

files and we will be creating the directory structure as described in [Meteor Directory Structure]({% post_url 2015-10-20-meteor-directory-structure %}).

Then in `lib/router.js`, add the following code

{% highlight javascript %}
Router.configure({
    layoutTemplate: 'layout'
});

Router.map(function () {
    this.route('home',{
        path: '/'
    );

    this.route('about');
}
{% endhighlight %}

Now create `client/template/home/home.html` with the following content.

{% highlight html %}
{% raw %}
<template name="home">
    <h1>Home page</h1>
    <p>This is the home page.</p>
    <a href="{{pathFor 'about'}}">About</a><br>
  <a href="/blog">Blog</a><br>
  <a href="/admin/blog">Blog Admin</a><br>
</template>
{% endraw %}
{% endhighlight %}

`client/template/_partial/layout.html`

{% highlight html %}
{% raw %}
<body>
  {{renderPage}}
</body>

<template name="layout">
    {{> loginButtons}}
    {{> yield}}
</template>
{% endraw %}
{% endhighlight %}

`client/template/about/about.html`

{% highlight html %}
{% raw %}
<template name="about">
    <h1>About</h1>
    <p>This is the about page.</p>
</template>
{% endraw %}
{% endhighlight %}

So now your folder should look like this

{% highlight bash %}
/client
  /template
    /_partial
      layout.html
    /about
      about.html   
    /home
      home.html         
/lib
  router.js
{% endhighlight %}

Now run `meteor` on terminal and navigate to [localhost:3000](localhost:3000) and you should see your home page with a link to the about page. 

## Analysis

As described in previous posts