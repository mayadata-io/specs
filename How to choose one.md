### How do you choose your Control Plane ?

> You always have a choice !

- Is it simple to understand & contribute ?
- Is it lightweight i.e. made up of bare minimum pieces ?
- Does it have a loose coupling with its controlled entities (*read applications*) ?
- Is it agnostic to take care of any application's lifecycle behaviors ?
 - Some of these behaviors are: startup, shutdown, scaling, discovery, & recovery.
- Does it force to rely on an external infrastructure ?
- Does it have a scheduling piece ?
- Does it have a health checker functionality ?
  - This helps in abstracting self-healing features from an application.
- Does it have an reporting or metrics element ?
- Does it have an API for inquiry purposes ?
- Is it's scheduling piece pluggable ?
- Is the scheduling governed by policies ?
  - Are these policies declarative in nature ?
- Can it scale up & down its controlled entities ?
  - Does it do the right placement while scaling up ?
  - Does it choose the right entity while scaling down ?
- Does it perform at scale ?
  - Does it publicize its metrics w.r.t varying deployments & varying applications ?
  - *All in the spirit of openness*
- Can it be debugged at ease ?
- What type of system it is made of w.r.t CAP (Consistency, Availability, Partition) ?
