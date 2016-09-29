### List of various use-cases / patterns enabled via Control-Plane ingredients

Most of these are curated from various references. We shall put our own patterns 
and use-cases once we build/re-use/derive an approach for Control-Plane. The
references are mentioned explicitly at 
[link](https://github.com/openebs/Control-Plane/blob/master/Reference-Articles.md)

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

> [Container Pilot](https://www.joyent.com/containerpilot) will be included in MySQL containers.
This will orchestrate the bootstrap behavior, **coordinate** replication via Consul. A separate
logic will be invoked by Container Pilot to do the heavy lifting orchestration work. Details 
available at this [link](https://www.joyent.com/blog/dbaas-simplicity-no-lock-in)

![Architecture Diagram](https://www.joyent.com/content/blog/20160222-dbaas-simplicity-no-lock-in/architecture.png)
