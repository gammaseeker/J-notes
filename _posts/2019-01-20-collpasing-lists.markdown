---
layout: post
title: Collapsing Lists
date: 2019-01-20 11:45:59 -0500
categories: Programming
---
I was digging around looking for a model of a collapsing list that I could base my stretch/smart goal system off of, and thankfully I found <a href="https://jsfiddle.net/ann7tctp/">it.</a> <br>
However one of the first things I ever learned with regards to programming is:<strong>"never copy paste code from the internet."</strong> I'm pretty sure my teacher was only telling us this because he didn't want people on stackoverflow writing our homeworks for us, but like with any rules there are certain conditions in which to break them: never copy paste code from the internet... <strong>without understanding it first.</strong> <br>
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
