### Reference/Key ingredients as we design the Control Plane

> The proportion of ingredients is important, but the final result is also a matter of how 
you put them together. Equilibrium is key. 
-- Alain Ducasse

This presents some of the key features of the key ingredients that will make the Control-Plane. 
Most of these are curated from various references. We shall put original metrics & view points 
on the ingredients that are selected to be parts of Control-Plane. The references are mentioned
explicitly at [link](https://github.com/openebs/Control-Plane/blob/master/Reference-Articles.md)

<br />

#### `Raft consensus algorithm`

- It mandates what happens in split-brain scenario.
  - Neither side will be able to elect a leader
  - Writes are halt
  - Electing a leader requires a quorum

<br />

#### `Serf`

- It is an AP system. It trades **consistency** for availability.
  - Even when 90% of your instances are down, the Serf cluster will operate
- Can be used for (*a limited number of usecases has been mentioned*):
  - memcache pool
  - load balancers
  - peer to peer VPN topologies
- Operates at a node level abstration

<br />

#### `Consul`

- It is a CP system. It trades **availability** for consistency.
  - It is limited to tolerate failures.
  - However, this is not bad as long as the applications' requirements are met.
- It maintains a logical topology of your network without you doing much
  - It does it by using a gossip based protocol (*a derivative of paxos called Raft*)
- The database they have chosen in LMDB (*due to its light weight nature*)
  - An embedded database that avoids context switch out of the process
  - Hence is able to serve requests with lower latency & higher throughput
 - If you combine above statements it becomes, *a consistent key value store based on Raft*
- Operates at a service level abstraction
  - Serf is used in Consul to power the discovery of other nodes

<br />

#### `etcd`


<br />

#### `Terraform`

- Build, Modify & Version infrastructure with ease
- Generates an execution plan that describes the steps to reach the desired infra
- Create incremental execution plans which can be applied
- Manage a single application or an entire datacenter

<br />

#### `Kubernetes`

- Scheduling is policy-rich, topology-aware, workload-specific function
- Aspires to be an extensible, pluggable, building-block OSS platform & toolkit
- Enables higher-level PaaS functions without modification to core
