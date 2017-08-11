+++
date = "2017-08-10T15:56:17-07:00"
title = "Token Authentication with OpenWhisk"

+++
Ready to launch that sweet Web-App that sweeps Siri out of the water? If so,
you're in the right place. I'll show you how to <mark>generate a token
server-side</mark> for Watson's Speech
To Text Service in your Web-App.

<b><h4 id="setup">OpenWhisk</h4></b>
Now you may be thinking...OpenWhisk? Why
not use Node.js? Everyone knows Node, and there's much more documentation
if I get stuck. While I cannot refute the last statement, I'll show you why
using a new technology like OpenWhisk, similar to Amazon's Lambda, might save
you cash down the road.

<b><h4 id="setup">Getting Started</h4></b>
Every OpenWhisk function needs to have "main". Inside this function, we will
make an HTTP Request to fetch our token so that we can later use this in our
client-side code, without having to reveal our credentials.

<b><h4 id="setup">The Code</h4></b>
Don't be afraid to copy and paste. Just make sure you <mark>read the comments and
understand</mark> what you're
pasting...

```javascript

//package that we need to make an HTTP call
var request = require('request');

function main(params) {
  //Speech To Text Service Credentials
  var username = "username";
  var password = "password";

  //Authorization needs to be in base64 for some reason...
  var auth = "Basic " + new Buffer(username + ":" + password).toString("base64");

  //url for our HTTP Request
  var speechToTextUrl = "https://stream.watsonplatform.net/authorization/api/v1/token?url=https://stream.watsonplatform.net/speech-to-text/api";

  //promises are a way for our action to work asynchronously
  var promise = new Promise(function(resolve, reject) {
    request({
      url:     speechToTextUrl,
      headers : {
            "Authorization" : auth
        }
    },
    function(error, response, body){
      resolve ({
        //tell browser we will receive plain text from our HTTP Request
        headers: {
          'Content-Type': 'text/plain'
        },
        //display the token returned from our HTTP request
        body: body
      });
    });
  });
  return promise;
}

```

<b><h4 id="setup">Webify</h4></b>
The only thing we have to do is turn this into a web action. Simply
add the --web true param as shown below.
```
wsk action create {yourPackage}/speechToText speechToText.js --web true
```

<b><h4 id="setup">Conclusion</h4></b>
Now that you have a web action that returns a token, all you have to do
is make a simple XHR Request to your Web Action URL (if you do not know
what your Web Action URL is, read more <a href="https://console.bluemix.net/docs/openwhisk/openwhisk_webactions.html#openwhisk_webactions">here</a>) and you'll be ready to use Voice Recognition
in your Web-App. Since we are using a serverless (Function As A Service) cloud platform, you don't have to keep your server up 24/7 as
you would if you spun up an old-school Node.js server. What that means for you is that
you'll be saving a lot of money since you are billed <mark>a very small
percentage of a cent per second of execution</mark>. Now that's pretty neat :)  
