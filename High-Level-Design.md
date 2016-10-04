
> This proposal is a way to discuss, learn, and build tools for a better orchestration ecosystem.


### Core Development Principles

- Simple
  - We all agree, it is tough to expose simplicity
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
- Support Management
  - Otherwise known as supportability of a software
  - Does it strive to being fully automatic ?
  - This leads to features such as self-healing
- Life-Cycle Management
- Secrets Management
- Config Management
- Analytics Management
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
