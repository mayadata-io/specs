## Analyzing ContainerPilot implementation(s)

### MySQL Autopilot Implementation [WIP]

- More on Autopilot pattern can be found [here](http://autopilotpattern.io/)
- The key enabler that implements *autopilot pattern* for MySQL is **ContainerPilot**
  - More on ContainerPilot can found [here](https://www.joyent.com/containerpilot)
- source code [link](https://github.com/autopilotpattern/mysql)

#### Contents of Dockerfile

- The base image is ```FROM percona:5.6```
- The image is kept small & hence a lot of dependencies are mentioned here
  - low level till high level dependencies are mentioned here  
- MySQL-Autopilot scripts are put at /usr/bin/local
- Finally the containerpilot command is exposed as a CMD

#### Contents of docker-compose.yml

- This includes two services
  - mysql & consul
  - these are not linked
  - mysql service refers to a containerpilot.json ??
  - consul service refers to a containerpilot command ??
- linking of these two services is done in a separate file called local-compose.yml
  - this file extends from docker-compose.yml

#### Contents of makefile

- building, tagging & shipping to docker hub
- a test-runner target that is a docker build of tests/Dockerfile
- *this is where the makefile gets **complex***:
  - coupling with manta
  - coupling with triton
  - defining & triggering tests on various deployments
  - it seems to have catered to functional tests from this makefile
