# ansible-gitlab-ci-demo

## What?

Exemplar for individualised Ansible Roles based on the basic `ansible-galaxy init` template and [William Yeh's Ansible Docker image](https://github.com/William-Yeh/docker-ansible).


## Why?

To illustrate, and maybe provide a simple template for, easy Docker-based Ansible testing.

## How?

The `gitlab-ci.yml` file runs the tests in a Docker image, keeping things neat and tidy for us.

*NOTE:* This is meant to run with the [Docker executor](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/executors/README.md) but much of the same `gitlab-ci.yml` file should work for Kubernetes, VirtualBox, Parallels, and Docker Machine builds. Testing Ansible code by applying it is *not recommended* with the Shell and SSH executors as they would end up configuring the test box permanently with every test.

* `image: williamyeh/ansible:centos7` - This defines the Docker image each job will start with.
* `test: ...` - This sets the name of the job. It can be almost anything. There can be many of these and they can use their own Docker images. This allows a project to be tested against multiple distros or environments in one pipeline run.
* `script: ...` - The commands that follow this will be run inside the Docker container. Their PWD will start off in the repo's root. Each command is run in its own TTY so you can spread an `if` across multiple lines. For complex individual tasks, add scripts to the `test/` directory and call them from here.
