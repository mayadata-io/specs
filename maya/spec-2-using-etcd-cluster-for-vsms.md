# The Problem

> Frame the problem that you trying to solve. More importantly, explain why it is worth addressing. 
Be specific, and provide metrics.

- Earlier we played with creation of a etcd cluster. 
- Now its time to use the etcd cluster.
  - i.e. Ability to make use of etcd cluster for persisting configuration data

> NOTE: **The details mentioned here are applicable to when this spec was introduced. 
If there are any changes to the overal plan (*which obviously will*), there should be
separate specs file detailing the modified design decisions, etc.**

# Measurable Goals

> Promise clear deliverables and outcomes. Identify what’s out of scope. Make sure it’s easy to look
at each goal and answer: did we hit it?

- Setup & Tear down a clustered maya deployment.
- This will provide necessary ideas to using etcd cluster for openebs' VSMs (Virtual Storage Machines).

# Context

> Provide evidence that your audience needs to understand the problem and believe in your proposal.
Assumptions, use-cases, metrics, etc.

I shall try playing with registrator project. 

### What is Registrator ?

- Refer - [registrator](https://github.com/gliderlabs/registrator/)
- Registrator project registers the docker containers.
- It does so without the knowledge of containers.
- It does so by using docker events.
- It can push (i.e. persist) the data to etcd.
- The backend (i.e. etcd) is pluggable (i.e. consul can also be used)

### Why should openebs use Registrator ?

> It depends on how much openebs can leverage w.r.t Docker events.

Docker events can be of below type:

- docker container specific
- docker image specific
- docker plugin specific
- docker volume specific
- docker network specific
- docker daemon specific

Currently, all of the above seems good to be leveraged by openebs.

### Should we use Registrator as-is ? 

- i.e run Registrator containers on every openebs nodes (a linux host that uses docker)

or Q2 - Should we use Registrator code inside Maya & produce a single Maya binary ?

- Not sure. We shall evaluate the pros & cons

### Dependencies of Registrator ?

- github.com/fsouza/go-dockerclient

> Above library has very active community. It may be used otherise in maya as well.

### Deployment Strategy

- A linux host + docker == openebs host
- etcd runs on openebs host
- Registrator will run as-is in a docker container

# Final Solution

> Your proposal should be detailed enough for your team to consume and execute. Provide the 
code link and install / demo steps.


# Timeline

> List dates and milestones that your team believes in. This section may start off vague, but should 
be finalized in your last spec review.

- To be completed by 4th Nov 2016

# Possible Questions

### What if Registrator is not useful for openebs ?

- There are 2 things in Registrator: listen to docker events & persist to etcd.
- We may use Registrator's pluggable backends e.g. etcd.

### Similar projects that are based on Docker events ?

- https://github.com/gliderlabs/logspout

### What is a VSM ?

- It is Virtual Storage Machine.
- It is not a VM on any hypervisor.
- It is a container.
- It is a docker container specifically.
- It is a docker container running a iscsi service.

### What is an openebs host ?

- It is a linux host with docker running.
- There will be other components as well, but lets begin with above knowledge for the time being.
