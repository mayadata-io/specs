## Using etcd cluster for VSMs

Earlier we played with creation of a etcd cluster. Now its time to use the same.
I shall try playing with registrator project. 

> NOTE: The details mentioned here are applicable to current date & time. 
If there are any changes to this doc, there will be /should be separate specs 
file detailing the design decisions, etc.

### What is Registrator ?

- Refer - [registrator](https://github.com/gliderlabs/registrator/)
- Registrator project registers the docker containers.
- It does so without the knowledge of containers.
- It does so by using docker events.
- It can push (i.e. persist) the data to etcd
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

- a linux host + docker == openebs host
- etcd runs on openebs host
- Registrator 

### What if Registrator is not useful for openebs ?

- There are 2 things in Registrator: listen to docker events & persist to etcd.
- We may use Registrator's pluggable backends e.g. etcd.

### Similar projects that are based on Docker events ?

- https://github.com/gliderlabs/logspout

### Appendix

- What is a VSM ?
  - It is Virtual Storage Machine.
  - It is not a VM on any hypervisor.
  - It is a container.
  - It is a docker container specifically.
  - It is a docker container running a iscsi service.
