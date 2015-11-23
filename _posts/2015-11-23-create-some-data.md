---
layout: post
title: Create some data
categories: []
tags: []
published: True
date: 2015-11-23

---

Now that we have are serving some static pages, we should start looking into serving data from database. Meteor is after all for creating web apps and not web sites. And web apps are bound to have to work with data.

## Procedure

### Create the collection

In `lib/collection.js`

{% highlight javascript %}
Plans = new Mongo.Collection('plans');
{% endhighlight %}

### Displaying on home page

Add the following code on the `home.html` file after the `Blog Admin` link

{% highlight html %}
{% raw %}
<h2>Plans</h2>
{{#each plans}}
    <p>Name: {{name}}</p>
    <p>Description: {{description}}</p><br>
{{else}}
    <p>There are no plans</p><br>
{{/each}}
{% endraw %}
{% endhighlight %}

### Serving data using router

Add the following to the home page route in `router.js` so it returns all the plans data.

{% highlight javascript %}
this.route('home',{
    path: '/',
    data: function () {
        return { plans: Plans.find() };
    }
});
{% endhighlight %}

### Add data through client console

Run meteor then browse to <http://localhost:3000>. Open up the developer console on your web browser. Type 

{% highlight javascript %}
Plans.insert({name:'test plan', description:'some text'})
{% endhighlight %}

If it returns an id, that means it has successfully inserted the data into database.

### Add data through meteor mongo

In terminal browse to the project directory and type `meteor mongo`, this will bring you into mongodb within meteor. 


{% highlight bash %}
db.plans.insert({name:'mongo', description:'mongo description'})
{% endhighlight %}

You should get `WriteResult({ "nInserted" : 1 })` and the new plan will show up on the website.

## Analysis

### Create the collection

`Mongo.Collection('plans')` tells meteor to create a new collection in the mongo database named plans. Currently meteor only works with [Mongo Database](https://www.mongodb.org). It is a document-oriented database instead of the relationship database like MySQL. It is not difficult to use and have high performance. If you're coming from SQL background, you just have to be prepared to make some small adjustments. 


To keep things simple, the `plan` data object will have a `name` and a `description` like following. 

{% highlight javascript %}
plan :{
  name :       'test plan',
  description: 'test description'
}
{% endhighlight %}

### Displaying on home page

Checkout the [View Template]({% post_url 2015-11-19-view-template %}) for meanings the `{% raw %}{{ }}{% endraw %}` in the code. 

### Serving data using router

The data entry for the home route will search the mongo database for all `Plans` and return as `plans` variable to the view template.

### Add data through client console

One of the strength of meteor is data changes are reflected in the view immediately. Data changes can be done via web form or through client console in this case. You'll see that by entering the command through the console, the data is immediately shown on the webpage. 

Client side database manipulation is very limited due to security reason, we will get into it later. 

### Add data through meteor mongo

Data can also be altered on server side which is mostly through `meteor mongo`. More things can be done on the server side so you will have to be very careful not to destroy data while here. 