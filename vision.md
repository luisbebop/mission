# What is hypernet?
Hypernet is:

- a p2p network
- - an annonymity layer
- - a public key cyrpto layer
- - a messaging layer
- a p2p filesystem
- - a pub/sub system
- - a version control system
- - a homomorphic crypto layer
- - an indexable database
- - a type system allowing applications to share data
- a p2p computing enviornment
- - a sandbox
- - a system idle monitor
- - a compute farbic that forges emergant reliability from an inherently unreliable substrate

# What is the point?
Hypernet is a replacement for the internet.  The internet today looks a lot like a set of dumb terminals (browsers) connected to mainframes (data centers).  While a centralized hub-and-spoke architecture might seem like nothing more than an uninteresting implementation detail, it's actually a detail that carries serious side effects.  Those side effects can be mitigated using a distributed architecture instead.

## Privacy
###### CENTRALIZED
A server is by definition a man-in-the-middle attack.  So long as your traffic eventually hits a server, anonymity is just not possible.  Using something like TOR can't help you mask your identity or the identitiy of the recipient if you're sending someone an email.

###### DISTRIBUTED
Because there are no servers a p2p network can statitically garauntee your privacy no matter who's wiretapped what.  There are still gotchas and pitfalls but at least privacy is actually possible.


## Security
###### CENTRALIZED
For transmitting data, the internet has more crypto patchwork than a new england quilting convention.  Worse, once data arrives on a server it's hardly ever encrypted because the premise of internet security today is that there is an inside and an outside.  Once inside -- and attackers always find a way to get in -- everyone's data is typically there for the taking.  Keep in mind that an "attacker" maybe the company itself (selling your private data to the highest bidder) or a government.

###### DISTRIBUTED
In a p2p system, anyone can inspect the data.  This means 2 things: 1) the data should be secured 2) the method with which that data is secured is verifiable by anyone.  There's not a whole lot of room for shennanigans (especially since the whole thing is open source).  More importantly, data that's sharded out across multiple nodes presents a more complicated attack surface.  Instead of offering attackers a single, high value target with a known public address, a p2p system stores random chunks of arbitrary data on random computers.  Comprimising a single node gives an attacker absolutely nothing and it's statistically imossible for an attacker to even discover what other nodes need to be compromised before a single document can be reconstructed... and that's assuming the attacker can decrypt the document.

## Control
###### CENTRALIZED
Companies control your data and many companies simply take ownership of your data.  Decide to migrate off Facebook onto some other social network?  Tough Noogies.  Don't like linkedin's latest UI update?  You best start liking it.  Want to make sure that thing you uploaded that you shouldn't have (you know the one I'm talking about)?  Good luck with that.

###### DISTRIBUTED
Users control their own data.  There is no way for an app developer to delete a user's data or deny them access to it.  Interestingly, a distributed system is harder for a single entity to control in other ways.  Ever notice that torrents come in faster than youtube?  There are a lot of reasons for this but one reason is that congestion along a single point in the network doesn't necessarily result in a loss of throughput.  It won't be so easy for comcast to throttle netflix... or for Turkey to ban twitter.  Looking into the future, what if the interent wasn't a bunch of copper and glass owned by companies?  We'll need better radios than whatever we're using for wifi and bluetooth but within cities it's easy to imagine computers talking to each other over an ad-hoc wireless mesh network.  We aren't actually going to leave the internet in the hands of ISPs are we?

## Cost
###### CENTRALIZED
It costs a lot of money to operate wikipedia.

###### DISTRIBUTED
What if end users donated their excess compute resources to power wikipedia instead?  We'd like to see an interent powered by the users for the users.

## Scale
###### CENTRALIZED
The asymetry of trying to serve a distributed audience using a centralized architecture is pretty obvious.  

###### DISTRIBUTED
Bittorrent scales... imgur doesn't.  But it's not just bandwidth.  Storage, and compute cycles can also scale proportionally with demand in a p2p network.

## Engineering
###### CENTRALIZED
If you haven't heard of the ~~eight~~ nine fallacies of distributed computing, you're gunna have a bad time.

###### DISTRIBUTED
All internet apps are already disributed -- they run on multiple machines in a data center but they're still written as if for a von Neumann machine.  With hypernet you can code for a **network**. 

# Are you a business?
Yes and we're currently selling ephemeral nodes at $1/node/month.  They're a lot like Amazon spot instance and they probably aren't very useful to most people but it's a starting point for us and if you need cheap spot instances, we can hook you up.

# What's the status of hypernet?
Parts of hypernet are exactly as advertised but most parts are completely fake.  A lot of functionality isn't powered by a p2p network at all.  Instead we cheat and use a centralized server.  The thing is, we have absolutely no idea what we're doing and our guess is niether does anyone else.  (Incidentally, if you know how to fix the internet and existing models of software development [we want to hear from you](mailto:info@hypernet.io).  In the mean time,
before we commit to implementing something crazy (like an entirely new functional programming language) we want to be sure that what we're building is actually useful.  The best way we know to do that is to mock it up using a disposable implementation and see what works and what doesn't.  So you'll just have to wait for the grand unveiling... or you could [jump in right away](http://github.com/hypernet).  We're open source and we welcome your contributions.
