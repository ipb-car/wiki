<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [How to setup any host machine to operate the ipb-car](#how-to-setup-any-host-machine-to-operate-the-ipb-car)
  - [Setting up the host machine for the very first time](#setting-up-the-host-machine-for-the-very-first-time)
    - [Install the operating system](#install-the-operating-system)
    - [Install Docker](#install-docker)
      - [Docker: Installation](#docker-installation)
      - [Docker: Post-installation](#docker-post-installation)
      - [Docker: Login to our private registry](#docker-login-to-our-private-registry)
      - [](#)
    - [Extras](#extras)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

**_NOTE: Last updated by Nacho on 21.04.2023_**

# How to setup any host machine to operate the ipb-car

In just a few simple steps, you can get a freshly installed Linux machine to build the ipb-car setup:

1. [Install Docker](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
2. [Config Docker](https://docs.docker.com/engine/install/linux-postinstall/)
3. log in to our docker private registry

```shell
docker login -u ipb_car -p zzxMDFwg6LyM3hW6TB4c gitlab.ipb.uni-bonn.de:4567
```

That's it! You are ready to [launch the system.](https://gitlab.ipb.uni-bonn.de/ipb-team/robots/ipb-car/docs/-/wikis/How-to%3ALaunch-the-system)

<details>
<summary>Click to expand a more detailed explanation</summary>

Nacho has drastically simplified the host machine setup through the usage of [Docker](https://gitlab.ipb.uni-bonn.de/ipb-team/robots/ipb-car/docker_images/-/merge_requests/26 "Finish polenta docker setup"). To keep this wiki entry short, we will not enter more details; the only thing to know is that you should **NOT** be using any `dotfiles`, `config_files`, or any other configuration system. All the host-machine configuration is located in the [docker image](https://gitlab.ipb.uni-bonn.de/ipb-team/robots/ipb-car/docker_images/-/tree/master/images/polenta) we use to launch the setup.

If the host machine is already setup, then you can already go to the [How to launch the system wiki](https://gitlab.ipb.uni-bonn.de/ipb-team/robots/ipb-car/docs/-/wikis/How-to%3ALaunch-the-system)

## Setting up the host machine for the very first time

If you are in the horrible situation of setting up the host machine for the first time, follow the instructions below. I logged all the manual steps after a fresh install using `PopOS 22.04`.

### Install the operating system

Just google how to do this; I picked PopOS 22.04 because it was the latest stable release the day I reinstalled the OS on Polenta. Pick the one you like the most.

### Install Docker

After you install the os, we need just a few utilities to let you run the car setup, mainly `git`. That's all you need

#### Docker: Installation

Just follow the [official documentation](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository). I run all those commands. This will also install the docker-compose plugin.

Then:

```shell
sudo docker run hello-world
```

If this succeeds, then you are in good shape.

#### Docker: Post-installation

Just follow the official [instructions](https://docs.docker.com/engine/install/linux-postinstall/)

#### Docker: Login to our private registry

To access our private docker images, you **must** log in to our private registry, fire up a shell, and run:

```shell
docker login -u ipb_car -p zzxMDFwg6LyM3hW6TB4c gitlab.ipb.uni-bonn.de:4567
```

####

### Extras

Install whatever you want, zsh, VSCode, vim. At this point, that's optional, and it's not related to how to launch the setup

</details>
