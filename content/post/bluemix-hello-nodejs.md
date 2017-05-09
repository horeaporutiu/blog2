+++
css = []
date = "2017-05-04T14:18:15-07:00"
description = ""
draft = false
highlight = true
scripts = []
tags = []
title = "Run Node.js server with Bluemix"

+++
Let's learn how to build that Node.js web-server using Bluemix! If you prefer video
tutorials, please watch <a href="https://www.youtube.com/watch?v=enTQkCb8vlU&t=4s">my video</a> on this topic.
Before we start, you will need to do a few things.

<hr>
<h4 id="setup">Initial Setup</h4>

1) Get a <a href="https://console.ng.bluemix.net/registration/">Bluemix Account</a>

2) Install <a href="https://brew.sh/">Homebrew</a> if you have a mac. Otherwise, skip this step.

3) Install npm/node <a href="http://blog.teamtreehouse.com/install-node-js-npm-mac"> for Mac</a> or npm/node
<a href="http://blog.teamtreehouse.com/install-node-js-npm-windows"> for Windows</a>

4) Install <a href="https://github.com/cloudfoundry/cli#downloads">cf</a>
command line tool<hr>

<h4 id="code">Starter Code</h4>
Open up terminal, and use the following git commands:

<pre><code class="language-toml">$ git clone https://github.com/IBM-Bluemix/bluemix-hello-node
$ cd bluemix-hello-node</code></pre>
<br>
<h4 id="test">Test Locally</h4>

<pre><code class="language-toml">$ npm install
$ npm start
</code></pre>
Once the server is up and running, you can type in your browser “localhost:8080” and you should see the hello world app. If the page is blank, or there is an error, make sure you are in the bluemix-hello-node directory and that there are no
errors in the installation of npm or starting the server.<br>

If everything is all and well, your site should look similar to this: <img src="../../img/hello.png" alt="Mountain View" style="width:600px;height:228px;">

<br><br>

<h4 id="Bluemix">Bluemix Login</h4>

Firstly, set the enviornment with the cf api command:

<pre><code class="language-toml">$ cf api https://api.ng.bluemix.net
</code></pre>

If all went well, you should see this:

Setting api endpoint to https://api.ng.bluemix.net...
OK


Next we need to login to Bluemix:

<pre><code class="language-toml">$ cf login
</code></pre>

If you have a IBM w3ID, this will not work, and you will have to use this command
instead:

<pre><code class="language-toml">$ cf login -sso
</code></pre>

You’ll get prompted with a one time code, and then you can simply copy and paste that code to login.
<hr>
<h4 id="deploy">Deploy</h4>

This is the cool part! Getting to put that app out there!

Firstly, let’s open up our manifest.yml in your favorite text editor, mine being <a href="https://atom.io/">Atom</a>.

Now we must come up with a unique URL for our site. This is done by changing the host: line in the manifest.yml file.

Change the line host: hello-node to username-hello-node. Should look similar to this, except with your
own user name, not mine. <img src="../../img/hostName.png" alt="Mountain View" style="width:600px;height:100px;">

One last command:

<pre><code class="language-toml">$ cf push
</code></pre>

If you run into this error <img src="../../img/failed.png" alt="Mountain View" style="width:600px;height:130px;"> it is because the name is not unique.
<hr>
<h4 id="conclusion">Conclusion</h4>


If there are no errors, you are officially deployed! Go to http://username-hello-node.mybluemix.net/ to see your finished product! One last thing: if you want to make some changes, simply change something in the index.html file for example, and then just use cf push to deploy your latest changes. Happy coding!
