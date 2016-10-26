
> This proposal is a way to discuss, learn, and build tools for a better orchestration ecosystem.


### Core Development Principles

- Simple
  - We all agree, it is tough to build simple products
    - Documentation / Literate programming
    - Code Clarity
    - Code Consistency
      - Follow guidelines to achieve consistency
    - Community Review
    - Modularity / DRY Code
- Naming
  - Take time to pick names that are well understood
  - Names should match their intention
- Standard Orchestration Contracts
  - This leads to composable & pluggable components
- Tests
  - Unit Testing leading to 100% code coverage
  - *In a recent paper, it was found that <b> 88% of critical bugs </b> could have been discovered by unit tests*
- CD & CI
  - At any point of time, the code should be in a production grade i.e. releas-able format
  - Aim to eliminate manual involvement towards a release
    - In other words, it is impractical & error prone to release based on manual efforts
    - QA & release manager(s) should only supplement above process

<br />

### Modules / Components

- Fault Management
  - Automatic detection of faults, & tools to recover from inconsistent states
  - Real-time failover
- Self-Serving
- Self-Healing
  - Otherwise known as supportability of a software
  - Does it strive to being fully automatic ?
  - This leads to features such as self-healing
- Life-Cycle Management
- Secrets Management
- Config Management
- Monitoring
  - Containers are getting smaller & more numerous
  - Understanding their interdependencies to do the root cause analysis
  - Maintaining operational health at scale
  - Monitoring systems need to be more available & scalable than the systems being monitored
  - Monitoring on an orchestration layer imposes fair amount of complexity
    - understand the semantic context imposed on the containers by the orchestration system
    - containers are being served from schedulers across a variety of underlying nodes
  - Differentiate between data & information
    - Metrics need to be provided with context to aid interpretation
- Policy Change Management
  - Monitor policy changes
  - Alert on invalid configurations
  - Track down potential problems

<br />

### Entities

- Resource
- Process

<br />

### References

- refer [Zeppelin Framework Proposal & Development Roadmap](https://medium.com/zeppelin-blog/zeppelin-framework-proposal-and-development-roadmap-fdfa9a3a32ab#.49wfkeyey)
- refer [Cattle Concepts](http://docs.cattle.io/en/latest/concepts/orchestration.html#resources)
- refer [OpenZeppelin Style Guide](https://github.com/OpenZeppelin/zeppelin-solidity/blob/master/CONTRIBUTING.md#style-guidelines)
- refer [InfoQ on Containers](http://www.infoq.com/resource/minibooks/emag-container-technology/en/pdf/Exploring-Container-Technology-in-the-Real-World-eMag.pdf)
- refer [Build Technical Wealth](http://firstround.com/review/forget-technical-debt-heres-how-to-build-technical-wealth/?mc_cid=07889699da&mc_eid=9a1ca6920c)
