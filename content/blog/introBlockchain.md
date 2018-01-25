+++
date = "2018-01-19T14:12:43-08:00"
title = "Intro to Blockchain Beyond Bitcoin"

+++
<center><img class = "pic" src="../../img/bitcoinAccepted.jpg" alt="Mountain View" ></center>

<center><b>Many large companies such as Subway, Reddit, Whole Foods, and Shopify are accepting their online products to be bought with Bitcoin [1].</b></center>

Once you get that ‘a-ha’ moment and truly understand blockchain, I think you’ll see why numerous companies are changing their name to ____ blockchain. My best work as a developer is when I fully understand a solution, and am motivated to implement it. My primary goal is to get you excited (motivated) about blockchain, and share my understanding of this complex technology. It took me months before I had the ‘a-ha‘ moment, and the timing is different for everyone. Stay patient, and stay hungry. I will not show you any code, as this blog post is mostly to give you a background and comparison of different blockchains.

<br>


<center><img class = "pic" src="../../img/ledger.jpg" alt="Mountain View" ></center>
<br>
<center><b>The ledger: a key concept behind blockchain.</b></center>

<h4 id="setup">The Ledger</h4>
Before we dive into what blockchain is, we need to understand business networks first. A business network is a complex network of companies, working together to accomplish certain goals [2]. The purpose of a business is to generate value, which happens by exchanging goods and services across a business network. The goods can be tangible, like a house, or intangible, like Bitcoin. At the foundation of a business is the ledger — or a ‘master record’ of the inputs and outputs of a business [3]. Now this is important. What is recorded on these ledgers are transactions, or the communication between a buyer and a seller to exchange an asset [4]. Another term that will be critical in our discussion will be a contract, or the conditions necessary for a transaction to occur.

<br>


<h4 id="setup">The Problem</h4>
Recording transactions of goods and services, or accounting, can be traced back thousands of years, but as we evolve into the digital age, this recording process has become much more complex [5]. As the growth of e-commerce and global e-commerce continue into the 21st century, keeping track of transactions between different businesses in a business network has become increasingly difficult. Each business carries its own separate ledger and updates it for their transactions, which is a process prone to human error, malicious activity, and misinterpretation. Currently, we must rely on intermediaries such as government officials, lawyers, accountants, dealers, and banks to ensure the integrity of our transactions. The more intermediaries that are needed, the more time and money that is required. This is where blockchain comes in.

<br>

<center><img class = "pic" src="../../img/blockchainCompared.png" alt="Mountain View"></center>

<br>


<h4 id="setup">One decentralized, shared ledger</h4>
Let’s start simple: blockchain is a continuously growing list of records (a ledger). Now let’s add some buzz words. Blockchain is a ‘trusted, distributed ledger with shared business processes’. One of the main open-source blockchain platforms is the Hyperledger project. Created by the Linux Foundation, this project aims to create an architecture that allows for secure transactions between network participants. Effectively, this architecture eliminates the need of intermediaries. All the participants within a business network can view a synchronized and secure ledger of transactions, in chronological order [6]. To ensure data privacy, blocks can be encrypted using cryptography, making them much harder to corrupt.


<br>

<center><img class = "pic" src="../../img/consensus.jpg" alt="Mountain View" ></center>

<center><b>Consensus is the process by which transactions are ordered onto the blockchain.</b></center>

<br>


<h4 id="setup">Consensus</h4>
When you go to the bank to make a transaction you wait in line for your turn. It’s simple, since if there are people in front of you, you just go wait behind them, and if not, even better. In a decentralized network, there is no sign that says, ‘please start the line here’ with a nice line drawn to show where the line starts. So, who then determines the order of the transactions? This is where the lines are blurred. With Bitcoin, the algorithm called ‘proof of work’ determines the order in which transactions are chained together. For your transaction to be a part of the Bitcoin blockchain, a node, or participant, in the network must solve a time-intensive problem and other nodes will have to verify this solution. Think of it like putting together a 10,000-piece puzzle. It takes hours to put together, but when someone sees it, they can instantly tell that it’s correct. Hyperledger, on the other hand, is created to be modular and extensible for any business network. By this same token, its consensus algorithms vary widely, depending on the use case.

<br>



<center><img class = "pic" src="../../img/smartContracts.jpg" alt="Mountain View" ></center>
<center><b>Smart contracts take care of validating and if need be, rejecting transactions.</center></b>


<br>


<h4 id="setup">Smart Contracts</h4>
What makes blockchain so brilliant is that business transactions can be executed quickly, efficiently, and most importantly without the help of intermediaries. Smart contracts are programmed using chaincode in the various programming languages at the genesis of the chain, and cannot be altered. So, when you think of chaincode, you should pretty much be thinking ‘the code that implements the logic of a smart contract’. The goal of the smart contract is to
allow the performance of credible transactions without third parties. These transactions are trackable and irreversible [8].
The interesting part of the contracts is that they can be ‘self-executing’ and ‘self-enforcing’ because of their source code. Furthermore, they reduce transaction costs and provide exceptional security since after they are programmed, they cannot be altered.


<br>

<center><img class = "pic" src="../../img/business.png" alt="Mountain View" >


<b>In a private blockchain, participants need to be authorized by a ‘Membership service provider’ to join the network.</b></center>


<br>

<h4 id="setup">Blockchain for Business</h4>
The main requirements for a business blockchain are simple. A shared ledger, smart contracts, privacy services, and trust. As security threats and hacks are becoming more commonplace, it is becoming more and more important to know who you are doing business with. This is part of why Hyperledger employs a ‘private’ blockchain, in which participants need to be authorized by a ‘Membership Service Provider’: not just anyone can join the network. Since each business network is different, a membership service provider may define its own rules to validate identity, based on the specific business use case [9]. This has very positive impacts for the business blockchain — most importantly the efficiency and speed of transactions. This concept of private vs. public blockchain is very important, and is one of the main differences between the Hyperledger blockchain and the cryptocurrency blockchains that are so popular right now.


<br>


<h4 id="setup">Conclusion</h4>
Let’s recap. What did you learn? At its core, the blockchain is a ledger that records transactions. The problem with the digital age is that keeping track of different businesses across a business network has become increasingly difficult. The blockchain solves this problem by creating one shared ledger that allows for secure transactions with a clear history of who owns what and at what time. There are different methods by which to determine the order of which transactions become part of the blockchain — these are called consensus algorithms. Along with privacy, consensus algorithms are one of the main ways blockchains differ from one another. And finally, smart contracts are business rules that are programmed into the chain. They allow certain transactions to become validated, while others will be rejected.

Phew! That was a lot. I congratulate you for getting this far. Hope you learned a thing or two, and please feel free to reach out to me in the comments below, on Twitter, or on LinkedIn. Happy Friday!

<h4 id="setup">Resources</h4>
<hr>

1) https://99bitcoins.com/who-accepts-bitcoins-payment-companies-stores-take-bitcoins/

2) https://en.wikipedia.org/wiki/Business_network

3) https://quickbooks.intuit.com/r/bookkeeping/whats-general-ledger-need-one/

4) https://en.wikipedia.org/wiki/Transaction

5) https://en.wikipedia.org/wiki/History_of_accounting

6) https://developer.ibm.com/courses/all/blockchain-essentials/

7) https://coinsutra.com/smart-contracts/

8) https://en.wikipedia.org/wiki/Smart_contract

9) https://www.hyperledger.org/wp-content/uploads/2017/08/Hyperledger_Arch_WG_Paper_1_Consensus.pdf
