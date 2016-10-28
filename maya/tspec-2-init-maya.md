
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

ubuntu@ubuntu-xenial:~$ # What if I create another container of same image ?

ubuntu@ubuntu-xenial:~$ sudo docker run -d -p 80 tutum/hello-world
209d36f619fd501b852bfb195e470146d23553fa216f295afa693d368e5c4d36

ubuntu@ubuntu-xenial:~$ sudo docker ps
CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS  PORTS  NAMES
209d36f619fd        tutum/hello-world               "/bin/sh -c 'php-fpm "   5 seconds ago       Up 3 seconds 0.0.0.0:32770->80/tcp   admiring_poincare
95c5a07f76d0        tutum/hello-world               "/bin/sh -c 'php-fpm "   24 minutes ago      Up 24 minutes       0.0.0.0:32769->80/tcp   boring_mahavira
de8d428470b1        gliderlabs/registrator:latest   "/bin/registrator etc"   57 minutes ago      Up 57 minutes                               mayaregistrar

ubuntu@ubuntu-xenial:~$ # Docker creates 3 containers
ubuntu@ubuntu-xenial:~$ # Lets check the etcd database

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
     },{
     "key":"/services/hello-world/ubuntu-xenial:admiring_poincare:80",
     "value":":32770",
     "modifiedIndex":10,
     "createdIndex":10
   }],
   "modifiedIndex":9,
   "createdIndex":9
 }
}

ubuntu@ubuntu-xenial:~$ # We see 2 unique keys based on docker names
ubuntu@ubuntu-xenial:~$ # These keys are nested under /services/hello-world
```

### etcd leader stats

- leader has a view of entire cluster
- keeps track of:
  - latency
  - count of failed / successful Raft RPC requests

```bash
ubuntu@ubuntu-xenial:~$ curl http://localhost:2379/v2/stats/leader

{"leader":"1678331e18f3811d",
 "followers":{
   "12df9dc201e641ca":{
     "latency":{
       "current":0.002169,
       "average":0.009764827744420562,
       "standardDeviation":0.04865928038819622,
       "minimum":0.000552,
       "maximum":1.668563
     },
     "counts":{
       "fail":0,
       "success":17654
     }
   },
   "d860400699ce61e":{
     "latency":{
       "current":0.002077,
       "average":0.009798825684871677,
       "standardDeviation":0.05406535945924713,
       "minimum":0.000614,
       "maximum":2.393876
     },
     "counts":{
       "fail":0,
       "success":17193
     }
   }
 }
}

```

### Other etcd API options

- curl http://localhost:2379/v2/stats/self
- curl http://localhost:2379/v2/stats/store
- Set key from a file
  - curl http://localhost:2379/v2/keys/afile - XPUT --data-urlencode value@file.txt
- Deleting a dir
  - curl http://localhost:2379/v2/keys/some_dir?dir=true -XDELETE
  - curl http://localhost:2379/v2/keys/some_dir?recursive=true -XDELETE
