---
layout: post
title: Meteor Directory Structure
categories: [meteor]
tags: []
published: True
date: 2015-10-20

---

There is no conventional file structure for meteor but the following is a good guide. 

{% highlight bash %}
/client
  /template
    /_partial
      navbar.html
      footer.html
      layout.html
      layout.js
    /plan               # This is just for example
      add_plan.html     
      edit_plan.html    
      list_plans.html   
      plan.js           
    ...
  /style
/server
/lib
  router.js
  collection.js
/public
  /img
{% endhighlight %}

### Client
Any files here are only served to the client. This is a good place to keep your HTML, CSS, and UI-related JavaScript code. I put the `layout`, `navbar` and `footer` in the `_partial` folder because these appears in almost all meteor prpjects. There's also a `layout.js` file which we use to put helper functions for `layout.html`. 

The `plan` is just an example folder. It is a seperate folder because I wanted to put all plans related html and javascript files in a neat folder. 

I also prefer to put css files in separate folder but it's not necessary.

### Server
Any files in this directory are only used on the server, and are never sent to the client. We typically put propriatory code, database updating etc code in server to prevent client side attack. 

### Lib
This is typically for files which is accessible both from client and server. Router.js is a good example as both needs to know how to go to certain route. Collections.js holds information on database collections and possibly data verification.

### Public
Files in /public are served to the client as-is. Use this to store assets such as images.
