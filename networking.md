# Hypernet Networking
Traditionally, internet applications run on a well known, pre-defined set of servers with a fixed set of (public) IPs.  Moreover, those machines are expected to have a high uptime.  Applications running on a p2p network are in a different position.  The set of machines they run on change with relatively high frequency at (relatively) unpredictable times.  Additionally, those machines often run behind NATs or firewalls.  Consequently, there could easily be multiple machines behind a single IP.  Moreover, the machines are not even remotely administered in any coordinated fashion.  They could be running any other kind of software, using arbitrary ports.  Lastly, to the extent that a centralized authority can be trusted, arbitrary end users most definitely cannot be.  Hypernet Networking addresses all these challenges.  It also provides a "legacy bridge" that allows interoperation between the old internet and Hypernet.  So what is Hypernet Networking?  It's a:

- NAT / firewall hole puncher / relay
- p2p networking
- DHT
- anonymous routing
- a p2p DNS replacement

## NAT Traversal
This is a well understood topic but because Hypernet runs a visor that runs other apps, there is an additional bit of functionality that must be supported.  Apps not only need to open their own ports but they have to have a way to advertise which services they vend on what ports.

## p2p
The p2p networking layer is responsible for mapping between (hashes of) cryptographic keys and IP addresses/ports.  At the moment, Hypernet uses a Kademlia-style routing scheme.

## DHT
The DHT is a simple key value store.  In addition to get, put and remove operations, it is responsible for self-healing replication.  It implements a minimal amount of security that ensures only the owner can remove a value but it otherwise makes no other checks of any kind.  The DHT is an implementation detail and is not exposed directly to users or applications of Hypernet.

## Anonymity
Anonymity serves two purposes.  1) Some transactions are sensitive by nature, such as personal correspondences, or banking 2) While security through obscurity is generally a derisive term, "obscurity" in this case can hide the origin of an encrypted data shard.  An attacker attempting to decrypt data would have no identifiable target and would ultimately be stuck decrypting pretty much everything in hopes of finding something of interest.  The result is a **provider-independent** security solution that is considerably more secure than traditional centralized architectures.

## p2p DNS
The p2p "DNS" is not so much for end users as it for app instances need to discover other app instances.  Consequently, the question of "trusting" the results from the "DNS" is not quite the same as truesting a traditional DNS server to return the "right" IP.  Visors return a hash of the app together with IP/port mappings.  A malicious visor can lie about this hash which means in practice an attacker can usurp (probably encrypted) data.  In extreme cases, an attacker could hijack more than half the nodes in which case the default concensus scheme would be effectively subverted giving an attacker the opportunity to alter the result of a computation.
