### List of *Frequently Asked Questions* w.r.t Control-Plane

#### Will it be be good to have the service discovery tools run on Cassandra ?

- The problem statement is not about the datastore.
- It is more w.r.t high-availability & discovery (*of the registered services*).
- Tools like Consul maintain a logical topology of your network without you doing much.
- Cassandra can be a building block & can be augmented with features to be like Consul.
- But is Cassandra light weight ?

#### Why does distributed systems need a service discovery tooling ?

> Think of these scenarios: An app talking to multiple DBs, or multiple instance of an app
talking to multiple DBs. How does your app know about its dependencies? How does your app
learn about a failing dependency ? Do you intend to have a support to do these code/env/config
changes manually ? Will the application not miss its SLAs ?
