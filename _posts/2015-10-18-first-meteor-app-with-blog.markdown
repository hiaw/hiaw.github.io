---
layout: post
title:  "First Meteor app With Blog"
date: 2015-10-18
tags: ['meteorblog']
---
[Meteor][meteor] is a pretty awesome platform for developing web and mobile application. Here's a quick start to have a blog running on Meteor. 

***

##PROCEDURE

First install Meteor:

{% highlight bash %}
curl https://install.meteor.com/ | sh
{% endhighlight %}

Then open up terminal and create a new project

{% highlight bash %}
meteor create meteorblog
cd meteorblog
meteor add iron:router accounts-ui accounts-password twbs:bootstrap ryw:blog
meteor
{% endhighlight %}

Now open up meteorblog.html using your favourite editor and change

{% highlight html %}
{% raw %}
<template name="hello">
  <button>Click Me</button>
  <p>You've pressed the button {{counter}} times.</p>
</template>
{% endraw %}
{% endhighlight %}

to 

{% highlight html %}{% raw %}
<template name="hello">
    {{> loginButtons}}
</template>
{% endraw %}
{% endhighlight %}

Now your browser and go to <http://locahost:3000>, click on the "Sign In" button, then the "Create account". Now enter a valid email and password and press enter. You are now logged in if you see the email address you entered in place of "Sign In".

Now go to <http://locahost:3000/admin/blog>. You will be greeted by a rich featured blogging interface to start blogging. Once you have created some blog post, you can navigate to <http://locahost:3000/blog> to view them.

We haven't even touched on the code yet and we have a working blogging system?! Not bad now isn't it? 

---

##ANALYSIS

###CREATE

Now let's go back and see step by step what we just did. 

curl https://install.meteor.com/ | sh
This step essentially just install the meteor command line tool which we will use to create and run meteor apps.

`meteor create meteorblog` ask meteor to create a new meteor project call meteorblog. The default example gives you a very simple 3 files structure which includes a html, css and javascript file. You can get meteor to create a project base on other available examples by reading the help menu for meteor create `meteor create --list`.

Another directory that is usually hidden is the .meteor directory. In here are where all the meteor magic happens. It keeps track of all the packages install, version, platform to build and a place to place all the builds. In most cases one do not need to worry about this directory. 

###PACKAGES

"meteor add" is the command to add packages to your app. Below are the packages you added and a brief description on what they do.

{% highlight bash%}
iron:router         Routing specifically designed for Meteor
accounts-ui         Simple templates to add login widgets to an app
accounts-password   Password support for accounts
ryw:blog            A package that provides a blog at /blog
twbs:bootstrap      The most popular front-end framework for developing responsive, mobile first projects on the web.
{% endhighlight %}

All of these (except `ryw:blog`) are almost always seen with typical meteor application. They provide the basic framework to routing, sign in, sign out and front end. ryw:blog is a more specialized package for creating a blog in your app without any code. In fact I am writing using it right now.

###RUNNING

`meteor` is short for `meteor run` on the command line. It will build the app and serve it on <http://locahost:3000>. Noticed that I did not ask you to run the app after changing the code. That's because meteor watches for file change and will rebuild or renew the site when necessary. 

###CODING

Note that you took the default example and change one line of code. That line of code is provided by the accounts-ui package which a way to register and login. This was necessary because the blog package needs the user to be logged in to be able to access the admin page for creating the blog posts. Once that's done, everything works.

___

##FINALLY
This was a very long post for very short procedure but with lots of functionality. I'll dive into much more detail in the next post. Thanks for visiting.



[meteor]:http://meteor.com