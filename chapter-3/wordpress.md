# Deploying wordpress on the Swarm cluster

Wordpress is a popular blogging tool. It is written in PHP and requires a database backend. Let's go ahead and deploy wordpress on our cluster.

We need to create two services here, one for the database (mariadb) and other for frontend (php). Let's call them `db` and `wp` respectively. As wp depends on a database, let's start with creating the `db` service.

If you haven’t already, open a terminal and ssh into **manager** node.

```bash

manager:~$ docker service create \
    --name mariadb \
    --replicas 1 \
    --network wp \
    --constraint=node.role==manager \
    --secret source=root_db_password,target=root_db_password \
    --secret source=wp_db_password,target=wp_db_password \
    -e MYSQL_ROOT_PASSWORD_FILE=/run/secrets/root_db_password \
    -e MYSQL_PASSWORD_FILE=/run/secrets/wp_db_password \
    -e MYSQL_USER=wp \
    -e MYSQL_DATABASE=wp \
    mariadb:10.1
uo33zcv6e4fpewz2tpf1bfaw0

manager:~$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE
uo33zcv6e4fp        mariadb             replicated          1/1                 mariadb:10.1
```

Now let's create the `wp` service with the following commandx

```bash
manager:~$ docker service create \
    --name wp \
    --constraint=node.role==worker \
    --replicas 1 \
    --network wp \
    --publish 80:80 \
    --secret source=wp_db_password,target=wp_db_password,mode=0400 \
    -e WORDPRESS_DB_USER=wp \
    -e WORDPRESS_DB_PASSWORD_FILE=/run/secrets/wp_db_password \
    -e WORDPRESS_DB_HOST=mariadb \
    -e WORDPRESS_DB_NAME=wp \
    wordpress:4.7
    
iepao2b38x9i9np2lyq1ks8f5

manager:~$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE
iepao2b38x9i        wp                  replicated          1/1                 wordpress:4.7
uo33zcv6e4fp        mariadb             replicated          1/1                 mariadb:10.1
```

To verify the wordpress setup open your browser and visit http://localhost:8080/
(8080 port number comes from the Vagrantfile.)


---
##### Resources
https://blog.maddevs.io/deploy-and-scale-wordpress-with-docker-cloud-swarm-mode-f780d4e735cb
