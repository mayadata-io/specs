
> This proposal is a way to discuss, learn, and build tools for a better orchestration ecosystem.


### Core Development Principles

- Simple
  - Below are fundamental to achive simplicity
    - Documentation / Literate programming
    - Code Clarity
    - Code Consistency
      - This leads to style guidelines
      - refer [OpenZeppelin Style Guide](https://github.com/OpenZeppelin/zeppelin-solidity/blob/master/CONTRIBUTING.md#style-guidelines)
    - Community Review
    - Modularity / DRY
- Naming
  - Take time to pick names that are well understood & match the intention
- Standard Orchestration Contracts
  - This leads to composable & pluggable components
- Tests
  - Unit Testing must result into 100% code coverage
  - *In a recent paper, it was found that 88% of critical bugs could have been discovered by unit tests*
- CD & CI
  - At any point of time, the code should be in a production grade releasable format
  - Aim to eliminate manual involvement towards release
    - QA & release manager(s) should only supplement above process

<br />

### Modules / Components

- Fault Tolerance
  - Automatic detection of faults, & tools to recover from inconsistent states
- Supportability
  - Leading to self healing
- Life-Cycle
- Secrets Management
- Config Management

<br />

### Entities

- Resource
- Process

<br />

### References

- refer [Zeppelin Framework Proposal & Development Roadmap](https://medium.com/zeppelin-blog/zeppelin-framework-proposal-and-development-roadmap-fdfa9a3a32ab#.49wfkeyey)
- refer [Cattle Concepts](http://docs.cattle.io/en/latest/concepts/orchestration.html#resources)
