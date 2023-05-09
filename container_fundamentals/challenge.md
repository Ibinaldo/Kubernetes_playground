# Challenge
Run an apache container in such a way that all logs are forwarded to the host that runs the container

## Solution
```
docker run --rm -v /dev/log:/dev/log fedora:latest logger "message from the container"
```
