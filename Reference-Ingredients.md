### Reference/Key ingredients as we design the Control Plane

> The proportion of ingredients is important, but the final result is also a matter of how you put them together. Equilibrium is key. 
-- Alain Ducasse

This presents some of the key features of the key ingredients that will make the Control-Plane. 
Most of these are curated from various references. We shall put original metrics & view points 
on the ingredients that are selected to be parts of Control-Plane.

<br />

#### Raft consensus algorithm

- It mandates what happens in split-brain scenario.
  - Neither side will be able to elect a leader
  - Writes are halt
  - Electing a leader requires a quorum

<br />

#### Serf

- It is an AP system. It trades **consistency** for availability.
  - Even when 90% of your instances are down, the Serf cluster will operate
- Can be used for (*a limited number of usecases has been mentioned*):
  - memcache pool
  - load balancers
  - peer to peer VPN topologies

<br />

#### Consul

- It is a CP system. It trades **availability** for consistency.
  - It is limited to tolerate failures.
  - However, this is not bad as long as the applications' requirements are met.

<br />

#### etcd

