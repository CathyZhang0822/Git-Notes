# OPA - Open Policy Agent
## Overview
OPA decouples policy decision-making from policy enforcement. When your software needs to make policy decisions it queries OPA and supplies structured data (e.g., JSON) as input. OPA accepts arbitrary structured data as input.   
理解：Services send JSON类似的data 到OPA, OPQ做了decisions之后，把decisions返给services.   
OPA可以做而且不限于以下decisions：
- Which users can access which resources.
- Which subnets egress traffic is allowed to.
- Which clusters a workload must be deployed to.
- Which registries binaries can be downloaded from.
- Which OS capabilities a container can execute with.
- Which times of day the system can be accessed at.

## Example
![example](https://user-images.githubusercontent.com/36396754/102041966-92563500-3d85-11eb-9d34-7996913187e7.png)

There are 3 kinds of components in the system:
- Servers expose zero or more protocols (e.g., http, ssh, etc.)
- Networks connect servers and can be public or private. Public networks are connected to the Internet.
- Ports attach servers to networks.
All of the servers, networks, and ports are provisioned by a script. The script receives a JSON representation of the system as input:    
理解：这就是services
```
{
    "servers": [
        {"id": "app", "protocols": ["https", "ssh"], "ports": ["p1", "p2", "p3"]},
        {"id": "db", "protocols": ["mysql"], "ports": ["p3"]},
        {"id": "cache", "protocols": ["memcache"], "ports": ["p3"]},
        {"id": "ci", "protocols": ["http"], "ports": ["p1", "p2"]},
        {"id": "busybox", "protocols": ["telnet"], "ports": ["p1"]}
    ],
    "networks": [
        {"id": "net1", "public": false},
        {"id": "net2", "public": false},
        {"id": "net3", "public": true},
        {"id": "net4", "public": true}
    ],
    "ports": [
        {"id": "p1", "network": "net1"},
        {"id": "p2", "network": "net3"},
        {"id": "p3", "network": "net2"}
    ]
}
```
