# Understanding the nature of a container

1. Applications need a runtime environment
2. Traditional runtime environment is a physical/virtual host on which an application is installed with all of its dependencies.
3. Dependencies can be a problem when updating applications.
4. As a complete runtime environment that is isolated from everything else on the system, a container is offering a solution to that problem.
5. Containers are self-contained and never offer any dependency problems.
6. Containers are **Linux**, and are running on top of a **container engine**, and as such don't offer any platform requirement either.

## Containers vs virtual machines
* Many containers can run on top of the same host kernel
* A container is not a virtual machine. Main operational difference is that a container has a default application that it must start
* Without specifying the default application, the container will start and immediately stop again as it doesn't know what to do
