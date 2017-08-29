+++
date = "2017-08-28T11:11:20-07:00"
title = "Updating Cloudant Database via Rest API"

+++

Trying to update your Cloudant Database via REST API? Not sure how to get
started? You've come to the right place. In this post, I'll teach you
how to update your database programmatically using Node.js and REST API
calls. As a bonus, I'll show you how to keep
track of the objects in your database, and how to sort your database according
to your most popular objects.

I will assume you have created a Cloudant account through IBM Cloud
<a href="https://console.bluemix.net/registration/">"Bluemix"</a>, and
have created a database and a document through the Cloudant UI. (There is a
create database and create document button at the top-right corner of Cloudant
Website.) Now let's get to the fun part.

<b><h4 id="setup">Getting the Current State of our Database</h4></b>
The first thing we want to do is make a simple 'GET' request to get the current
state of our database. To setup our GET request, we need to provide our
authentication and Cloudant URL. This should look something like this:
P.S (The below username and password do NOT work, they are simply for learning
  purposes.)
```javascript

var auth = 'Basic ' + new Buffer("https://8bb71405-438f-4372-9b43-975e0220f3cd-bluemix" +
':' +"935624a91478c5f8918d3d0b2e104ef6fe825939ed2304f28ec2225fa9a952df").toString('base64');

var options = {
  url: https://8bb71405-438f-4372-9b43-975e0220f3cd-bluemix.cloudant.com/db1/1e37764c1dfc4d448bc2450e9c04ecd0,
  method: 'GET',
  headers: {
      'Authorization': auth;
  }
};
```
<br>
The first thing to note is <mark>the URL</mark>. The first part of the URL is simply
your username - it ends with '-bluemix.cloudant.com'. The next part of the URL
is your specific database. In my case, I named my database 'db1'. The last part of
the URL is the specific document in that database. The document that I created
in 'db1' has an 'id' of "1e37764c1dfc4d448bc2450e9c04ecd0". Next, your
authentication. The first part of the authentication header is your Cloudant
Username - the first part of the URL. The second (and last) part of the
authentication is simply your Cloudant Password. Now, let's use the
request package (if you don't have it, you can simply do an npm install request)
to make the GET call.

```javascript
request.get(options, function(err, body){
  if (err) {
    console.log(err);
  }
  var docObj = JSON.parse(body.body)
  var revID = docObj._rev;
}
```
<b><h4 id="setup">Inserting into Cloudant</h4></b>
The most important part of the request body is the Revision ID or '._rev'.
This is a number that Cloudant assigns to keep track of the number of times
you have updated your specific document. <mark>We need this number to
update our database</mark>.
Now that we have the revision ID number, we can use that to update the same
document over and over. To insert into our database, we will simply make a
PUT request and use the revID that we got from the GET request to ensure
that we will update our current document. As an example, I simply inserted a
tennis player into the database.
```javascript
request.get(options, function(err, body){
  var docObj = JSON.parse(body.body)
  var revID = docObj._rev;
  var tennisPlayers = {name:'Andre Agassi'}

  var putOptions = {
    url: https://8bb71405-438f-4372-9b43-975e0220f3cd-bluemix.cloudant.com/db1/1e37764c1dfc4d448bc2450e9c04ecd0,
    method: 'PUT',
    json: {
      '_rev': revID,
      'index':tennisPlayers //where all of our data goes
    },
    headers: {
        'Authorization': auth,
        'Content-Type': 'application/json' //needed since we are inserting json
    }
  };

  request.put(putOptions, function(err, body){
    console.log(body) //should give you a message saying that you have successfully inserted
  });
}
```
<b><h4 id="setup">Bonus: Sorting Database by Relevance</h4></b>
In this last section, i'll show you how to sort your database by
relevance using a simple sort function. Let's say you want to sort a
database of tennis players by the number of grand slams they win.
Let's say you want to update after every Grand Slam.
```javascript
var grandSlamWinners = [
  {name:'Rafael Nadal',grandSlams:'15'},
  {name:'Andre Agassi',grandSlams:'8'},
  {name:'Roger Federer',grandSlams:'19'}
]
```
<br>
Let's suppose Roger Federer wins the 2017 US Open...which would
be a 'joke' as quoted by Federer himself. Then we would want to increment
the number of slams he has. Thus, we need to search through the
database to see if the player has already won a slam, and if he
has, then we want to increment his number of slams. Otherwise,
its their first slam and we insert and them with their first Grand
Slam. P.S. (You will probably want to do a check if the database
is empty, and if it is, insert anyway, but this is beside the point).

```javascript
var tennisPlayerToInsert = {name:'Roger Federer'}
var insertIntoDict = true;

  //check every player in the database for a match
  for(var i=0;i<grandSlamWinners.length;i++){
     if (grandSlamWinners[i].name == tennisPlayerToInsert.name) {
       insertIntoDict=false;
       grandSlamWinners[i].grandSlams++;
       break;
     }
  }
  //if player is not in DB, add it!
  if(insertIntoDict){
    grandSlamWinners.push({
      name: tennisPlayerToInsert.name,
      grandSlams: 1
    });
  }

```
<br>
First we check every single player in database to check if the US Open
Slam Winner is a past winner. If they are, we set the flag to false,
and increment their slam number. Otherwise, congrats on their first slam!
One more bit...let's sort by descending slams, since we want to see
the most famous players first.

```javascript
grandSlamWinners.sort(function(a, b) {
  return (b.grandSlams) - (a.grandSlams);
});
```
<br>
And that's it! Hope you learned a bit more about Cloudant and databases
in general.
