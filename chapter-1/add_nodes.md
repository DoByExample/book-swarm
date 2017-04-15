# Adding nodes to the swarm

Once you’ve created a swarm with a manager node, you’re ready to add worker nodes.

1. Open a new terminal and ssh into the **node1**, our worker node for the day
```bash
local_swarm ❯❯❯ vagrant ssh node1
...
node1:~$
```
Run the command produced by the docker swarm init output from the Create a swarm tutorial step to create a worker node joined to the existing swarm
```bash
node1:~$ docker swarm join \
    --token SWMTKN-1-2w490za4y94p2xjgh6ln5b57bdqc2ff9o09hh91g8z3dbxirh4-9mt0j1iaa57ti9wk9upunodn6 \
    10.0.7.100:2377
This node joined a swarm as a worker.
```

2. Open a new terminal and ssh into **node2**, our second worker node, and run the smae `docker swarm join command`
```bash
node2:~$ docker swarm join \
    --token SWMTKN-1-2w490za4y94p2xjgh6ln5b57bdqc2ff9o09hh91g8z3dbxirh4-9mt0j1iaa57ti9wk9upunodn6 \
    10.0.7.100:2377
This node joined a swarm as a worker.    
```

3. Switch to **manager** and verify the cluster size (3 in this case) with `docker node ls` command
```bash
manager:~$ docker node ls
ID                           HOSTNAME  STATUS  AVAILABILITY  MANAGER STATUS
a6j1abnp8vb6ki98vzjc080nr    node2     Ready   Active
f7am684112gdhebg45kj61jnt    node1     Ready   Active
nxjtuxrd8mdx5975ybf7gowkh *  manager   Ready   Active        Leader
```

The MANAGER column identifies the manager nodes in the swarm. The empty status in this column for node1 and node2 identifies them as worker nodes.

Swarm management commands like `docker node ls`  **only work on manager nodes**.
