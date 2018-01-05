## Welcome to [Docker DOC Pages](https://kemixkoo.github.io/docker-docs/)

### Commands 
- Stop all running containers
```
docker stop $(docker ps -q)
docker ps -q | xargs docker stop
```
- Kill all running containers
```
docker kill $(docker ps -q)
docker ps -q | xargs docker kill
```
- Remove all stopped containers
```
docker ps -a | grep "Exited" | awk '{print $1 }' | xargs docker rm
```
- Remove all `<none>` images
```
docker images | grep '<none>' | awk '{print $3 }' | xargs docker rmi
```
- Remove all containers
```
docker rm -f $(docker ps -a -q)
```

**NOTE:**

**If no any containers/images, will have problem when execute the front commands.**

**Also, make sure current user is in `sudoers` list. Else need add `sudo` in the front of each commands.**



-----------------------

### Difference between `stop` and `kill`
- `docker stop`: Stop a running container (send SIGTERM, and then SIGKILL after grace period)
   The main process inside the container will receive SIGTERM, and after a grace period, SIGKILL
   
- `docker kill`: Kill a running container (send SIGKILL, or specified signal) 
   The main process inside the container will be sent SIGKILL, or any signal specified with option --signal.

Means, *"kill"* will stop container immediately, *"stop"* before stop, still have time to clean up, save state,finish any currently-executing requests, etc.
