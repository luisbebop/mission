# Hypernet Data
Hypernet data serves a number of different purposes.  It's a

- p2p persistence layer
- version control system
- database
- pub/sub system
- rights management system

What does HND actually *need* to do and why does it need to do those things?  Let's look at some examples.

## Example: Google Docs
### Persistence
> Users exect that data loss generally won't happen.  The one exception is when changes are made to a document during a network outage.  Users understand that those changes cannot be persisted without reconnecting.

Given the unreliable nature of the p2p compute fabric, a high level of replication is needed.  Any `fsync` equivelant or semantic should not return until a certian (perhaps user-specified?)level of replicaiton has been achieved.  To economize bandwidth and optimize throughput, multi peer transfers should be used.

### Permissions
> Users share content with arbitrary groups of users.  Different users hold different rights.  Some may:

> - read
> - write
> - delete
> - change the rights of other users (as well as add/remove users)

The challenge in a p2p environment is that there is no central authority that can grant, revoke and evaluate permissions.  There are several cryptographic alternatives.

1. Circulate a key to all members that have access to a document.  The downside is that for each version, new keys must be created and disseminated.  Especially for documents that are updated frequently, this is not a workable solution.
2. Use a permission "block".  The idea is to provide each rights holder with a read, write or admin key that is valid for as long as the rights set doesn't change.  The keys are encrypted once per member with the member's public key.

### Security
> Users who do not have permission to a certain document (or document version) should have no way of accessing that data.

The answer is encryption.

### Revisions
> The same "document" can be edited numerous times in rappid succession.

 We'll need binary diffs.  Larger documents cannot practically be uploaded, downloaded, or stored multiple times.  Storing previous revisions makes it possible to establish some degree of determinism in an otherwise highly non-deterministic system.

### Notifcations
> Users must have a way of recieving push notifcations for the latest revision.

Imagine the document is a google document... or the front page of reddit.  Applications must be informed when there is a new version.  Polling is not an accceptable solution.  We'll need a pub/sub system.  If the system leverages multi peer transfers it will (auto) scale gracefully.

### Conflicts
> Conflicts can occur whenever there is a bifurcation in the causal chain.  Slow networks, network partitions and other faults can result in multiple, conflicting edits.

While it is impossible to automatically resolve conflicts in a generalizable way, conflicts must be detected and the applicaiton or user should be able to decide how to resolve them without suffering arbitrary data loss.  Some policies can be fully automated, though.  In cases like Dropbox all revisions are saved but the last write becomes the head.

### Searchable metadata
> Users must be able to search for their documents.  The search criteria is app secpfic but can include mod dates, owners, and even full text search.  For example, when a user logs in they need to have some way of seeing their files.

Listing all documents belonging to a "domain" seems easy enough.  But what's a domain?  Filesystems use hierarchical namespaces (i.e. `/users/Peter/Desktop/theplan.md`) but what should the path components be in this case?

There may be another opportunity here.

## Example: Log aggregator
### Grep, Tail
The two most common operations typically associated with logs is grep and tail.

### Analysis
Logs also need to be analyzed for certain kinds of events.  Some form of local processing (or map reduce )are common use cases.

### Streaming
While local processing makes the most sense, local processing isn't always possible or desired.  In such cases, there should be a streaming download that allows data to be processed as it comes in.  This may be a duplicate of the tail requiremet.

## Example: Netflix
### Load balancing
> There is no way to know a priori just how much a given document will be requested if it is made available to a large audience.

The solution here seems to come from multi peered downloads (a la bittorrent) which autoscale with no further logic.

# What could actually be built with such a solution?

Well, it seems like pretty much everything.  Could you write a secure chat app?  Sure.  Just make the "document" available to the participants and grant all participants write access and watch them "edit" the document.  Could you write video sharing webite?  Sure, why not.  The videos are distributed using multi-peer downloads so they autoscale.  Public videos are stored without a permission block (which means they aren't encrypted) and the "front page" is just another document owned by the app but granting everyone read privelleges (again, the document would not be encrypted).
