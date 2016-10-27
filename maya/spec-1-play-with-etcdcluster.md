# The Problem

> Frame the problem that you trying to solve. More importantly, explain why it is worth addressing. 
Be specific, and provide metrics.

- Need for a data store for application specific configurations
- The data store should be highly available as it will form the backbone of the management plane
- We have decided to play with etcd

> NOTE: **The details mentioned here are applicable to when this spec was introduced. 
If there are any changes to the overal plan (*which obviously will*), there should be
separate specs file detailing the modified design decisions, etc.**

# Measurable Goals

> Promise clear deliverables and outcomes. Identify what’s out of scope. Make sure it’s easy to look
at each goal and answer: did we hit it?

- Setup & Tear down an etcd cluster with ease
- Verify if sample configurations are available when a etcd node/instance goes down

# Context

> Provide evidence that your audience needs to understand the problem and believe in your proposal.
Assumptions, use-cases, metrics, etc.

# Final Solution

> Your proposal should be detailed enough for your team to consume and execute. Provide the 
code link and install / demo steps.

# Timeline

> List dates and milestones that your team believes in. This section may start off vague, but should 
be finalized in your last spec review.

- To be completed by 27th Oct 2016
