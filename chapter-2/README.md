# Services

### What is a swarm?

A `swarm` is a cluster of (Docker) `nodes`, where you deploy `services`. The Docker Engine CLI and API include commands to **manage swarm nodes**, and deploy and **orchestrate services** across the swarm.

### What is a node?

A **node** is an instance of the Docker engine participating in the swarm. You can also think of this as a Docker node. You can run one or more nodes on a single physical computer or cloud server.

**Manager nodes** perform the orchestration and cluster management functions required to maintain the desired state of the swarm. Manager nodes elect a single leader to conduct orchestration tasks.

**Worker nodes** receive and execute tasks dispatched from manager nodes. An agent runs on each worker node and reports on the tasks assigned to it. The worker node notifies the manager node of the current state of its assigned tasks so that the manager can maintain the desired state of each worker.

### Services

A **service** is the definition of the tasks to execute on the worker nodes. It is the central structure of the swarm system and the primary root of user interaction with the swarm.

When you create a service, you specify which container image to use and which commands to execute inside running containers.

---
https://docs.docker.com/engine/swarm/key-concepts/
