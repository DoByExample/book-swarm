# Inspecting a service on the swarm

When you have deployed a service to your swarm, you can use the Docker CLI to see details about the service running in the swarm.

If you haven’t already, open a terminal and ssh into the **manager** node.

Run `docker service inspect --pretty <SERVICE-ID>` to display the details about a service in an easily readable format.

To see the details on the helloworld service:

```
manager:~$ docker service inspect --pretty helloworld

ID:		xvdsz9zwjfwwkbu4e4mp15xbg
Name:		helloworld
Service Mode:	Replicated
 Replicas:	1
Placement:
UpdateConfig:
 Parallelism:	1
 On failure:	pause
 Max failure ratio: 0
RollbackConfig:
 Parallelism:	1
 On failure:	pause
 Max failure ratio: 0
ContainerSpec:
 Image:		alpine:latest@sha256:58e1a1bb75db1b5a24a462dd5e2915277ea06438c3f105138f97eb53149673c4
 Args:		ping docker.com
Resources:
Endpoint Mode:	vip
```

The output shows a blueprint of the service with details like ID, name, replicas, Image, Args etc.

To see which nodes are running the service use `docker service ps <SERVICE-ID>`.

```bash
manager:~$ docker service ps helloworld
ID                  NAME                IMAGE               NODE                DESIRED STATE       CURRENT STATE           ERROR               PORTS
xvdsz9zwjfww        helloworld.1        alpine:latest       node2               Running             Running 4 minutes ago
```

In this case, the one instance of the helloworld service is running on the **node2** node. You may see the service running on your manager node. By default, manager nodes in a swarm can execute tasks just like worker nodes.

Swarm also shows you the DESIRED STATE and LAST STATE of the service task so you can see if tasks are running according to the service definition.

You can ssh into **node2** and verify that there is a container running on that node.

```bash
node2:~$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
f4b82c3f82e6        alpine:latest       "ping docker.com"   2 minutes ago       Up 2 minutes                            helloworld.1.ko6c86bij1tjvvlxp19i6wuu4
```

You can also check logs for the container with `docker logs -f CONTAINER-ID`

```bash
node2:~$ docker logs -f f4b82c3f82e6
PING docker.com (54.210.142.11): 56 data bytes
```
