# Scaling service 

Once you have deployed a service to a swarm, you are ready to use the Docker CLI to scale the number of service ps in the swarm.

If you haven’t already, open a terminal and ssh into **manager** node.

Run the following command to change the desired state of the service running in the swarm:
```bash
  $ docker service scale <SERVICE-ID>=<NUMBER-OF-TASKS>
```
  
For example:

```bash
manager:~$ docker service scale helloworld=5

 helloworld scaled to 5
```

Run `docker service ps <SERVICE-ID>` to see the updated task list:

```bash 
manager:~$ docker service ps helloworld
ID                  NAME                IMAGE               NODE                DESIRED STATE       CURRENT STATE            ERROR               PORTS
ko6c86bij1tj        helloworld.1        alpine:latest       node2               Running             Running 2 hours ago
y8kmb3424yrt        helloworld.2        alpine:latest       node1               Running             Running 38 seconds ago
ddmvhrnz9v7x        helloworld.3        alpine:latest       manager             Running             Running 39 seconds ago
t4hh1mqw8odc        helloworld.4        alpine:latest       manager             Running             Running 39 seconds ago
xhosuapvgre2        helloworld.5        alpine:latest       node2               Running             Running 39 seconds ago
```

You can see that swarm has created 4 new tasks to scale to a total of 5 running instances of Alpine Linux. The tasks are distributed between the three nodes of the swarm. One is running on manager.

Run docker ps to see the containers running on the node where you’re connected. The following example shows the tasks running on manager:

```bash
manager:~$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
7d37b38b8df2        alpine:latest       "ping docker.com"   7 minutes ago       Up 7 minutes                            helloworld.3.ddmvhrnz9v7x44sdp8fo88kib
b42fed3e66fb        alpine:latest       "ping docker.com"   7 minutes ago       Up 7 minutes                            helloworld.4.t4hh1mqw8odckpw3v8sin0yxe
```

If you want to see the containers running on other nodes, ssh into those nodes and run the docker ps command.
