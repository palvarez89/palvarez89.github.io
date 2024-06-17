---
layout: cv
title: Curriculum
---

# Pedro Alvarez Piedehierro

<p style="text-align: right;">
    Manchester, UK<br>
    <strong>Email:</strong> <a href="mailto:pedro@alvarezpiedehierro.com">pedro@alvarezpiedehierro.com</a> <br>
</p>


## Personal Statement

**Computer Science Engineer** with experience working with embedded devices and
Linux systems. Main areas of expertise include: build systems, system
integration (including building Linux systems from scratch), infrastructure,
open-source technologies and culture. Special interest in automation and
reproducibility, infrastructure as code, CI/CD, and contributing to open-source
projects. Team player, always willing to help, and to share knowledge.

## Programming Languages & Tools

* Python, Shell, Go
* Basic knowledge of C++, Rust and some others.
* Ansible, Docker, Kubernetes, Terraform.
* Git, Gerrit/GitHub/GitLab, Jenkins, Travis, GitLab CI, GitHub actions, Zuul CI.
* OpenStack, AWS, OpenNebula
* Linux, systemd.


## Employment History

### **SoftIron** - Senior Systems Engineer 11/2021 - Current

- Supoported and improved deployment tooling for our Ceph-based solution.
- Integrate our solution with other solutions to create partnerships.
- Networking switches configuration (Ubiquiti and SONiC).
- Deployment experience on Datacentres.
- Lead Open Sourcing internal benchmarking tooling.
- Worked on initial integraions and automations on the cloud product
- Created Public IaC examples and recorded videos to support the examples.
- Helped develop a Kubernetes CSI driver for the cloud.
- Automated sanity and end-to-end tests for the CSI
- Set up an internal ArgoCD setup with multiple environments.
- Implemented a Rancher node driver for our cloud product.
- Created multiple Appliances for our marketplace integrating multiple
  solutions (ownCloud, TrueNAS, Rancher, FilterBox...) using Libguestfs
  and Packer.
- Worked on adding support to more type of Appliances on the Marketplace.
- Integrated a Kuberneted-based AI solution, using NVIDIA GPUs.

### **Codethink** - Senior Software and Systems Engineer & Tech Lead

###### 03/2021 – 08/2021
#### Remote-execution setup on OpenStack

Deploy a remote-execution solution on customer's infrastructure.
- Used Terraform to automate the deployment of instances on OpenStack
- Ansible scripts to setup all instances with the different BuildBarn services
- Updated configuration of projects to build on remote execution
- Zuul CI for automation


###### 06/2020 – 02/2021
#### Python services for internal development workflow

Develop a set of microservices on customer's multi-environment
architecture to develop a PR-like workflow for patches to SVN.
- Integrated with Kafka messaging queues from external services
  to track validation progress
- Microservices running on a multi-environment architecture
- Collaboration with multiple customer teams to get our solution
  integrated.

###### 02/2020 – 05/2020
#### SVN split to Git automatic migration

Automation of a previously manual process for migrating libraries
from a mono-repo in SVN to individual git projects.

- Developed scripts and libraries in python to handle the automatic
  migration of hundreds of libraries from SVN to Git.
- Used Jenkins pipelines for the automation process, triggered via
  GitHub PRs

###### 11/2019 – 01/2020
#### TroveKube, Git mirroring service on Kubernetes

Initial effort to migrate Baserock Trove (<https://git.baserock.org>) from a
monolithic server to a microservices architecture.

- Migrated Baserock's monolithic mirroring service to python3
- Created containers for each of the services in Docker, and a PoC using
  docker-compose.
- Adapted the solution to run on Kubernetes running locally (minikube)
- Developed a Helm chart, to deploy easily the service, including EFS and SSL
  support.
- Used Terraform for AWS deployments of ELK and EFS.


###### 07/2019 - 11/2019
#### Autonomous driving demo for ELCE

Robots (NVIDIA Jetson Nano boards with wheels and a camera) that use AI to
follow a road, and stop when necessary.

- Built a Linux system from scratch for the NVIDIA Jetson Nano, using
  Freedesktop SDK and BuildStream.
- Implemented OTA upgrades for the rootfs and kernel using OSTree.


###### 04/2019 - 07/2019
#### Remote Execution API Test Suite

To provide a continuous way of testing the compatibility between different
Remote Execution clients (Bazel, RECC, BuildStream) and servers (Buildbarn,
Buildfarm, BuildGrid).

- Architected and started initial implementation of the project.
- Created a test suite to check API stability of Bazel remote execution,
  against the 3 most used Remote Execution implementations.
- Used Amazon EKS with Terraform to run the services and tests on
  Kubernetes from Gitlab CI.


###### 01/2019 - 04/2019
#### OpenStack on ARM64 servers

Deploy and maintain an ARM64 OpenStack cloud to validate the architecture
is supported, and to fix any problems found. The main goal is to add ARM64
as a target on OpenStack CI.

- Automated deployments of OpenStack and Ceph to ARM64 machines hosted in
  packet.net.
- Upstreamed (via Gerrit) some fixes needed in kolla/kolla-ansible to support
  ARM64 in their Docker templates and Ansible scripts.
- Created extra Ansible scripts to help with the deployment automation and
  debugging.
- Researched ways to have isolated self-managed domains, to workaround current
  limitations in OpenStack.


###### 01/2017 - 12/2018
#### Application for configuring and working with ANC chips

Develop an application to help with the tuning and flashing of ANC devices.

- Created and maintained CI/CD pipelines in Jenkins, setting the best practices
  for all the teams.
- Architected and implemented an RPC server to communicate Python with legacy
  software in Matlab.
- Developed Python libraries for flashing and loading code into the ANC
  development board, and to emulate the process for testing purposes.


### **Codethink** - Software and Systems Engineer

Involved in and developed a wide variety of projects

###### 08/2013 - 01/2017
#### Baserock and others

- Integrated and maintained software in a set of definitions of Linux systems.
  OpenStack, Systemd, linux kernel, graphics stack, etc.
- Troubleshoot integration problems from the application to kernel layer.
- Continuous investigation about new possible applications of Baserock.
- Created and maintained the core infrastructure of the project, using Ansible
  and OpenStack.
- Implemented and improved existing tooling to support atomic system upgrades.
- Added support and ported Baserock to new architectures (POWER, ARMv6, ARMv7)
- Interacted with various Open Source communities,


## Education

###### 09/2007 - 09/2012
#### MSc Computer Science Engineering (2:1)

**Universidad de Extremadura**, Cáceres, Spain - **5 years degree** covering
many different areas, including Mathematics, Unix, Networking, Databases,
Software Analysis and Design, AI, Robotics.


## Links Of Interest

- **GitHub:** <https://github.com/palvarez89>
- **GitLab:** <https://gitlab.com/palvarez89>
- **Open Hub:** <https://www.openhub.net/accounts/palvarez89>
