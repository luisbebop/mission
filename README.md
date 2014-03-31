# What is Hypernet?
Hypernet is a compute fabric that forges emergent reliability from an inherently unreliable substrate.  It consists of:

- a p2p network
	- an anonymity layer
	- a public key crypto layer
	- a messaging layer
- a p2p filesystem
	- a pub/sub system
	- a version control system
	- a homomorphic crypto layer
	- an indexable database
	- a type system allowing applications to share data
- a p2p computing environment
	- a sand box
	- a system monitor
	- a method for remote code execution

# What is the point?
Hypernet is a replacement for the internet.  The internet today looks a lot like a set of dumb terminals (browsers) connected to mainframes (data centers).  While a centralized hub-and-spoke architecture might seem like nothing more than an uninteresting implementation detail, it's actually a detail that carries serious side effects.  Those side effects can be mitigated using a distributed architecture instead, which is exactly what Hypernet offers.

## Privacy
###### CENTRALIZED
A server is by definition a man-in-the-middle attack.  So long as your traffic eventually hits a server, anonymity is just not possible.  Using something like TOR can't help you mask your identity or the identity of the recipient if you're sending someone an email.

###### DISTRIBUTED
Because there are no servers a p2p network can statistically guarantee your privacy no matter who's wire-tapped what.  There are still gotchas and pitfalls but at least privacy is actually possible.

## Security
###### CENTRALIZED
For transmitting data, the internet has more crypto patchwork than a new england quilting convention.  Worse, once data arrives on a server it's hardly ever encrypted because the premise of internet security today is that there is an "inside" and an "outside".  Once inside -- and attackers always find a way to get in -- everyone's data is typically there for the taking.  Keep in mind that an "attacker" may be the company itself (selling your private data to the highest bidder) or a government.

###### DISTRIBUTED
In a p2p system, essentially anyone can inspect the data because it's stored on end users' nodes.  This means 2 things: 1) the data should be secured 2) the method with which that data is secured is verifiable by anyone.  There's not a whole lot of room for shenanigans (especially if the whole thing is open source).  More importantly, data that's sharded out across multiple nodes presents a more complicated attack surface.  Instead of offering attackers a single, high value target with a known public address, a p2p system can store random chunks of arbitrary data on random computers.  Compromising a single node gives an attacker absolutely nothing and it's statistically impossible for an attacker to even discover what other nodes need to be compromised before a single document can be reconstructed... and that's assuming the attacker can decrypt all the document shards.

## Control
###### CENTRALIZED
Companies control your data and many companies simply take ownership of your data.  Decide to migrate off Facebook onto some other social network?  Tough noogies.  Don't like linkedin's latest UI update?  You best start liking it.  Want to really delete that thing you uploaded that you shouldn't have (you know the one I'm talking about)?  Good luck with that.

###### DISTRIBUTED
If application data is stored in a way that only the user can control who has access to it then competing (or complimentary) apps can work with each other's data.  But wouldn't this be terrible for companies like LinkedIn and Facebook and lots of other companies, too?  You betcha.  We think a company's value should be measured in terms of the value it delivers to its users and not in terms of the switching cost it imposes on its users.  Interestingly, a distributed system is harder for a single entity to control in other ways as well.  Ever notice that torrents come in faster than youtube?  There are a lot of reasons for this but one reason is that congestion along a single point in the network doesn't necessarily result in a loss of throughput.  It won't be so easy for comcast to throttle netflix... or for Turkey to ban twitter.  Looking into the future, what if the internet wasn't a bunch of copper and glass owned by companies?  We'll need better radios than whatever we're using for wifi and bluetooth but within cities it's already easy to imagine computers talking to each other over an ad-hoc wireless mesh network.

## Cost
###### CENTRALIZED
It costs a lot of money to operate wikipedia.

###### DISTRIBUTED
What if end users donated their excess compute resources to power wikipedia instead?  We'd like to see an internet powered by the users for the users.

## Scale
###### CENTRALIZED
The asymmetry of trying to serve a distributed audience using a centralized architecture is pretty obvious.

###### DISTRIBUTED
Bittorrent scales... imgur doesn't.  But it's not just bandwidth.  Storage, and compute cycles can also scale proportionally with demand in a p2p network.

## Engineering
###### CENTRALIZED
Building apps, even for data centers is hard.  Many engineers still tend to ignore the ~~eight~~ nine fallacies of distributed computing despite most internet apps being run on a network of machines.

###### DISTRIBUTED
Hypernet let's us get a fresh start and code for a *network* instead of a *computer*.  In other words, stop coding for von Neumann machines and start coding for the internet.

# Business Model
We're currently selling ephemeral nodes at $1/node/month.  They're a lot like Amazon spot instance but they only let you run JARs.  They probably aren't very useful to most people but it's a starting point for us and if you need cheap spot instances that run JARs, we can hook you up.  Our business model is pretty simple.  In Hypernet there are **givers** and there are **takers**.  Givers are application developers or content publishers that drive adoption of Hypernet.  Takers are people who need computational resources but do not deliver value to end users of Hypernet.  We take the money we make from **takers** and we do a revshare with **givers**.  So, app developers and content publishers looking to make money, [drop us a line](mailto:info@hypernet.io).

# Funding
We're currently [raising money](https://angel.co/hypernet-1).

# What's the status of Hypernet?
Parts of Hypernet are exactly as advertised but most parts are completely fake.  A lot of functionality isn't powered by our p2p network yet.  Instead we cheat and use a centralized server.  The thing is, we have absolutely no idea what we're doing and our guess is neither does anyone else.  (Incidentally, if you know how to fix the internet and existing models of software development [we want to hear from you](mailto:info@hypernet.io).  In the mean time, before we commit to implementing something crazy (like an entirely new functional programming language) we want to be sure that what we're building is actually useful.  The best way we know to do that is to mock it up using a disposable implementation and see what works and what doesn't.  So you'll just have to wait for the grand unveiling... or you could [jump in right away](http://github.com/hypernet).  We're open source and we welcome your contributions.
