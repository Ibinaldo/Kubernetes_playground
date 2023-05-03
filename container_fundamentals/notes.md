# 2.1 Understanding the nature of a container

1. Applications need a runtime environment
2. Traditional runtime environment is a physical/virtual host on which an application is installed with all of its dependencies.
3. Dependencies can be a problem when updating applications.
4. As a complete runtime environment that is isolated from everything else on the system, a container is offering a solution to that problem.
5. Containers are self-contained and never offer any dependency problems.
6. Containers are **Linux**, and are running on top of a **container engine**, and as such don't offer any platform requirement either.

## 2.1.1 Containers vs virtual machines
* Many containers can run on top of the same host kernel
* A container is not a virtual machine. Main operational difference is that a container has a default application that it must start
* Without specifying the default application, the container will start and immediately stop again as it doesn't know what to do
* Virtual machines are isolated, and you can run multiple OS virtual machines e.g. windows, Linux etc. However, it takes up a lot of overhead.

# 2.2 Understanding container architecture
* Container are Linux and built on top of Linux kernel features
* Namespaces provide strict isolation at a Linux kernel level
* CGroups provide resource allocation to guarantee dedicated resources to be available.
* SELinux can be used to enforce security in a containerized environment.

## 2.2.1 Docker architecture
* Docker uses a client-server architecture
* The docker **daemon** is responsible for building, running and downloading container images.
* The docker **client** is responsible for communicating with the docker server.
* Note: *containers are slightly less secure than virtual machines*. Consider using SELinux.

# 2.3 Container offerings
1. LXC (early container solution)
2. Docker (2013)
3. Linux Systemd
4. Rkt (2014): More secure alternative to Docker but its slowly phasing out.
5. Podman: New, alternative to Docker in Red Hat Enterprise Linux 8

# 2.4 Docker and Podman
* **Images** are read-only environments that contain the runtime environment that includes the application and all libraries it requires
* **Registries** are used to store images. Docker Hub is a common registry, but private registries can also be created.
* **Containers** are the isolated runtime environments where the application is running. By using **Namespaces** the containers can be offered as a strictly isolated environment.
* Containers are Linux, so you need a base Linux distribution to be running within your containers.
* The container host platform can be a full Linux distribution, but also a minimal distribution such as Fedora Atomic or CoreOS.

# 2.5 Container images
* Images are what the container is started from
* Base images are available at Docker Hub
* Can go to [docker hub](https://hub.docker.com) to search for images, or use the CLI interface (Docker search)
* Container images are using multiple layers of filesystem. Docker images are immutable, each modification adds an extra layer to the pre-existing layers.
* The container sees it as a single virtual file system by using UnionFS
* Modifications are stored in a new layer, so only the new layer needs to be stored.

two approaches to creating an image:
1. Using a running container: container is started, modifications are applied to the container. From the container, **docker** commands are used to write modifications.
2. Using a Dockerfile: a Dockerfile contains instructions for building an image. Each instruction adds a new layer to the image, which offers more control over which files are added to which layer.

### Dockerfile
* Its a way to automate container builds
* It contains all instructions required to build a container image
* So instead of distributing images, you can distribute the Dockerfile. 
