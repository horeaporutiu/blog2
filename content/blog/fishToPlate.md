+++
css = []
date = "2018-02-13"
description = ""
draft = false
highlight = true
scripts = []
tags = []
title = "How Hyperledger blockchain tracks your fish from ocean to plate"

+++

Look, it’s been a long day. 7:15 wake up, 7:30 call, work, gym, bike to work, eat, bike to meetup, take notes, talk, network, come home, see a nice juicy piece of salmon on the table.


<br>

<center><img class = "pic" src="../../img/salmon.jpg" alt="Mountain View" ></center>
<br>
<center><b>Nice slab of salmon sitting out.</b></center>

<br>

WHAT? Yup, you heard me right. I walk into my flat a few minutes past 9PM, back from the <a href="https://www.meetup.com/Hyperledger-SF/events/247293511/">Hyperledger Meetup</a>. And I just see a raw piece of salmon sitting out. That’s that ‘Wild Sockeye Salmon’ from Trader Joes. But I can’t stop from thinking,

```
“how do I actually know it’s wild caught, and not simply marketed as so?”
```

Well, that’s what Intel has been doing with the help of a Linux Foundation project called Hyperledger <a href="https://www.hyperledger.org/projects/sawtooth">Sawtooth</a>. But before we get into that, let’s back up.<br>


<br>

<center><img class = "pic" src="../../img/jquery.jpg" alt="Mountain View" ></center>
<br>
<center><b>The <a href="https://js.foundation/">JavaScript Foundation</a>, a project of the Linux Foundation, is responsible for creating <a href=http://jquery.com/>jQuery</a>, a popular JavaScript library.</b></center>

<br>

<h4 id="setup">What is the Linux Foundation?
</h4>


<ol>
  <li><b>It’s open-source.</b> Not only that, but it’s the largest open-source non-profit org in the world.</b>
  </li>
  <br>

  <li><b>It’s community-based.</b> 10/10 of the largest cloud service providers contribute (write or ‘donate’ code) to the Linux Foundation projects.</li> 
  <br>
  <li><b>It’s the largest shared tech investment. </b> $16 billion is the estimated development cost of the Linux Foundation projects.</li>
  <br>
  <li><b>It’s about deploying code. </b> The purpose of the foundation is to accelerate tech development, and to help speed commercial adoption.</li>
</ol>
<br>
Some of its notable projects include: Node.js, Kubernetes, and of course, <a href="https://www.linuxfoundation.org/projects/linux/">Linux itself</a>. Okay, the Linux Foundation has a good track record, sure, but what does Hyperledger have to do with the Linux Foundation?

<center><img class = "pic" src="../../img/fish.jpg" alt="Mountain View" ></center>
<br>
<center><b>How can you keep track of fish while possession moves from the ocean, to port, to factory, and ultimately to your plate?</b></center>

<h4 id="setup">Hyperledger in the wild
</h4>

<ol>
  <li><b>An umbrella project.</b> Hyperledger actually has five ‘frameworks’, commonly known as Sawtooth, Iroha, Fabric, Burrow, and Indy.</b>
  </li>
  <br>

  <li><b>Seafood Traceability.</b> Back to that nice salmon. It’s sitting there, and you paid twice the amount since it had <i>‘wild’</i> prefixed to the name. Sawtooth ensures that you are getting your money’s worth. But how?</li> 
  <br>
  <li><b>IoT sensor enabled. </b> Sensors attach to the seafood and continually send data about time and location to the blockchain. As possession changes hands (from fisherman to processing plant), the events are recorded in the ledger.</li>
  <br>
  <li><b>The buyer trusts the product. </b> Since the buyer can view a record of the fish’s journey from the fisherman all the way to the retailer, the buyer trusts the product.</li>
</ol>

<center><img class = "pic" src="../../img/plumber.jpg" alt="Mountain View" ></center>
<br>
<center><b>Plumbing is not fun.

</b></center>

<h4 id="setup">Why open-source?

</h4>

While writing high-level business logic is pretty fun, and is usually specific to a certain company’s business model, you need underlying technology to do the low-level things so that you can build business logic on top of it. The low-level stuff is like plumbing. It’s something that needs to be done, but it’s not pretty. This is where the open-source community comes in. Since there is so much interest blockchain technology, developers are willing to take the time to do the low-level ‘plumbing’ in order to create a <b>baseline or ‘platform’ for all blockchain applications</b>. The platform has to be so broad that you can build an app for any use case. And along with this low-level platform, you’ll need tools to build that next app you have been dreaming of.


<br>

<center><img class = "pic" src="../../img/tools.jpg" alt="Mountain View" ></center>
<br>
<center><b>Photo by Barn Images on Unsplash

</b></center>

<h4 id="setup">Hyperledger Tools</h4>

<ol>
  <li><b>Hyperledger Quilt.  </b> What happens when you have multiple ledgers but they can’t communicate with each other? Quilt offers a way to transfer value between distributed and non-distributed ledger systems with the ILP protocol.</li><br>
  <li><b>Hyperledger Cello.</b> This tool helps reduce the effort in creating, managing, and terminating blockchains.</li> <br>
  <li><b>Hyperledger Explorer. </b> Much like its name, this tool helps visualize, query, or invoke transactions and associated data as well as other info that is stored in the ledger.</li><br>
  <li><b>Hyperledger Composer. </b> While this project is still in incubation, the most advanced of the Hyperledger tools is Composer, which offers an accelerated time-to-value for building blockchain applications. This tool works <b>on top of</b> Hyperledger Fabric, and provides an easy editor to develop smart contracts, and the details of a business network. If you want to understand Hyperledger Fabric, this tool is a good place to start.
</li> 
</ol>

<br>

<center><img class = "pic" src="../../img/chain.jpg" alt="Mountain View" ></center>
<br>
<center><b>Expect more (block)chain solutions to dominate headlines in 2018.


</b></center>

<h4 id="setup">What’s Next?</h4>

As Fabric is nearing a V1.1 release, expect more Proof-Of-Concepts to be developed on the <i>‘granddaddy’</i> of the Hyperledger projects. Not only that, but expect <b>more tooling</b> to be built around the Hyperledger frameworks. With many companies keeping their blockchain solutions private, 2018 will be the year where solutions start going public. Another big problem that we have seen with the popularity of blockchain and cryptocurrencies is the fragile infrastructure behind these applications. Binance has recently been down. Coinbase has been quite slow in validating transactions. This is <b>a problem that is seen when your system doubles in popularity</b>. For the web, in the dot com era, CDNs such as Cloudflare were created to ensure that an increase in traffic will keep your application running smoothly. Nothing like this exists for blockchain today.

<hr>


Since the technology is so new, there is SO much opportunity for development in this space. And this is exactly why I am so excited and blessed to be working and learning about this incredible new space. Stay hungry out there! Horea Call of Duty in :)