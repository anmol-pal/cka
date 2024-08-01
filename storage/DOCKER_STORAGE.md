# Docker Storage

1. Storage Driver

2. Volume Driver

## Storage Driver
When docker is installed below file system is created.
Docker stores all its data here
```
/var/lib/docker
/var/lib/docker/aufs
/var/lib/docker/containers
/var/lib/docker/images
/var/lib/docker/volumes
```

Docker Layered Architecture

uses layers , and copy on write to store temporary layers.

There are two types of volume mounts
1. Volume mount  - Mounting volume created by docker under /var/lib/docker/volumes
```
docker volume create data_volume
ls /var/lib/docker/volumes/data_volume 

docker run -v data_volume:/location_inside/container nginx
```
2. Bind mount - Mounting any random volume on Docker host to container
```
docker run -v /location/on/host:/location/on/container  nginx
or
docker run \
--mount type=bind, source=/location/on/host, target=/location/on/container nginx
```
This is done by ```storage drivers```
eg: AUFS | ZFS | BTRFS | DEVICE MAPER | OVERLAY

## Volume Driver

eg: Local | Azure File Storage | Convoy | Portworx | Digital Ocean Block Storage | NetApp | VMware vSphere Storage | RexRay

When you run a docker container, you can choose a volume driver to provision it.


