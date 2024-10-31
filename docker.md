## What is Docker?
Docker - it's a development tool, that packs all of the working stuff such as code, environment, libraries and dependencies to a portable container.

## Why Docker makes life easier?
### Before
Let's see how the development process were before the Docker was introduced.

Developers should have installed a needed software and tools for building application into their own OS. Typically, installation process of all this stuff was complex and depends on a specific OS.

Imagine our company has an app. To build it you need to get executable from file from C++ source code. With the code itself Developers team have to create a textual guideline about how to make an executable on a server.

And let's say that our app also uses a Postgre database too. With that Devs also would create another textual guideline on how to configure and run db on the server.

With that, OPS (Operational Team) starts to configure server. But, it can be very complicating and frustrating because something can show up upon the installation process or Devs can simply forgot to mention some details because of human factor. Imagine doing that every time something changed.


### Nowadays
With containers you don't have to install all of this stuff into our machine.

Docker gives you an isolated environment and with that you can have all of your dependencies and configurations just in the Docker container and simply start to use it by one command (same for all OS).

> Docker standardizes process of running any service on any local dev environment

> Easy to run different versions of same app without any conflicts

Today developers just pack all of the dependencies to a container and deliver it to the OPS team. With that, they only have to configure a Docker runtime on a server and run the container.

There is less room for issues with this setup.


## Docker vs Virtual Machine
> Docker is a virtualization tool just like a Virtual Machine.

In order to understand how Docker run it's containers, we should know how an OS is made up.

OS (Linux, MacOS, Windows) has a 2 main layers - OS kernel and OS Application Level.

    Application layer

    OS kernel

    Hardware

* Kernel is at the core of every operating system

* Kernel interacts between hardware & software components

So, as we now by this moment, Docker and Virtual Machines is both virtualization tools.

**What parts of the OS do they virtualize?**

*Docker virtualizes an Application layer* and uses host's kernel.

* Contains the OS application layer

* Services and apps installed on top of that layer


*VM virtualizes an OS kernel and an Application layer* - basically a complete operating system.

Which means when you download a VM it uses it's own kernel.

### Pros/Cons

#### Docker Pros

* Docker images smaller than VMs (couple of **MB** vs couple of **GB**).

* Containers take seconds to start, while VM has to start it's kernel every time on boot up

#### Docker Cons
* VM is compatible with all OS but you can't do that with Docker. At least directly.

Docker works with linux kernel.

Docker Desktop it's an app for running linux-based containers on a MacOS and Windows by using a Hypervisor layer to create a lightweight linux kernel.

<!--#TODO: learn about Hypervisor and virtualization-->

### Docker Images vs Docker Containers
Docker allows to package the application along with it's environment to artifacts.

Artifacts like a regular files can be easily shared and moved.

**Docker image** is an executable application artifact. But different with from C++ or Java executable is the environment, any services like npm, node and a source code.

But what is a container then?

To run the Docker Image (basically an app) in our computer, preconfigured app should run somewhere. An instance of a Docker Image is running on a **Docker Container**.

From one image you can run multiple containers.

`docker images` - List all Docker images

`docker ps` - List running containers

We get containers when we run a Docker Image. But how do we get these images?

### Docker Registries
**Docker Registries** - a storage and distribution for Docker images.

Official images available from applications like Redis, Mongo, Postgres etc.

Official images are maintained by the software authors in collaboration with the Docker community.

Docker hosts one of the biggest Docker Registry, called **Docker Hub**.

Docker tags are used to identify images by name (tag = version).

### How to get an Image
1. Locate image, for example nginx, a simple webserver.

2. Select the tag.

3. Execute `docker pull nginx:1.23`

After this Docker Client (our Docker CLI) says to Docker Service to pull the Image from Docker Hub.

4. Execute `docker images`


### Run an Image
Simply execute `docker run nginx:1.23`.

Running `docker ps` we can get some info about running containers.

To run container without block a terminal `docker run -d nginx:1.23`.

To see log of a running container if we run our application in the background `docker logs {containerID}`

* Docker pulls Images automatically when running an Images

For example, we can simply do without any pull: `docker run redis`.


### Port Binding
How do we get access to a container? We can't right now.

Application inside container runs in an isolated Docker network.

We need to expose the container port to the host (the machine the container runs on).

Each application has some standard port. nginx is port 80. Now we can't access it through browser like this: *localhost:80*.

`docker stop {container}` - to stop a container

Port forwarding:

`docker run -d -p {host_port}:{container_port} {image}:{tag}`

`docker run -d -p 9000:80 nginx:1.23`


Now with -p 9000:80 we expose docker container to our local network.

*localhost:9000* - code 200.

For our host machine we can choose any port. But it's standard to use the same port on your host as container is using.


### Start and stop containers

