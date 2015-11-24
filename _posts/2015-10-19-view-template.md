---
layout: post
title: View Template
categories: []
tags: ['meteorblog']
date: 2015-10-19

---

From previous post, meteorblog.html have the following code.

{% highlight html %}
{% raw %}
<body>
  <h1>Welcome to Meteor!</h1>

  {{> hello}}
</body>

<template name="hello">
    {{> loginButtons}}
</template>
{% endraw %}
{% endhighlight %}

`{% raw %}{{> hello}}{% endraw %}` tells meteor to insert the content of the `hello` template at that location. `{% raw %}{{> loginButton}}{% endraw %}` is provided by the accounts-ui package for a simple view of login/registration forms.

## Template

The template file ends with `.html` for Meteor. The template is how meteor displays the html and css of the app. You would write template as normal html with some `{% raw %}{{ }}{% endraw %}` brackets for special operations. The example here is with `{% raw %}{{> ...}}{% endraw %}`. The `>` operator tells meteor to show a template with that name. 

Typically meteor app will have a `layout.html` which will look something like this. 

{% highlight html %}
{% raw %}
<body>
  {{renderPage}}
</body>

<template name="layout">
    {{> navbar}}
    {{> yield}}
    {{> footer}}
</template>
{% endraw %}
{% endhighlight %}

The `navbar` template is for the navigation bar, the `footer` template is for the footer and `yield` is for whatever template the route is suppose to point to. That way, every page that your app is serving will have the navigation bar and footer included. 

Typically the template filename and the template name are the same. But you can also have multiple templates in a single file. For example, `post.html` file can have `list_posts`, `show_post`, `add_post`, `edit_post` etc templates so that all `post` related views are within a single html file. 

## Template functions

Other examples include

- `{% raw %}{{#each ...}} ... {{/each}}{% endraw %}`
- `{% raw %}{{#if ...}} ... {{else}} ... {{/if}}{% endraw %}`
- `{% raw %}{{#with ...}} ... {{/with}} {% endraw %}`

The following example shows how to use the operator. The `plan` data object have entry name `label` and `description`. So this will display all plans with a `h3` and `p` html tags each. 

{% highlight html %}
{% raw %}
{{#each plans}}
    <h3>{{label}}</h3>
    <p>{{description}}</p></hr>
{{/each}}
{% endraw %}
{% endhighlight %}

## Template Helper

There's also template helper that allow you to create any function and output to the view. But we wouldn't go into detail now. 
