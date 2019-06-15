---
layout: post
title: node.js Project Boilerplate
date: 2019-06-14 8:59:59 -0500
categories: Programming 
---
This is post is documentation that I can look back on. The tech stack here is: Mongodb, Express, Node
Run `genWeb.sh <name_of_your_project>`
This script will generate the proper directory structure of a node project and set up the project
for version control. Go to localhost:8080 to verify set up was correct.
```
#!/bin/bash
cd projects # Assuming a directory named projects exist
mkdir $1
cd $1
npm install express
mkdir views
mkdir views/partials
touch views/partials/header.ejs
cp /home/prodigy/Templates/header.ejs views/partials/header.ejs # Assuming you have templates to copy code from
touch views/partials/footer.ejs
cp /home/prodigy/Templates/footer.ejs views/partials/footer.ejs # Assuming you have templates to copy code from
mkdir public
mkdir public/css
mkdir public/js
touch app.js
cp /home/prodigy/Templates/app.js app.js # Assuming you have templates to copy code from
git init
touch .gitignore
echo "node_modules/*" >> .gitignore
node app.js
```
After verifying the project is running, run these next commands:
```
npm init
npm install express --save
npm install ejs --save
npm install mongoose --save
```
The script `start_mongod.sh` will run a mongodb instance for your project. Run like this: `start_mongod.sh <name_of_your_project>`
```
#!/bin/bash
cd /home/prodigy/projects/$1
gnome-terminal
mongod --smallfiles
```
## Establishing Databse Connection 
In `app.js` add the following lines to the top of the file:
```
var MongoClient = require('mongodb').MongoClient;
var mongoose = require("mongoose");
var url = "mongodb://localhost:27017/<name_of_your_project>";
mongoose.connect("mongodb://localhost:27017/<name_of_your_project>", {useNewUrlParser: true});
```
Add this method to the bottom of the file, but <strong> before </strong> the app.listen handler
```
MongoClient.connect(url, {useNewUrlParser: true},function(err, db){
    if(err) throw err;
    console.log("Db created");
    db.close();
});
```
If everything it set up correctly you should see "Db created" in your console.
### Possible pit falls
"mongod address already in use error" to solve this run:
```
ps aux | grep mongod
```
Look for the pid of the `/usr/bin/mongod --config /etc/mongodb.conf` process and send signal SIGTERM to it
```
kill -9 <pid>
```
run `start_mongod.sh` again then `node app.js`