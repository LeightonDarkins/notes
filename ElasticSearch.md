# ElasticSearch

## 1.7.2

- only runs with \$JAVA_HOME pointing to 1.8 JVM :(
-

## ElasticSearch Deployment

### General

- embedded unsupported since v2.0 (now at v6.5)
- standalone performs exactly the same
- well documented
- disk encryption is a must (2008 to 2012r2 at least)

### Windows installation

- zip
- msi
- run as a service

### Linux installation

- zip

### Resource usage

- default 1gb of heap
- turn off swapping if not the only service on a box
- most other settings aren't needed

### Deploy via docker

- just pull the image and go
- set memory/cpu limits via the Docker daemon
- no risk to the PSServer JVM

### ES Server Downtime

- how does the Client deal with the ES service dying? :(
