### Reference/Key ingredients as we design the Control Plane

> The proportion of ingredients is important, but the final result is also a matter of how you put them together. Equilibrium is key. 
-- Alain Ducasse

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
