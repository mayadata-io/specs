### List of various use-cases / patterns / tools w.r.t Control-Plane

Most of these are curated from various references. We shall put our own patterns 
and use-cases once we build/re-use/derive an approach for Control-Plane. The
references are mentioned explicitly at 
[link](https://github.com/openebs/Control-Plane/blob/master/Reference-Articles.md)

> Most of these present a **slice** of what an orchestration platform should aim for.

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

<br />

#### Why Twitter decided to move from Apache Storm to Heron ?

> At Twitter, Apache Storm at our current scale was becoming increasingly challenging due to
issues related to scalability, debug-ability, manageability, and efficient sharing of cluster 
resources with other data services.

refer [link](https://www.infoq.com/news/2016/09/twitter-opensources-heron)

<br />

#### Can you make it simple ?

> **Simplified orchestration:** In an attempt to provide more reliable orchestration people often 
propose or gravitate towards complex workflow engines. Stampede tries to find an elegant balance 
between complex workflows and naive sequential programming. Stampede is heavily focused on the 
concept of managing state transitions and attaching logic to those transitions.

refer [link](https://github.com/cattleio/stampede#concepts)

<br />

#### Consul & Containers

> Build images of applications and services that do not contain any configuration. They
instead point themselves to Consul. In other words, when a new container is brought up, the
container's Consul agent is started which regusters the container's service at Consul. Hence,
the container service is dynamically available to the whole cluster.

> The container does not have any config but only service specific code.

![Consul & Docker](http://www.pythian.com/blog/wp-content/uploads/Consul-Demo-Architecture.png)

<br />

#### Autopilot Pattern (*term coined by Triton / Joyent*)

> An approach to application and infrastructure design that pushes automation for each component 
of our systems into the application. Each container that makes up the application has its own 
lifecycle, and we package those lifecycle behaviors into the application container rather than 
relying on external infrastructure.

<br />

#### MySQL on Autopilot

##### Service Discovery & Topology Queries

- How does the replica know where to find the primary ?
- How does the primary tell the replicas where to start replication ?
- How does the client know where to find nodes & which node accept writes ?

##### Post Deployment Queries

- How do we do backups ?
- How do we promote a replica if the primary fails ?
- How do the other replicas know where to find a new primary during failover ?
- How does the client know that we failed over ?

> [Container Pilot](https://www.joyent.com/containerpilot) will be included in MySQL containers.
This will orchestrate the bootstrap behavior, **coordinate** replication via Consul. A separate
logic will be invoked by Container Pilot to do the heavy lifting orchestration work. Details 
available at this [link](https://www.joyent.com/blog/dbaas-simplicity-no-lock-in)

![Architecture Diagram](https://www.joyent.com/content/blog/20160222-dbaas-simplicity-no-lock-in/architecture.png)
