---
layout: post
title: iron:router
categories: []
tags: []
published: True
date: 2015-11-21

---

[`iron:router`](https://github.com/iron-meteor/iron-router) is probably one of the most essential package every meteor apps should have. What is it for? Well, routing of course. See the code below to see what I mean. 

{% highlight javascript %}
Router.map(function () {
    this.route('about');
}
{% endhighlight %}

This code tells meteor to serve the `about` view template when the browser request for <http://localhost:4000/about> page. It is actually a shortcut to write the following as the path and template are the same name as the route.

{% highlight javascript %}
Router.map(function () {
    this.route('about',{
        path: '/about',
        template: 'about'
    });
}
{% endhighlight %}

One important route to define is the home route which will serve the home page when user land on your side. Note that I omitted the template name since it is the same as the route name.

{% highlight javascript %}
Router.map(function () {
    this.route('home',{
        path: '/'
    });
}
{% endhighlight %}

One can configure the default layout template to use. Also for loading and 404 templates. 

{% highlight javascript %}
Router.configure({
  layoutTemplate : 'layout',
  loadingTemplate: 'loading',
  notFoundTemplate: 'notFound'
});
{% endhighlight %}

The following shows how you can customise the url to include the plan id for individual plan. 

{% highlight javascript %}
Router.route("plan_show", {
  route : "/plan/:_id",
  data : function(){
    return Plans.findOne({_id : this.params._id});
  }
});
{% endhighlight %}

`pathFor` command is useful for getting the path in view template. Therefore, one should only change the actual path in the router.js file and use `pathFor` in view templates to minimise routing mistakes. Other command include `urlFor` and `linkTo`.

{% highlight javascript %}
{% raw %}
{{pathFor 'about' }}         '/about'
{{pathFor 'plan_show' _id }} '/plan/_id'
{% endraw %}
{% endhighlight %}


Other useful hooks are but we wouldn't go into detail now. Take a look at their [documentation](http://iron-meteor.github.io/iron-router/) for more.

{% highlight javascript %}
Router.onBeforeAction
Router.onAfterAction
Router.onRun
Router.onReRun
Router.onStop
{% endhighlight %}
