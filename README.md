# Error-Handling-Presentation
## How to get started
1. Pull the documents down from Github.
2. Put ALL the files into a folder.
3. Open CMD(PC) or Terminal(MAC).
4. Go to the folder where all the files are located.
5. Type "npm start" to start the localhost server.
6. Open Browser and go to "http://localhost:3000" to open the web app.


### Step 1
Main-project/error.ejs:29

Adding the Message to display the error on the page.


````
<div class="container">
    <h1><%= message %></h1>
    <hr>
    <h2>Error Status: <%= error.status %></h2>
    <div class="well">
        <p><%= error.stack %></p>
    </div>
     <hr>
````


### Step 2
Main-project/app.js:28
Catching the 404 and forwarding to the error handler.

````
app.use(function(req, res, next) {
  var err = new Error('Not Found');
  err.status = 404;
  next(err);
});
````



### Step 3
Main-project/app.js:35
Error handing. This will print the stacktrace.

````
if (app.get('env') === 'development') {
  app.use(function(err, req, res, next) {
    res.status(err.status || 500);
    res.render('error', {
      message: err.message,
      error: err
    });
  });
}
````


### Step 4
Main-project/app.js:43
This is the production error handler, it makes sure the stacktraces are not leaked to user

````
app.use(function(err, req, res, next) {
  res.status(err.status || 500);
  res.render('error', {
    message: err.message,
    error: {}
  });
});
````

