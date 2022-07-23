# Jenkins docker
* Jenkins CI with docker client

# Build docker image

```
docker build -t jenkins-docker .
```

# stop & remove old jenkins container e.i `jenkins`

```
docker stop jenkins && docker rm jenkins
```

* Note: Because the old contents are under a volume they will not remove.

Check it out:

```
ls /var/jenkins_home/
```

Now we create une jenkins container and we connect it docker sockets:

```
docker run --restart unless-stopped -p 8080:8080 -p 50000:50000 -v /var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins -d jenkins-docker
```

Run linux shell:
```
docker exec -it jenkins bash
```

check if you have access to docker sockets and docker command inside jenkins container:
```
ls -ahl /var/run/docker.sock
```

OUTPUT:

```
srw-rw---- 1 root docker 0 Jun 24 10:55 /var/run/docker.sock
```

```
docker ps -a
```

OUTPUT:

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                                                      NAMES
6f821ad08f5b        jenkins-docker      "/usr/bin/tini -- /u…"   2 minutes ago       Up 2 minutes        0.0.0.0:8080->8080/tcp, :::8080->8080/tcp, 0.0.0.0:50000->50000/tcp, :::50000->50000/tcp   jenkins
```


Exit:

```
exit
```


https://hub.docker.com/r/alagarbaa/docker-nodejs-demo