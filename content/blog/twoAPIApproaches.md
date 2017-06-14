+++
date = "2017-06-13T16:14:34-07:00"
title = "Two Approaches to API Calls with Server-Side Swift"

+++

In this blog, i'm going to go over how to make an HTTP Post Request using
Kitura (A Server-Side Swift Framework). First i'll be making Post Requests using
URLSession, and then using KituraNet. If you are not
sure how to start up a Kitura project, go
<a href="http://www.kitura.io/en/starter/gettingstarted.html">here</a>. If you
want to see another implementation of a HTTP Post Request with KituraNet,
<a href="https://akrabat.com/posting-data-using-kituranet/">Rob Allen</a>
does a great job explaining his code.  

The completed code for the URLSession Request is as follows:
```javascript
import Kitura
import Foundation

let router = Router()
router.post(middleware: BodyParser())

var parameters = [String:String]()

router.post("/players") { request, res, next in

    //fill with actual data
    parameters["tennisPlayer"] = "Rafael Nadal"

    let url = URL(string: "your-url-here")
    var request = URLRequest(url: url!)
    request.httpMethod = "POST"
    //pass in JSON for http call
    let httpBody = try? JSONSerialization.data(withJSONObject: parameters, options: [])
    request.httpBody = httpBody
    //let server know we are sending and accepting JSON
    request.addValue("application/json", forHTTPHeaderField: "Content-Type")
    request.addValue("application/json", forHTTPHeaderField: "Accept")

    //URLSESSION POST REQUEST
    URLSession.shared.dataTask(with: request) { (data, response, error) in
        let returnData = String(data: data!, encoding: .utf8) //data to String
        res.send(returnData!) //send response back
    }.resume()

}
//set up Kitura to run on localhost:8080
Kitura.addHTTPServer(onPort: 8080, with: router)
Kitura.run()
```
<br>
The completed code for the HTTP Post Request using KituraNet is below:
```javascript
import Kitura
import Foundation
import SwiftyJSON
import KituraNet

let router = Router()
router.post(middleware: BodyParser()) //populates request.body with POST parameters
var parameters = [String:String]() //needed for API call
var result: String = "" //stores final JSON
router.post("/players") { request, res, next in

    // change to actual data
    let dataToSend = ["tennisPlayer": "Rafael Nadal"]
    //convert parameters to type data, done with SwiftyJSON
    let bod = try! JSON(dataToSend).rawData()

    // create the request
    var options: [ClientRequest.Options] = [
        .schema(""),
        .method("POST"),
        .hostname("your-url-here")
    ]
    //add headers - let server know we are sending and accepting JSON
    var headers = [String:String]()
    headers["Accept"] = "application/json"
    headers["Content-Type"] = "application/json"
    options.append(.headers(headers))

    let request = HTTP.request(options) { response in
        do {
          //convert ClientResponse to JSON
          if let responseStr = try response?.readString() {
              result = responseStr //result now has final JSON we want
            }
            else {
                result = "err"
            }

        } catch {
            print("Error \(error)") // error handling here
        }
    }

    request.write(from: bod) //needed to convert back into JSON
    request.end()
    //send result back to client
    res.send(result)
}
Kitura.addHTTPServer(onPort: 8080, with: router)
Kitura.run()
```
<hr>
<h3 id="">URLSession Explained</h3>


<br>
Let's take it step by step now, and explain some of the code. After
you get set up with kitura, you should have this basic code structure:


```javascript
import Kitura
import Foundation

let router = Router()
router.post(middleware: BodyParser()) //populates request body with POST parameters

router.post("/players") { request, res, next in
}

Kitura.addHTTPServer(onPort: 8080, with: router)
Kitura.run()
```
<br>
Depending on your use case, you will now need to populate the body of
the request. Check out your API documentation for details.

```javascript
parameters["tennisPlayer"] = "Rafael Nadal"
```
<br>

Next we need to specify a URL for the API call, and specify which HTTP verb
will use. In our case, it is POST.

```javascript
let url = URL(string: "your-url-here")
var request = URLRequest(url: url!)
request.httpMethod = "POST"
```
<br>
After that, we need to modify a couple other details. Let's use JSONSerialization
to go from a Foundation object to JSON data, since that is the type that
httpBody is expecting. Next we set the headers to tell the server we will be using JSON.
If you need to do basic authentication for your API call, this part can be a bit tricky.
Check out this <a
href="https://stackoverflow.com/questions/24379601/how-to-make-an-http-request-basic-auth-in-swift">
stackoverflow</a> post for more details.
```javascript
let httpBody = try? JSONSerialization.data(withJSONObject: parameters, options: [])
request.httpBody = httpBody
request.addValue("application/json", forHTTPHeaderField: "Content-Type")
request.addValue("application/json", forHTTPHeaderField: "Accept")
```
<br>
The last step is to Create the URLSession and pass in our request. Then we
have to convert our data to a readable format, like a string, and send the
response back.

```javascript
URLSession.shared.dataTask(with: request) { (data, response, error) in
    let returnData = String(data: data!, encoding: .utf8)
    res.send(returnData!)
}.resume()
```
<hr>
<h3 id="">KituraNet Explained</h3>
<br>
We start our KituraNet example with some import statements this basic code
structure. The main logic of the code will go inside the router.post statement.
```javascript
import Kitura
import Foundation
import SwiftyJSON
import KituraNet

let router = Router()
router.post(middleware: BodyParser()) //populates request.body with POST parameters
var parameters = [String:String]() //parameters for API call
var result: String = "" //stores final JSON response
router.post("/players") { request, res, next in
}
Kitura.addHTTPServer(onPort: 8080, with: router)
Kitura.run()
```
<br>
Next, we need to pass in our data. This will be different based on what API
you are using, so check your API documentation for details. After we pass in
our data, we use SwiftyJSON to convert our parameters to type "data".
```javascript
let dataToSend = ["tennisPlayer": "Rafael Nadal"]
let bod = try! JSON(dataToSend).rawData()
```
<br>
After passing in our data, we need to create the request. This part can be a
bit tricky, since sometimes the URL might be broken down into hostname and path.
For example, if your url is "https://www.yoursite.com", but the url needed to make the
call is https://www.yoursite.com/examplePath, then you might have to break up
the options into .hostname(yoursite.com) and .path(examplePath). The schema
should either be "" or "https://". If you need to add authentication, simply
add in .username("your-username-here") and .password("your-password-here").
```javascript
var options: [ClientRequest.Options] = [
    .schema(""),
    .method("POST"),
    .path("your-url-here"),
]
```
<br>
Next we create our HTTP Request, and pass in our parameters which we set above. In the request, we
convert our ClientResponse to JSON and set our result to be the response
from the HTTP Request. I'm leaving out error handling for clarity.
```javascript
let request = HTTP.request(options) { response in
    if let responseStr = try response?.readString() {
        result = responseStr
    }
}
```

<br>
Lastly, we simply need to convert our data that we sent from type "data" back
to a readable format, like JSON. The final step is to send the result to the
client.
```javascript
request.write(from: bod)
request.end()
res.send(result)
```
<br>
Please leave a comment if you have any questions.
