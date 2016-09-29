### List of various use-cases w.r.t the Control-Plane ingredients

#### Consul & Containers

> Build images of applications and services that do not contain any configuration. They
instead point themselves to Consul. In other words, when a new container is brought up, the
container's Consul agent is started which regusters the container's service at Consul. Hence,
the container service is dynamically available to the whole cluster.

> The container does not have any config but only service specific code.
