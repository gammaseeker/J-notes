---
layout: post
title: Cascading Style Struggles
date: 2019-01-12 1:42:59 -0500
categories: Personal
---

I think most people struggle to understand CSS, including me. It has been three years since my web development class in junior year of high school where I first learned CSS, and admittedly that’s where my skills with that language peaked. Without constant practice, the technology slowly turns from a science to magic. This is something that I am determined to change about myself. To the common populace, people do not really care or understand complex backend operations, but they can definitely identify when a website looks “aesthetic.” I want to take you along with me on my quest to conquer CSS.
![css-monster]({{site.url}}/{{site.baseurl}}/assets/img/css-monster.jpg)<br>
Recently, I’ve been working on a todo list application that I call ToDoThis. Here is the current status of the website:
![todo-current]({{site.url}}/{{site.baseurl}}/assets/img/todo-current.png)<br>
Not very impressive style-wise, but it gets the job done like any todo list app. It creates items on the list, and you can delete them when you’ve finished them. The improvement I want to make to the frontend of my application is this:<br>
![todo-wireframe]({{site.url}}/{{site.baseurl}}/assets/img/todo-wireframe.png)<br>
So my first move is to reduce the width of the borders of the todo list items and align the input box and add item button with the borders of the items.
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
