# Deleting the service running on the swarm

In the final section of this chapter we will see how to delete a service as we would not be using `helloworld` in the next chapter.

If you haven’t already, open a terminal and ssh into the **manager** node.

Run `docker service rm <SERVICE-ID>` to remove a service.

```bash
$ docker service rm helloworld

helloworld
```

Run `docker service inspect <SERVICE-ID>` to verify that the swarm manager removed the service. The CLI returns a message that the service is not found:

```bash
manager:~$ docker service inspect helloworld
[]
Status: Error: no such service: helloworld, Code: 1
```


