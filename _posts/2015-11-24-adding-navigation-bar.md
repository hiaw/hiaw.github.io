---
layout: post
title: Adding Navigation Bar
categories: []
tags: []
published: True
date: 2015-11-24

---

Now let's make the site look a bit better by adding a navigation bar and footer

## Procedure

Bring up the terminal and install and remove some packages

{% highlight bash %}
meteor add ian:accounts-ui-bootstrap-3
meteor remove accounts-ui
{% endhighlight %}

In `client/_partial/navbar.html`

{% highlight html %}
{% raw %}
<template name="navbar">
  <nav class="navbar navbar-inverse">
    <div class="container">
      <div class="navbar-header">
        <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
        <a class="navbar-brand" href="/">Project name</a>
      </div>
      <div id="navbar" class="collapse navbar-collapse">
        <ul class="nav navbar-nav">
          <li class="active"><a href="/">Home</a></li>
          <li><a href="{{pathFor 'about'}}">About</a></li>
          <li><a href="/blog">Blog</a></li>
        </ul>
        <ul class="nav navbar-nav navbar-right">
          {{#if currentUser}}
            <li><a href="/admin/blog">Blog Admin</a></li>
          {{/if}}
          {{> loginButtons}} <!-- here -->
        </ul>
      </div><!--/.nav-collapse -->
    </div>
  </nav>
</template>
{% endraw %}
{% endhighlight %}

In `client/_partial/footer.html`

{% highlight html %}
{% raw %}
<template name="footer">
    <footer class="footer">
        <p>&copy; Company 2014</p>
    </footer>
</template>
{% endraw %}
{% endhighlight %}

Change `client/_partial/layout.html` to 

{% highlight html %}
{% raw %}
<template name="layout">
    {{> navbar}}
    {{> yield}}
    {{> footer}}
</template>
{% endraw %}
{% endhighlight %}

## Analysis

So first thing we did here is that we swap out the accounts-ui package for the bootstrap themed accounts-ui package. This is mainly so that we can place the login button on the navigation bar

Next we created the navbar.html, which I copied from the example from [Bootstrap](http://getbootstrap.com). The only new thing here is the `{% raw %}{{#if currentUser}}{% endraw %}` line. This is ask meteor if there's any user logged in, if so, diplay the blog admin link. 

Then it's just a matter of placing the navbar and footer in the right location in layout.html. 