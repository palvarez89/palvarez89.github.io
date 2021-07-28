---
layout: cv
title: Curriculum
---

# Pedro Alvarez Piedehierro

<p style="text-align: right;">
    Manchester, UK<br>
    <strong>Email:</strong> <a href="mailto:pedro@alvarezpiedehierro.com">pedro@alvarezpiedehierro.com</a> <br>
    <strong>Phone:</strong> <a href="tel:+447508939171">+44 (0)750 8939 171</a> <br>
</p>


## Personal Statement

**Computer Science Engineer** with experience working with embedded devices and
Linux systems. Main areas of expertise include: build systems, system
integration (including building Linux systems from scratch), infrastrucutre,
open-source technologies and culture. Special interest on automation and
reproducibility, infrastructure as code, CI/CD, and contributing to open-source
projects. Team player, always willing to help, and to share knowledge.


## Other Relevant Experience

Things that I've done in my spare time, or even at work, but that aren't
related to a project:

- Actively participated in open-source communities when working on related
  projects.
- Maintained the Baserock project and also its infrastructure for years.
- Developed multiple automation scripts using Ansible for deploying and
  maintaining various pieces of infrastructure for the Baserock project,
  EtCaterva group and myself: Nginx, Apache, Django, Gerrit, Jenkins, OpenVPN,
  Docker...
- Helped to organise PyCon Spain 2017. Co-organised PyLondinium 2018 and 2019.
- Taken part on SoW writing and review, requirements gathering on site,
  estimates, and pre-sales calls.


## Employment History

### **Codethink** - Software and Systems Engineer & Tech Lead


###### 05/2020 – 07/2020
#### Remote-execution setup on OpenStack

Deploy a remote-execution solution on customer's infrastructure.
- Used Terraform to automate the deployment of instances on OpenStack
- Ansible scripts to setup all instances with the different BuildBarn services
- Updated configuration of projects to build on remote execution
- Zuul CI for automation


###### 06/2020 – 02/2021
#### Python services for internal development workflow

Developed set of microservices on customer's multi-environment
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

- Architected and initiated current implementation of the project.
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
- Upstreamed (via Gerrit)  some fixes needed in kolla/kolla-ansible to support
  ARM64 in their Docker templates and Ansible scripts.
- Created Ansible scripts to automatically debug all the VLANs from/to all the
  nodes.
- Researched ways to have isolated self-managed domains, to workaround current
  limitations in OpenStack.


###### 01/2017 - 12/2018
#### Application for configuring and working with ANC chips

Develop an application to help with the tuning and flashing of the ANC devices.

- Team and technical leader responsibilities.
- Created and maintained CI/CD pipelines in Jenkins, setting the best practices
  for all the teams.
- Architected and implemented an RPC to communicate Python with legacy software
  in Matlab.
- Developed Python libraries for flashing and loading code into the ANC
  development board.


### **Codethink** - Software and Systems Engineer

Involved in and developed a wide variety of projects

###### 08/2013 - 01/2017
#### Baserock

- Integrated and maintained software in a set of definitions of Linux systems.
  OpenStack, Systemd, linux kernel, graphics stack, etc.
- Troubleshoot integration problems from the application to kernel layer.
- Continuous investigation about new possible applications of Baserock.
- Created and maintained the core infrastructure of the project, using Ansible
  and OpenStack.
- Implemented and improved existing tooling to support atomic system upgrades.
- Added support and ported Baserock to new architectures (POWER, ARMv6, ARMv7)
- Interacted with various Open Source communities,
- …

#### GENIVI Baseline

- Integrated and maintained software following the GENIVI Baseline compliance.
- Involved on getting the GENIVI Development Platform (GDP) also integrated.
- Delivered a Hands-on session in the GENIVI AMM

#### Immut

- Investigation and use of Ostree repositories.
- Involved with Atomic community to work on new goals for tools like
  'rpm-ostree'.
- Used tools like Docker and Packer.

#### Software dependency visualizer

- Research about different ways of visualizing the data.
- Development of a prototype using JavaScript, and TypeScript.
- Use of JS libraries like d3.js to construct the user interface.


## Education

###### 09/2007 - 09/2012
#### MSc Computer Science Engineering (2:1)

**Universidad de Extremadura**, Cáceres, Spain - **5 years degree** covering
many different areas, including Mathematics, Unix, Networking, Databases,
Software Analysis and Design, AI, Robotics.


## Programming Languages & Tools

* Python, Shell, Java
* Basic knowledge of C++, Rust and some others.
* Ansible, Docker, Kubernetes, Terraform.
* Git, Gerrit/GitHub/GitLab, Jenkins, Travis, GitLab CI, GitHub actions, Zuul CI.
* OpenStack, AWS.
* Linux, systemd.


## Links Of Interest

- **GitHub:** <https://github.com/palvarez89>
- **GitLab:** <https://gitlab.com/palvarez89>
- **Open Hub:** <https://www.openhub.net/accounts/palvarez89>


## Languages

- **Spanish:** Native.
- **English:** Professional.
