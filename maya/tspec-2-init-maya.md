
```bash
ubuntu@ubuntu-xenial:~$ sudo docker ps
CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS              PORTS                   NAMES
95c5a07f76d0        tutum/hello-world               "/bin/sh -c 'php-fpm "   7 minutes ago       Up 6 minutes        0.0.0.0:32769->80/tcp   boring_mahavira
de8d428470b1        gliderlabs/registrator:latest   "/bin/registrator etc"   40 minutes ago      Up 40 minutes                               mayaregistrar

ubuntu@ubuntu-xenial:~$ # you see 2 containers. One is registrator & other is a hello-world container.
ubuntu@ubuntu-xenial:~$ # lets access the etcd

ubuntu@ubuntu-xenial:~$ curl http://localhost:2379/v2/keys
{"action":"get",
 "node":{
   "dir":true,
   "nodes":[{
     "key":"/services",
     "dir":true,
     "modifiedIndex":9,
     "createdIndex":9
    }]
  }
}

ubuntu@ubuntu-xenial:~$ # you see the concept of node, dir, nodes, key,& audit columns
ubuntu@ubuntu-xenial:~$ # where is the value ?

ubuntu@ubuntu-xenial:~$ curl http://localhost:2379/v2/keys/services
{"action":"get",
 "node":{
   "key":"/services",
   "dir":true,
   "nodes":[{
     "key":"/services/hello-world",
     "dir":true,
     "modifiedIndex":9,
     "createdIndex":9
   }],
   "modifiedIndex":9,
   "createdIndex":9
 }
}

ubuntu@ubuntu-xenial:~$ # /keys/services seems to be a key in etcd. A nested key structure.
ubuntu@ubuntu-xenial:~$ # where is the value ?

ubuntu@ubuntu-xenial:~$ curl http://localhost:2379/v2/keys/services/hello-world
{"action":"get",
 "node":{
   "key":"/services/hello-world",
   "dir":true,
   "nodes":[{
     "key":"/services/hello-world/ubuntu-xenial:boring_mahavira:80",
     "value":":32769",
     "modifiedIndex":9,
     "createdIndex":9
   }],
   "modifiedIndex":9,
   "createdIndex":9
 }
}

ubuntu@ubuntu-xenial:~$ # I see a value here. The port is the value i.e. 
ubuntu@ubuntu-xenial:~$ # 32769 is the port on host (0.0.0.0:32769->80/tcp) pointing to container's tcp:80.
ubuntu@ubuntu-xenial:~$ # This is how docker event is structured perhaps.
ubuntu@ubuntu-xenial:~$ # Or perhaps Registrator does something in between ?


ubuntu@ubuntu-xenial:~$ curl http://localhost:2379/v2/keys/services/hello-world/ubuntu-xenial:boring_mahavira:80
{"action":"get",
 "node":{
   "key":"/services/hello-world/ubuntu-xenial:boring_mahavira:80",
   "value":":32769",
   "modifiedIndex":9,
   "createdIndex":9
 }
}

ubuntu@ubuntu-xenial:~$ # there is no dir: true here !! Just the key value !!

```
