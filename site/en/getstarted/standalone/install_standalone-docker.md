---
id: install_standalone-docker.md
title: Install Milvus Standalone
label: Install with Docker Compose
order: 0
group: standalone
summary: Installation instructions for the standalone version of Milvus.
---

# Install Milvus Standalone

This topic describes how to install Milvus standalone with Docker Compose or on Kubernetes.

You can also [build Milvus from source code](https://github.com/milvus-io/milvus#to-start-developing-milvus).

<div class="alert note">
Installing Milvus with Docker Compose can only be used for testing and cannot be used in production.
</div>

{{tab}}


## Install Milvus Standalone with Docker Compose


1. Download and save **docker-compose.standalone.yml** as **docker-compose.yml**:

```
wget https://github.com/milvus-io/milvus/releases/download/v{{var.cpu_milvus_docker_image_version}}/milvus-standalone-docker-compose.yml -O docker-compose.yml
```

> You can also [download **docker-compose.yml** on GitHub](https://github.com/milvus-io/milvus/releases/download/v{{var.cpu_milvus_docker_image_version}}/milvus-standalone-docker-compose.yml).

<div class="alert note">
If you install your Milvus standalone with the original <b>docker-compose.yml</b> file, the data will be stored under <b>./volume</b> directory. To change the mapped directory, you can either change it directly in the <b>docker-compose.yml</b> file, or run <code>$ export DOCKER_VOLUME_DIRECTORY=</code>.
</div>

2. Start Milvus Standalone:

```shell
$ docker-compose up -d
```

```text
Docker Compose is now in the Docker CLI, try `docker compose up`
Creating milvus-etcd  ... done
Creating milvus-minio ... done
Creating milvus-standalone ... done
```

*If Milvus standalone boots successfully, three running docker containers appear (two infrastructure services and one Milvus service):* 

```
$ sudo docker-compose ps
      Name                     Command                  State                          Ports
----------------------------------------------------------------------------------------------------------------
milvus-etcd         etcd -listen-peer-urls=htt ...   Up (healthy)   2379/tcp, 2380/tcp
milvus-minio        /usr/bin/docker-entrypoint ...   Up (healthy)   9000/tcp
milvus-standalone   /tini -- milvus run standalone   Up             0.0.0.0:19530->19530/tcp,:::19530->19530/tcp
```


<div class="alert note">
To stop Milvus standalone, run <code> $ sudo docker-compose down</code>.

If you want to clean up data after stopping Milvus, run <code> $ sudo rm -rf  volume</code>.

</div>


<div class="alert note">
If you want to upgrade your Milvus 2.0 version, please refer to <a href="upgrade.md">Upgrade Milvus 2.0</a>.
</div>
