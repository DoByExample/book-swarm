# Create a Swarm

After you complete the vagrant setup, you're ready to create a swarm. Make sure that docker daemon is running on all three nodes.



1. ssh into `manager` vm
```
local-swarm ❯❯❯ vagrant ssh manager
...
manager:~$
```

2. Create a swarm using `docker swarm init` command  
```bash
manager:~$ docker swarm init --advertise-addr 10.0.7.100
Swarm initialized: current node (nxjtuxrd8mdx5975ybf7gowkh) is now a manager.
To add a worker to this swarm, run the following command:

    docker swarm join \
    --token SWMTKN-1-2w490za4y94p2xjgh6ln5b57bdqc2ff9o09hh91g8z3dbxirh4-9mt0j1iaa57ti9wk9upunodn6 \
    10.0.7.100:2377
To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```
The **--advertise-addr** flag configures the manager node to publish its address as 10.0.7.100. The other nodes in the swarm must be able to access the manager at the IP address.  
The output includes the command that contains the token ID of the manager. This command can be used to join new nodes to the swarm. Nodes will join as managers or workers depending on the value for the **--token** flag.
If you don’t have the command available, you can run the following command on a manager node to retrieve the join command for a worker:
```
manager:~$ docker swarm join-token worker
To add a worker to this swarm, run the following command:

    docker swarm join \
    --token SWMTKN-1-2w490za4y94p2xjgh6ln5b57bdqc2ff9o09hh91g8z3dbxirh4-9mt0j1iaa57ti9wk9upunodn6 \
    10.0.7.100:2377
```

3. Run `docker info` to view the current state of the swarm:
``` bash
$ docker info
..snip..
Swarm: active
  NodeID: nxjtuxrd8mdx5975ybf7gowkh
  Is Manager: true
  ClusterID: wb59ecpg6czv12udv8lgky4w2
  Managers: 1
  Nodes: 1
..snip..
```

4. Run the docker node ls command to view information about nodes:
``` bash
manager:~$ docker node ls
ID                           HOSTNAME  STATUS  AVAILABILITY  MANAGER STATUS
nxjtuxrd8mdx5975ybf7gowkh *  manager   Ready   Active        Leader
```

Our Swarm is now setup and it's time to add nodes to our swarm. By default the manager (leader) node works as a worker too i.e. any service you deploy on swarm might as well run on this node but this can be configured otherwise. 
