---
layout: post
title: Collapsing Lists
date: 2019-01-20 11:45:59 -0500
categories: Programming
---
I was digging around looking for a model of a collapsing list that I could base my stretch/smart goal system off of, and thankfully I found <a href="https://jsfiddle.net/ann7tctp/">it.</a> 
<br>
<br>
However one of the first things I ever learned with regards to programming is:<strong>"never copy paste code from the internet."</strong> I'm pretty sure my teacher was only telling us this because he didn't want people on stackoverflow writing our homeworks for us, but like with any rules there are certain conditions in which to break them: never copy paste code from the internet... <strong>without understanding it first.</strong> 
<br>
<br>
There is a ton of HTML to decipher, so we will just tale a look of a small subsection of the list, namely Item 1. 
{% highlight html %}
<a href="#item-1" class="list-group-item" data-toggle="collapse">
    <i class="glyphicon glyphicon-chevron-right"></i>Item 1
  </a>
  <div class="list-group collapse" id="item-1">
    
    <a href="#item-1-1" class="list-group-item" data-toggle="collapse">
      <i class="glyphicon glyphicon-chevron-right"></i>Item 1.1
    </a>
    <div class="list-group collapse" id="item-1-1">
      <a href="#" class="list-group-item">Item 1.1.1</a>
      <a href="#" class="list-group-item">Item 1.1.2</a>
      <a href="#" class="list-group-item">Item 1.1.3</a>
    </div>
  </div>
{% endhighlight %}
The collpasing effect is achieved through assigning an html element with the class `collapse`. An anchor tag is used to toggle states between collapse and expand with an href to the id of the target element, and a Bootstrap JavaScript plugin that is called via `data-toggle="collapse"` The outline of this process is something we will adapt to our codebase.
<br>
<br>
In the html for the stretch goal I am setting up the anchor tag so that it can collapse the proceeding html that contains our smart goals. I also removed the checkbox and replaced it with an arrow glyph that will represent the state of the html element. You will see why I made this decision in a future post.
{% highlight html %}
<span class="list-group-item">
    <span class="content-container">
        <a href="#smart_<%= todo._id %>" data-toggle="collapse">
            <i class="glyphicon glyphicon-chevron-right"></i>
            <span id="content<%= todo._id %>">
                <%= todo.title %>
            </span>
        </a>
    </span>

    <span id="delete"> 
        <a href="/destroy/<%= todo._id %>" title="Delete this todo item">
            <span class="glyphicon glyphicon-trash"></span>
        </a>
        <!--<a href="/update/<%= todo._id %>">Save</a> -->
    </span>
</span>
{% endhighlight %}
On top of making the smart goals collapsable, I also added the feature that each item could be checked off.
{% highlight html %}
<div class="list-group collapse collapse-container" id="smart_<%= todo._id %>">
    <span class="list-group-item">
        <input type="checkbox" class="form-check-input" 
        id="sCheck<%= todo._id %>" 
        onclick="isChecked('sCheck<%= todo._id %>', 'specific<%= todo._id %>')">
        <span id="specific<%= todo._id %>"><%= todo.specific %></span>
    </span>
    <span class="list-group-item">
        <input type="checkbox" class="form-check-input" 
        id="mCheck<%= todo._id %>" 
        onclick="isChecked('mCheck<%= todo._id %>', 'measurable<%= todo._id %>')">
        <span id="measurable<%= todo._id %>"><%= todo.measurable %></span>
    </span>
    <span class="list-group-item">
        <input type="checkbox" class="form-check-input" 
        id="aCheck<%= todo._id %>" 
        onclick="isChecked('aCheck<%= todo._id %>', 'achievable<%= todo._id %>')">
        <span id="achievable<%= todo._id %>"><%= todo.achievable %></span>
    </span>
    <span class="list-group-item">
        <input type="checkbox" class="form-check-input" 
        id="rCheck<%= todo._id %>" 
        onclick="isChecked('rCheck<%= todo._id %>', 'realistic<%= todo._id %>')">
        <span id="realistic<%= todo._id %>"><%= todo.realistic %></span>
    </span>
    <span class="list-group-item">
        <input type="checkbox" class="form-check-input" 
        id="tCheck<%= todo._id %>" 
        onclick="isChecked('tCheck<%= todo._id %>', 'timeline<%= todo._id %>')">
        <span id="timeline<%= todo._id %>"><%= todo.timeline %></span>
    </span>
</div>
{% endhighlight %}
To finish off I want my sublist to be indented so that it is easier to see the heirarchy of to-do list items.
```
.collapse-container{
    margin-left: auto;
    width: 90%;
}
```
With that our finished product.
![todo-collapse]({{site.url}}/{{site.baseurl}}/assets/img/todo-collapse.png)
