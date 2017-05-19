+++
css = []
date = "2017-05-19T14:18:15-07:00"
description = ""
draft = false
highlight = true
scripts = []
tags = []
title = "Connecting Watson && Kitura"

+++

Hey guys! I haven't written in a bit since I was exploring some cool technologies.
In the past week, i've been hard at work learning about Kitura.
In this blog, I will explain what I have learned, and help you get started learning Kitura
and integrating your apps with Watson. Below is an iOS app that integrates text to speech
and language translation services from watson. The source code to get started can be found
<a href="https://github.com/watson-developer-cloud/text-to-speech-swift">here</a>. If you want
to check out the source code of the app I made in the video below you can find it
<a href="https://github.com/horeaporutiu/text-to-speech-swift">here</a>. I simply added
a language translation service on top of the existing text to speech service.


<video controls="controls" width="800" height="600" name="Video Name" src="../../img/watsonApp.mov"></video>

<hr>

<h4 id="setup">Getting Started</h4>
1) For macOS, Download and install <a href="https://idmsa.apple.com/IDMSWebAuth/login?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&path=%2Fdownload%2F&rv=1">
Xcode 8.3</a>. For Ubuntu Linux, follow  <a href="http://www.kitura.io/en/starter/settingup.html"> These steps</a>
2) Create a new project directory

<pre><code class="language-toml">$ mkdir kituraProj
$ cd kituraProj
</code></pre>

3) Create a new Swift Project using the Swift Package Manager
<pre><code class="language-toml">$ swift package init --type executable
</code></pre>
<br>
<h4 id="setup">Adding Kitura to Swift Project</h4>


Next we have to add dependencies and let Swift download all of the
packages it needs to run the Kitura server. To do this, we have to add some
lines in our <b>Package.swift</b> file.

<pre><code class="language-toml">
import PackageDescription

let package = Package(
    name: "myFirstProject",
    dependencies: [
        .Package(url: "https://github.com/IBM-Swift/Kitura.git", majorVersion: 1, minor: 7),
        .Package(url: "https://github.com/IBM-Swift/HeliumLogger.git", majorVersion: 1, minor: 7)
    ])

</code></pre>
<br>
<h4 id="setup">Running Kitura Server</h4>

Next, we have to specify where we want to have our server.
Change the <b>Sources/main.swift</b> file to look like this:

<pre><code class="language-toml">import Kitura

// Create a new router
let router = Router()

// Handle HTTP GET requests to /
router.get("/") {
    request, response, next in
    response.send("Hello, World!")
    next()
}

// Add an HTTP server and connect it to the router
Kitura.addHTTPServer(onPort: 8080, with: router)

// Start the Kitura runloop (this call never returns)
Kitura.run()
</code></pre>

Compile the app.

<pre><code class="language-toml">$ swift build
</code></pre>

Create an xcode app.
<pre><code class="language-toml">$ swift package generate-xcodeproj
</code></pre>

Open the project in Xcode.

<pre><code class="language-toml">$ open kituraProj.xcodeproj
</code></pre>

Change scheme to be as shown below.
<img src="../../img/manageScheme.png" alt="Mountain View" style="width:600px;height:330px;">

Run the project. Product -> Run. Allow incoming connections.
<br>
Open your browser at http://localhost:8080
<hr>
<br>
<h4 id="setup">Hosting Static Content</h4>

To host simple static sites, you can simply add this line in your <b>main.swift</b> file. This will
look for any files in the 'public' directory. Put all of your styling files such as CSS and HTML in that directory.

<pre><code class="language-toml">$ router.all("/", middleware: StaticFileServer())
</code></pre>

Then create your public directory, add a simple index.html file in there, and add some code.

<pre><code class="language-toml">$ mkdir public
$ touch index.html
</code></pre>

In the index file, add a basic skeleton. You can find one here: http://htmlshell.com/
Run the app again, Open your browser at http://localhost:8080 and your new site should be there!
<hr>
<br>
<h4 id="setup">Connecting Watson and Kitura</h4>

To connect to watson, first clone a sample app.

<pre><code class="language-toml">$ git clone https://github.com/watson-developer-cloud/text-to-speech-swift.git
</code></pre>

Follow the instructions https://github.com/watson-developer-cloud/text-to-speech-swift to get started.
Once you have your app working, we want to have the server side code and the client side code different
directories. One directory should be your kituraProj(server side), and the other is watsonApp.
<hr>
<br>
<h4 id="setup">Watson Translates</h4>
<br>

To add Swift SDK frameworks, we first need to add the frameworks in our linked frameworks.
Watch the video below to learn how to add the frameworks by going into our Carthage directory
and opening the correct file. The last step in the video shows adding the
"Run Scrip Phase" in the "Build Phases" section of our app.

<video controls="controls" width="800" height="600" name="Video Name" src="../../img/setupLanguage.mov"></video>

<br>
<hr>

Right under the "Run Script", you will see Input Files. Click on the "+" icon, and add the following lines:
<pre><code class="language-toml">$(SRCROOT)/Carthage/Build/iOS/LanguageTranslatorV2.framework
</code></pre>

For the last step, we simply need to open the plist.info file -> view as source code. Then add these lines
from <a href="https://github.com/watson-developer-cloud/swift-sdk/blob/master/docs/quickstart.md#add-exception-for-app-transport-security">here</a>.

We are ready to add the language translation code! Let's do it!

Add this code to your view controller, and you are all set! Enjoy!
<pre><code class="language-toml">import LanguageTranslatorV2

let username = "your-username-here"
let password = "your-password-here"
let languageTranslator = LanguageTranslator(username: username, password: password)

// set the serviceURL property to use the legacy Language Translation service
// languageTranslator.serviceURL = "https://gateway.watsonplatform.net/language-translation/api"

let failure = { (error: Error) in print(error) }
languageTranslator.translate("Hello", from: "en", to: "es", failure: failure) {
    translation in
    print(translation)
}
</code></pre>
<br>
<h4 id="">Conclusion</h4>

Building an end-to-end app with Swift and Kitura has never been easier. Also,
integrating with Watson is relatively easy if you follow these guidelines. Find out
more about kitura <a href="http://www.kitura.io/">here</a>. Until next time!
