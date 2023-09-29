

```markdown
# Docker Swarm Lab

Docker Swarm is two main things:

1. An enterprise-grade secure cluster of Docker hosts.
2. An engine for orchestrating microservices apps.

On the clustering front, Swarm groups one or more Docker nodes and lets you manage them as a cluster. Out-of-the-box, you get an encrypted distributed cluster store, encrypted networks, mutual TLS, secure cluster join tokens, and a PKI that makes managing and rotating certificates a breeze. You can even non-disruptively add and remove nodes.

Docker Swarm is similar to Kubernetes — they both orchestrate containerized applications. While it's true that Kubernetes has more momentum and a more active community and ecosystem, Docker Swarm is an excellent technology and a lot easier to configure and deploy. It's an excellent technology for small-to-medium businesses and application deployments.

## Build a Secure Swarm Cluster

In this lab, we'll be building a secure Swarm cluster with three manager nodes and three worker nodes. You can use a different configuration with different numbers of managers and workers, and with different names and IPs.

### Log on to NodeA and Initialize a New Swarm

```bash
$ docker swarm init --advertise-addr 10.0.0.6:2377 --listen-addr 10.0.0.6:2377
Swarm initialized: current node (g7xmx514pozsv2wgs16vywukm) is now a manager.

To add a worker to this swarm, run the following command:

docker swarm join --token SWMTKN-1-4p06mjrfy9wna5ookiz8j0210ipjaoykra6iulkjleo2gyrz3n-c6p1ocul51jhak2ghyigckesc 10.0.0.6:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

The default port that Swarm mode operates on is 2377. This is customizable, but it's convention to use 2377/tcp for secured (HTTPS) client-to-swarm connections.

### List the Nodes in the Swarm

```bash
$ docker node ls
ID                            HOSTNAME   STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
g7xmx514pozsv2wgs16vywukm *   NodeA       Ready     Active         Leader           24.0.5
```

Notice that NodeA is currently the only node in the swarm and is listed as the Leader.

### Log on to wrk1 and Join It to the Swarm

```bash
$ docker swarm join --token SWMTKN-1-4p06mjrfy9wna5ookiz8j0210ipjaoykra6iulkjleo2gyrz3n-c6p1ocul51jhak2ghyigckesc 10.0.0.6:2377
This node joined a swarm as a worker.
```

```bash
$ docker node ls
ID                            HOSTNAME   STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
1omvv7bptshjm6dbvls4y8u3j     Slave      Ready     Active                          24.0.5
g7xmx514pozsv2wgs16vywukm *   Tomcat     Ready     Active         Leader           24.0.5
```

Congratulations! You've just created a 2-node swarm with 1 manager and 1 worker. As part of the process, the Docker Engine on each node was automatically put into swarm mode, and the swarm was automatically secured with TLS.
```

You can use this markdown file as documentation for setting up a secure Docker Swarm cluster with the provided instructions.
