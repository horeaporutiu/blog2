+++
date = "2017-10-09T15:13:21-07:00"
title = "Call External API From Watson Conversation"

+++

I've had a lot of trouble tackling this problem in the past when I
 wanted to create chatbots with Watson Conversation. I've also read
 countless posts that didn't explain it to the level where I felt 
comfortable doing this on my own. Let me try to bridge that gap.
In this post, i'll use <b>Node.js</b> to show you how to create an instance of the Watson Conversation API using a REST call, and then call
another API before returning a response to the user! Nice! The <a href="https://github.com/horeaporutiu/Watson-Conversation-External-API">code</a> can be found on Github. Also, I will use NPM (Node Package Manager), so you will need to <a href="https://www.npmjs.com/get-npm">install it</a> if you do not have it.

<b><h4 id="setup">Getting Started</h4></b>

1) Create Watson Conversation service in Bluemix.

2) Click on your Conversation Service in Bluemix, then click 'Launch tool' to get to the Watson Conversation interface.

3) Create a new workspace and inside this workspace create an intent called 'translate'.

4) Add 'translate this phrase.' as a user example for this intent.

5) Go back to your main page for your workspace, click on the three dots and then click 'view details' and copy your
Workspace ID to have handy for later.

<b><h4 id="setup">Code</h4></b>

In my code, I will set up a simple server to run on port 8081(not shown below for simplicity), and then create an instance of the Watson Conversation API. You will need your own username and password from your Bluemix credentials page. 

```javascript
var watson = require('watson-developer-cloud');

var conversation = watson.conversation({
    username: conversationUserame,
    password: conversationPassword,
    version: 'v1',
    version_date: '2017-05-26'
  });

```
<br>
I then call the message API (you need to input your workspace id from above),
 and pass in a phrase that will trigger our 'translate' intent. Then, in our callback
function, we check to make sure Watson has identified the correct intent, and then call our translate function(which
will call our external API). <b> Your translate function can be different than mine - that is where you will do your 
external call to the API.</b> After our external API returns, we simply set the output text to be the response of our
API call. 

```javascript
var context = {};
  
  conversation.message({
    workspace_id: 'your workspace id',
    input: {'text': 'translate this phrase.'},
    context: context
  },  function(err, response) {
    if (err)
      console.log('error:', err);
    else {
      console.log(response)
      if(response.intents.length > 0 && response.intents[0].intent === 'translate'){
        translate(response.input.text).then(function(translatedResopnse){
          response.output.text = translatedResopnse
          console.log(JSON.stringify(response,null,2))        
        });
      }
    }

  });

```
<br>
That's pretty much all there is to it. Also, here is the translate function, which will call the Watson Translation 
API and translate the phrase from our user. You will need service credentials for this call as you did for the 
Conversation API. I return a promise to make sure that only after the external API finished, the Conversation will
return the response to the user. Otherwise, we might get errors.

```javascript
function translate(userInput) {

  return new Promise((resolve, reject) => {

    var data = {};
    
    data.source = 'en';
    data.target = 'es';
    data.text = userInput;
    
    request.post({
        headers: {'content-type':'application/json'},
        url : transUrl,
        json : data,
        auth: {
          user: translationUsername,
          pass: translationPassword
        }
    }, function (error, response, body){
        if (error) {
            console.log(error);
            resolve(error);
        } else {
            console.log(body);
            resolve(body.translations[0].translation);
        }
    });

  });        

}

```

<b><h4 id="setup">Results</h4></b>

Our console should look something like this if everything went smoothly. <img class = "pic" width="50%" height="50%"src="../../img/watsonConsole.png" alt="Mountain View" >

 Once again, if you want to see the full code (creating server and all), please check out my <a href="https://github.com/horeaporutiu/Watson-Conversation-External-API">Github repo</a>. And of course, if this helped you at all please star it ;)

<b><h4 id="setup">Conclusion</h4></b>

Watson Conversation is an extremely powerful service that can be 
used to call external APIs with moderate ease. If you need more help,
please also check out the official <a href="https://www.ibm.com/watson/developercloud/conversation/api/v1/?node#send_message">API docs</a>.








