+++
css = []
date = "2017-05-05T14:18:15-07:00"
description = ""
draft = false
highlight = true
scripts = []
tags = []
title = "OpenWhisk Actions & API calls"

+++
In this blog, I will go over some of the basics of OpenWhisk and go over a simple
example of an action that will load weather for your area. I assume you already have a Bluemix
account. If you do not, go <a href="https://console.ng.bluemix.net/registration/">here</a>
to get one. <hr>

<h4 id="setup">Initial Setup</h4>

1) Setup <a href="https://console.ng.bluemix.net/openwhisk/cli">OpenWhisk CLI</a>  (Command Line Interface).
If you've verified your setup from the setup above, you should be good to go! If you were unable to install
the CLI, one problem might be that you need to give your computer permission to install it. For me, I had to go
to System Preferences -> Security & Privacy -> Allow apps downloaded from and click allow for this CLI.  

2) Put wsk in your PATH. Simply drag and drop the 'wsk' executable that you downloaded to /usr/local/bin (for macOS users) and
you should be able to use the wsk command. For other users, you can simply go to the folder where the 'wsk' executable is located
and you should be able to use ./wsk

<hr>
<h4 id="">Creating Actions</h4>
Actions run on the Bluemix platform in Swift, Java, Python, JavaScript or in a Docker container.
They can be used for many things, such as posting a Tweet or making API calls. We will do the ladder.
Let's start by creating a JavaScript file called 'hello.js'. Type in the following in the file:

<pre><code class="language-toml">function main() {
   return {payload: 'Hello world'};
}
</code></pre>

Let's create an action called 'hello' with the wsk action create command.

<pre><code class="language-toml">$ wsk action create hello hello.js
</code></pre>

You should get the output: ok: created action hello.
Just to make sure, let's list the actions we have created.

<pre><code class="language-toml"> $ wsk action list
</code></pre>

You should see:

<pre><code class="language-toml">actions
hello     private
</code></pre>

<h4 id="">Invoking Actions</h4>
We can run actions with the 'invoke' command. Let's try it out!

<pre><code class="language-toml"> $ wsk action invoke --blocking hello
</code></pre>

You should see:

<pre><code class="language-toml"> ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
{
   "result": {
       "payload": "Hello world"
   },
   "status": "success",
   "success": true
}
</code></pre>

Nice! We got what we wanted: Hello world printed to the screen in the form of result!
This id can be used if we ever want the result of this function again.
<hr>
<h4 id="">Actions & APIs</h4>

Now let's try an example that calls a Yahoo Weather Service API. Create a file
called weather.js. Write the following code in the file:

<pre><code class="language-toml">
var request = require('request');

function main(params) {
   var location = params.location || 'Vermont';
   var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';

   return new Promise(function(resolve, reject) {
       request.get(url, function(error, response, body) {
           if (error) {
               reject(error);
           }
           else {
               var condition = JSON.parse(body).query.results.channel.item.condition;
               var text = condition.text;
               var temperature = condition.temp;
               var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
               resolve({msg: output});
           }
       });
   });
}
</code></pre>
Let's break down the important parts of this code. <br>
1) location is the param that we will pass in when invoking the action from the command line.<br>
2) url is where we store the result from the API call in a JSON format.<br>
3) condition stores the result of parsing through the JSON that the API call returns<br>
4) We return a Promise because the result of this action is not available yet when the function returns.<br>
5) The result is returned in the <b>request</b> callback
<hr>

<h4 id="">Execute</h4>

Run these commands to create and invoke an action:

<pre><code class="language-toml">$ wsk action create weather weather.js<br>
$ wsk action invoke --blocking --result weather --param location "Brooklyn, NY"
</code></pre>

You should see the following output:

<pre><code class="language-toml">{
   "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
}
</code></pre>
And there we go, we created an OpenWhisk action that loads
weather for our specified area!
<hr>
<h4 id="">Final Remarks</h4>
The powerful idea behind OpenWhisk is that you do not have to develop a complex
backend from scratch. You can simply make multiple API calls to translate or
output your data exactly as you need. OpenWhisk has many other packages that
you could use by simply entering this in terminal: <pre><code class="language-toml"> $ wsk package	list /whisk.system
</code></pre>
For more info about OpenWhisk click <a href="https://console.ng.bluemix.net/docs/openwhisk/index.html#getting-started-with-openwhisk">here</a>. Enjoy!
