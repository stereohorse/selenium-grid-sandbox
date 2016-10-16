# Selenium Grid sandbox

## How to run

```
$ vagrant up
```

## What is in the box?

This vagrant sandbox setups 3 machines:

```
vm1 [192.168.5.2] - master host with swarm manager and consul

vm2 [192.168.5.3] - first slave with swarm node
vm3 [192.168.5.4] - second swarm node
```

Swarm manager listens to port `:4000` on **vm1**. You can control swarm with:

```
$ docker -H tcp://192.168.5.2:4000 info
$ docker -H tcp://192.168.5.2:4000 ps
```

Selenium Grid is deployed on top of that Swarm cluster. Hub is available on URL:

```
http://192.168.5.3:4444/grid/console
```
