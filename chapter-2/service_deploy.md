# Deploy a service to the Swarm

After you create a swarm, you can deploy a service to the swarm. We have a 3 node swarm cluster but that is not a requirement for deploying services, you can deploy a service on a single node cluster too.

The command used for deploying a service is `docker service create`.

Open a terminal and ssh into the **manager** node and run the following command:

```bash
manager:~$ docker service create --replicas 1 --name helloworld alpine ping google.com
xvdsz9zwjfwwkbu4e4mp15xbg
```
- The `docker service create` command creates the service.
- The `--name` flag names the service helloworld. (OPTIONAL)
- The `--replicas` flag specifies the desired number of running instances. (OPTIONAL)
- The argument `alpine` is the name of docker image to be used.
- The argument `ping google.com` define the command to be executed by the service.

Run `docker service ls` to see the list of running services:

```bash
manager:~$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE
xvdsz9zwjfww        helloworld          replicated          1/1                 alpine:latest
```

The REPLICAS column shows that 1/1 replicas are running for service with NAME helloworld. Also the ID column is the service ID which was returned on `docker service create` command.

In the next chapter we see how to inspect a service.
