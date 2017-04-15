# Setting up local environment

We will be using vagrant to create 3 virtual machines locally which will act as our swarm cluster for the exercises. 

* Manager 10.0.7.100
* Node1 10.0.7.11
* Node2 10.0.7.12

[If you don't have vagrant installed, go ahead and download it here https://www.vagrantup.com/downloads.html ]


``` bash
$ vagrant plugin install vagrant-alpine
$ git clone https://github.com/DoByExample/local_swarm.git
$ cd local_swarm
$ vagrant up
```

At this point you will have 3 vm's running which can be verified with `vagrant status`

```bash
local_swarm ❯❯❯ vagrant status                                                                                                                               master
Current machine states:

manager                   running (virtualbox)
node1                     running (virtualbox)
node2                     running (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`
```
