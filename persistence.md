# Hypernet Data
Processes are inherently ephemeral by nature, whether running on a PC, on a server in a data center or on a p2p node.  Persistent storage is what allows applications' state to outlive the process.  Recreating reliable persistence on a profoundly unreliable substrate is one of the problems Hypernet Data must solve.  It must do so in a way that makes the network as transparent to the user as possible.  So what is Hypernet Data? It's a:

- p2p persistence layer
- version control system
- database
- pub/sub system
- rights management system

But *why* does Hypernet Data actually need to do these exact things?  Let's look at some examples.

## Example: Google Docs
### Persistence
> Users expect that data loss generally won't happen.  The one exception is when changes are made to a document during a network outage.  Users understand that those changes cannot be persisted without reconnecting.

Given the unreliable nature of the p2p compute fabric, a high level of replication is needed.  Any `fsync` equivalent or semantic should not return until a certain (perhaps user-specified?) level of replication has been achieved.  To economize bandwidth and optimize throughput, multi peer transfers should be used.

### Permissions
> Users share content with arbitrary groups of users.  Different users hold different rights.  Some may:

> - read
> - write
> - change the rights of other users (as well as add/remove users)

The challenge in a p2p environment is that there is no central authority that can grant, revoke and evaluate permissions.  There are at least two cryptographic alternatives.

1. Circulate a key to all members that have access to a document.  The downside is that for each version, new keys must be created and disseminated or it's not possible to ever revoke access to a document.  Especially for documents that are updated frequently, this is not a workable solution since both generating and exchanging keys is costly.
2. Use a "permission block".  The idea is to provide each rights holder with a read, write or admin key that is valid for as long as the rights set doesn't change.  The keys are encrypted once per member with the member's public key.

### Security
> Users who do not have permission to a certain document (or document version) should have no way of accessing that data.

Encryption.

### Revisions
> The same "document" can be edited numerous times in rapid succession.

We'll need binary diffs.  Larger documents cannot practically be uploaded, downloaded, or stored multiple times.  Also, storing previous revisions makes it possible to establish some degree of determinism in an otherwise highly non-deterministic system.

### Notifications
> Users must have a way of receiving push notifications for the latest revision.

Imagine the document is a google document... or the front page of reddit.  Applications must be informed when there is a new version.  Polling is not an acceptable solution.  We'll need a pub/sub system.  If the system leverages multi peer transfers it will (auto) scale gracefully.

### Conflicts
> Conflicts can occur whenever there is a bifurcation in the causal chain.  Slow networks, network partitions and other faults can result in multiple, conflicting edits.

While it is impossible to automatically resolve conflicts in a generalizable way, conflicts must be detected and the application or user should be able to decide how to resolve them without suffering arbitrary data loss.  Some policies can be fully automated, though.  For example, all revisions can be saved but the last write becomes the head.

### Search-able metadata
> Users must be able to search for their documents.  The search criteria is app specific but can include mod dates, owners, and even full text search.  For example, when a user logs in they need to have some way of seeing their files.

Listing all documents in a path seems easy enough.  But what's a path?  Filesystems use hierarchical namespaces (i.e. `/users/Peter/Desktop/theplan.md`) but what should the path components be in a p2p filesystem that is used by applications and not users?  We could use a scheme like `/user/application/data-class/data-instance` but that approach limits the opportunity for multiple apps to easily exchange data.  iOS is a "good" example of the shortcomings of such an approach.

Currently, apps tend to use custom and opaque methods for storing their data.  If you don't like iTunes it's not trivial to switch to another player and keep all playlists, play counts and everything else.  Don't like Facebook?  Too bad.  There is absolutely no way you can realistically migrate *your* social network to another app.  In some cases you can import contacts but unless all your friends join you in the new social network... you're stuck.  This is far from ideal.  The ultimate problem here is that **data, logic and UI** are often conflated, and rolled into one giant opaque code base... sometimes as a result of poor design and sometimes on purpose to protect companies' interests at the expense of the users.

But how can multiple applications handle data from unknown sources?  MIME types seem to do some of that but they merely define types and not the kinds of schemas that most apps use.  However, if data schemas used "canonical" types and their indices were exposed and standardized then you could just as easily use iBooks as you can Kindle... depending on which reader you prefer.  *Your* library would be accessible to both reader apps.

Hypernet Data strongly "encourages" apps to make their data available to their users; without vending something like a DTD, apps would have no real way of querying for their own data because the data doesn't live in a application defined directory.

## Example: Log aggregator
### Streaming
> While local processing makes the most sense, local processing isn't always possible or desired.

In such cases, there should be a streaming download that allows data to be processed as it comes in.

### Grep, Tail
> The two most common operations typically associated with logs is grep and tail.

Tailing a large number of logs simultaneously in real time probably isn't possible because of bandwidth constraints but what about tailing a grep?  However, if the data is encrypted something like grep can't work.  In such cases, some form of **homomorphic cryptography** must be made available.  Additionally, perhaps some form of map reduce may be a common use case.

> The only complication here is that it is better to perform the mapping where the data is stored.

## Example: Netflix
### Load balancing
> There is no way to know a priori just how much a given document will be requested if it is made available to a large audience.

The solution here seems to come from multi peered downloads (a la bittorrent) which autoscales with no further logic.

# What could actually be built with such a solution?
Pretty much anything.  Could you write a secure chat app?  Sure.  Just make the "document" available to the participants and grant all participants write access and watch them "edit" the document.  Could you write a video sharing web site?  Why not.  The videos are distributed using multi-peer downloads so they autoscale.  Public videos are stored unencrypted and the "front page" is just another document owned by the app but granting everyone read privileges (again, the document would not be encrypted).  Surely something like Reddit couldn't be built since there are too many people editing at the same time, right?  Wrong.  Reddit has that "problem" today and it works just fine.  One reason threads on Reddit are hierarchical (whether the creators know it or not) is to allow for causal bifurcations in the thread.  Remember, as revolutionary as the spirit of this project might be, technologically the revolution happened when single apps started running on multiple machines.  We just make running distributed apps outside a data center easier.
