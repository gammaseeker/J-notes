---
layout: post
title: Stretch First, Get Smart Later
date: 2019-01-18 20:25:00 -0500
categories: Programming
---
Recently, I finished a book called <i> Smart, Faster, Better</i> by Charles Duhigg. One of the primary lessons that this book teaches is to strike a balance between wild dreams and pragmatic goals. The balance between thinking big and thinking small. So a strategy to achieve this balance is to create stretch goals supplemented with SMART goals. The idea here is that creating SMART goals provide one a more concrete plan to achieving their dreams. This type of system is something I want to implement in ToDoThis. As a disclaimer, I am going to disregard any frontend work, my main object is to get this feature working.
We need to provide the user with a form to fill out where they detail their stretch goal, and every aspect of their SMART goals. Once they submit this form, the stretch goal will appear on the to-do list with its SMART goals underneath it. So our first consideration is where to put this form, and for the time being I’m going to have a button on `index.ejs` that will send the user to `stretch.ejs` which will host the form.
{% highlight html %}
<div class="container">
    <form method="POST" action="/stretch-post">
        <label>Stretch Goal:</label>
        <input type="text" name="stretch"><br>

        <label class="smart">Specific:</label>
        <input type="text" name="specific"><br>

        <label class="smart">Measurable:</label>
        <input type="text" name="measurable"><br>

        <label class="smart">Achievable:</label>
        <input type="text" name="achievable"><br>

        <label class="smart">Realistic:</label>
        <input type="text" name="realistic"><br>

        <label class="smart">Timeline:</label>
        <input type="text" name="timeline"><br>
        
        <button class="btn btn-primary" type="submit">Add Item</button>
    </form>
</div>
{% endhighlight %}
![todo-stretch]({{site.url}}/{{site.baseurl}}/assets/img/todo-stretch.png)<br>
Next we have to edit our `todoSchema` schema such that it can handle the new information we’re passing into it.
`app.js`
{% highlight javascript %}
var todoSchema = new mongoose.Schema({
    title: String,
    strike: Boolean,
    isSmart: Boolean,
    specific: String,
    measurable: String,
    achievable: String,
    realistic: String,
    timeline: String
});
{% endhighlight %}
Now we can write our post request that will handle submissions of the form. Upon submission, the user will be redirected back to `index.ejs`
{% highlight javascript %}
app.post("/stretch-post", function(req, res){
    Todos.create({
        title: req.body.stretch,
        strike: false,
        isSmart: true,
        specific: req.body.specific,
        measurable: req.body.measurable,
        achievable: req.body.achievable,
        realistic: req.body.realistic,
        timeline: req.body.timeline
    }, function(err){
        if(err){
            console.log("error");
            } else{
                console.log("Saved stretch goal");
                res.redirect("/");
            }
        }
    );
});
{% endhighlight %}
Finally we need to write the HTML that will display the data from the form. The logic I have written into `index.ejs` checks to see if the user is just doing a quick add onto the to-do list or is setting a full on stretch goal.
`index.ejs`
{% highlight html %}
<% todos.forEach( function( todo ) { %>
    <% if(todo.isSmart){ %>
        <div class="list-group collapse" style="display: inline;">  
            <input type="checkbox" class="form-check-input" 
                id="check<%= todo._id %>" 
                onclick="isChecked('check<%= todo._id %>', 'content<%= todo._id %>')">
            <label class="form-check-label" for="check<%= todo._id %>" 
                id="content<%= todo._id %>">
                <%= todo.title %>
            </label>
            <span id="delete"> 
                <a href="/destroy/<%= todo._id %>" title="Delete this todo item">
                    <span class="glyphicon glyphicon-trash"></span>
                </a>
            </span>
                <span class="list-group-item"><%= todo.specific %></span>
                <span class="list-group-item"><%= todo.measurable %></span>
                <span class="list-group-item"><%= todo.achievable %></span>
                <span class="list-group-item"><%= todo.realistic %></span>
                <span class="list-group-item"><%= todo.timeline %></span>
        </div>
    <% } else{ %>
    <span class="list-group-item list-group-item-action">  
        <input type="checkbox" class="form-check-input" 
            id="check<%= todo._id %>" 
            onclick="isChecked('check<%= todo._id %>', 'content<%= todo._id %>')">
        <label class="form-check-label" for="check<%= todo._id %>" 
            id="content<%= todo._id %>">
            <%= todo.title %>
        </label>
        <span id="delete"> 
            <a href="/destroy/<%= todo._id %>" title="Delete this todo item">
                <span class="glyphicon glyphicon-trash"></span>
            </a>
        </span>
    </span>
    <% } %>
<% }); %>
{% endhighlight %}
![todo-stretch-done]({{site.url}}/{{site.baseurl}}/assets/img/todo-stretch-done.png)<br>
I know you’re probably throwing up at the sight of the app, but don’t worry we’re going to make all of this look spiffy!
To learn more about this goal setting methodology see this <a href="https://www.meaningfulhq.com/stretch-goals-smart-goals-examples.html">article.</a>
Check out my code <a href="https://github.com/gammaseeker/ToDoThis">here.</a>
