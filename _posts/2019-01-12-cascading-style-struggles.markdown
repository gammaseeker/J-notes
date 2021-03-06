---
layout: post
title: Cascading Style Struggles
date: 2019-01-12 1:42:59 -0500
categories: Programming 
---

I think most people struggle to understand CSS, including me. It has been three years since my web development class in junior year of high school where I first learned CSS, and admittedly that’s where my skills with that language peaked. Without constant practice, the technology slowly turns from a science to magic. This is something that I am determined to change about myself. To the common populace, people do not really care or understand complex backend operations, but they can definitely identify when a website looks “aesthetic.” I want to take you along with me on my quest to conquer CSS.
![css-monster]({{site.url}}/{{site.baseurl}}/assets/img/css-monster.jpg)<br>
Recently, I’ve been working on a todo list application that I call ToDoThis. Here is the current status of the website:
![todo-current]({{site.url}}/{{site.baseurl}}/assets/img/todo-current.png)<br>
Not very impressive style-wise, but it gets the job done like any todo list app. It creates items on the list, and you can delete them when you’ve finished them. The improvement I want to make to the frontend of my application is this:<br>
![todo-wireframe]({{site.url}}/{{site.baseurl}}/assets/img/todo-wireframe.png)<br>
So my first move was to reduce the width of the borders of the todo list items and align the input box and add item button with the borders of the items.
{% highlight css %}
#container
{
    text-align:center;
    width:25%; 
    height: 20%;
    margin: 0 auto;
}
input
{
   width: 17%;
   height: 30px;
   float: left; 
   margin-left: 47%;
}
button
{
    margin-right: 22%;
    float: right;
}
{% endhighlight %}
Next was to be rid of the awkward placement of the delete feature, and replace it with a trash can icon along with adding in checkboxes that would denote whether a task was completed or not. I also took the liberty of adding in a functionality where if the checkbox was checked off, it would strikethrough the adjacent text.
{% highlight html %}
<div id = "container" class="list-group">
      <% todos.forEach( function( todo ) { %>
        <span class="list-group-item list-group-item-action"> 
                <input type="checkbox" class="form-check-input" id="check<%= todo._id %>" onclick="isChecked('check<%= todo._id %>', 'content<%= todo._id %>')">
                <label class="form-check-label" for="check<%= todo._id %>" id="content<%= todo._id %>">
                    <%= todo.title %>
                </label>
            <span id="delete"> 
                <a href="/destroy/<%= todo._id %>" title="Delete this todo item">
                    <span class="glyphicon glyphicon-trash"></span>
                </a> 
            </span>
        </span>
      <% }); %>
</div>
{% endhighlight %}
{% highlight javascript %}
function isChecked(check_id, content_id){
    cbox = document.getElementById(check_id);
    content = document.getElementById(content_id);
    if(cbox.checked){
        content.style.textDecoration = "line-through";
    }else{
        content.style.textDecoration = "initial";
    }
}
{% endhighlight %}
```
.list-group-item
{
    border: 2px solid #ddd;
}
a
{
    color:inherit;
}
#delete
{
    float: right;
    color: red;
}

.form-check-label
{
    font-weight: inherit;
}

.form-check-input
{
    float: left;
    width: 17px;
    height: 17px;
}
```
So the last thing remaining is to add in that sidebar. 
{% highlight html %}
<div class="side-col">
        <div id="border-div">
                <img id="pfp" src="img/pfp.jpg">
        </div>
        <div id="ltg">
                Long Term Goals:
        </div>
</div>
{% endhighlight %}
```
html,body 
{ 
    height:100%; 
}
#pfp 
{
    width: 200px;
    height: 200px;
    border-radius: 50%;
}

.side-col
{
    margin-left: 2%;
    float: left;
    height: 100%;
}
#border-div
{
    border-right: 2px solid black;
    border-bottom: 2px solid black;
}
#ltg
{
    font-size: 18pt;
    text-align: center;
    border-right: 2px solid black;
    height: 100%;
}
```
![todo-sidebar]({{site.url}}/{{site.baseurl}}/assets/img/todo-sidebar.png)
And with that, ToDoThis is <i>slightly</i> better styled. Check out my code <a href="https://github.com/gammaseeker/ToDoThis">here</a><br>
![todo-done]({{site.url}}/{{site.baseurl}}/assets/img/todo-done.png)
