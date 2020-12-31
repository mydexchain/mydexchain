# MyDexChain

[![Releases](https://img.shields.io/badge/version-1.0.1-orange)](#)
[![Jenkins Build](https://img.shields.io/badge/build-passing-brightgreen)](#)
[![Docker Build](https://img.shields.io/badge/docker%20build-passing-brightgreen)](#)
[![Docker Image](https://img.shields.io/docker/image-size/mydexchain/mydexchain/latest?color=green)](#)
[![Docker Pulls](https://img.shields.io/docker/pulls/mydexchain/mydexchain?color=red)](https://hub.docker.com/repository/docker/mydexchain/mydexchain)
[![LICENSE](https://img.shields.io/badge/license-Apache-lightgray)](https://github.com/mydexchain/mydexchain/blob/master/LICENSE)

MyDexChain is the newest technology for `blockchain` and can be used as a payment gateway.

- [`MyDexChain`](https://mydexchain.io) : The official web page of MyDexChain
- [`MyDexPay`](https://mydexpay.io): MyDexChain Masterlife Web Page
- [`Academy`](https://academy.mydexchain.io): MyDexChain Trainings and Education Centre

This guide is used by dozens of product teams at MyDexChain. Have a question or comment? [Open an issue!](https://github.com/mydexchain/mydexchain/issues/new)

- [Release Notes](#release-notes)
- [MyDexChain Node Requirements](#mydexchain-node-requirements)
- [Pre-Installation Steps](#pre-installation-steps)
- [Usage](#usage)
- [FAQ](#faq)
- [Roadmap](#roadmap)

## Release Notes

##### 1.0.1
- Fixed PostgreSQL PID Lock Problem
- Fixed Block Logs 

## MyDexChain Node Requirements

- MyDexChain Node Minimum Requirements: **`2 Core`** of CPU **`4GB`** of Memory and **`100GB`** of HDD
- Tested Operation Systems `Windows Server 2016 or Later` || `Centos` || `Ubuntu` || `Amazon Linux`
- At Least `5mbit` of `Internet Connection` with Port `2020` Egress Allowed

## Pre-Installation Steps

MyDexChain is fully docker compatible and please follow [Windows](https://docs.docker.com/docker-for-windows/install/), [Centos](https://docs.docker.com/engine/install/centos/), [Ubuntu](https://docs.docker.com/engine/install/ubuntu/), [Amazon Linux](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html), [MAC OS](https://docs.docker.com/docker-for-mac/install/) installation steps before running MyDexChain Node. After docker installation open a command line || terminal and run command to check the docker version.

```
docker -v
```

> **Output**: Docker version 20.10.0, build 7287ab3


## Usage

##### 1. Run MyDexChain:

MyDexChain docker file is stored in dockerhub and ready for use with command: (Please check the version and use as tag rather than latest)

```
docker run -d --rm -p 2020:2020 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
```

After docker container **comes up** run the command;

```
docker ps
```

> **Output**: db641c6c55b7   mydexchain/mydexchain   "/startup.sh"   32 seconds ago   Up 31 seconds   0.0.0.0:2020->2020/tcp, 5432/tcp   mydexchain


##### 2. Follow Blocks:

```
docker attach mydexchain
```



##### 3. Node RestAPI commands :

```
"http://{DockerHostIP}:2020/setDextracker/{dexTrackerNumber}”
```
- `dexTrackerNumber : DexChain Tracker Number`
```
“http://{DockerHostIP}:2020/isWallet/{address}”
```
- `address: Dexchain Address`
```
"http://{DockerHostIP}:2020/balanceWallet/{address}"
```
- `address: Dexchain Address`
```
“http://{DockerHostIP}:2020/createWallet/{password}”
```
- `password: Dexchain Address password “Please Don’t Forget it”`
```
"http://{DockerHostIP}:2020/getTransactions/{address}&{limit}”
```
- `address: Dexchain Address`
- `limit: number of records`
```
"http://{DockerHostIP}:2020/sendTransaction/{sender}&{password}&{receiver}&{amount}&{fee}&{contract}&{description}"
```
- `sender : Sender Dexchain Address`
- `password: Dexchain Address password`
- `receiver: Receiver Dexchain Address`
- `amount: Amount of XMD`
- `fee: Fee of Transaction`
- `contract: DexChain Contract Address (if null please set “mydexchain”)`
- `description: Statements of Transaction (if null please set “null”)`

## FAQ

### Where Can I Run MyDexChain Node?
You can run MyDexChain Node on
- `Amazon Web Services`
- `Azure`
- `Google Cloud`
- `Your Own Server/Desktop`

### How Can I Update to the Latest MyDexChain Version?
Run the command on Current DockerHost:

`docker kill mydexchain && docker pull mydexchain/mydexchain && docker run -d --rm -p 2020:2020 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest`


### Common Problems
These options are settings that change shell behavior. The following table is a list of options that might be useful to you:

| Check | How         | 
| :---: | :---------- | 
| Cannot connect to the Docker daemon. Is the docker daemon running on this host?  | Check your docker service is up and running.|
| Block Sync is not working  | Check your internet connectivity. |


### How to Backup the MyDexChain Node?

MyDexCahin maps blocks inside PostgreSQL and it has been addressed inside dockerfile. All the data is saved inside **`/var/lib/docker/volumes/mydexchain`** and make sure that you **backup** the folder.

#### Linux & MacOs

##### 1. Stop `MyDexChain` Node Docker Container (For Data Consistency):

``` 
docker kill mydexchain
```

##### 2. Copy `/var/lib/docker/volumes/mydexchain` to Backup Path:

``` 
rsync -avzhHP /var/lib/docker/volumes/mydexchain/ /backup_path/mydexchain/
```

##### 3. Start `MyDexChain` Docker Container on the New Docker Host :

``` 
docker run -d --rm -p 2020:2020 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
```


##### 4. Follow the Blocks :

``` 
docker attach mydexchain
```

#### Windows 

##### 1. Stop `MyDexChain` Node Docker Container (For Data Consistency):

``` 
docker kill mydexchain
```

##### 2. Copy `%USERPROFILE%\AppData\Local\Docker\wsl\data\ext4.vhdx` to Backup Path:

##### 3. Start `MyDexChain` Docker Container on the New Docker Host :

``` 
docker run -d --rm -p 2020:2020 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
```


##### 4. Follow the Blocks :

``` 
docker attach mydexchain
```


### How to Migrate the MyDexChain Node to Another Docker Host?
Before migrating your node be sure that docker is `installed on target`.

#### Linux & MacOs

##### 1. Stop `MyDexChain` Node Docker Container:

``` 
docker kill mydexchain
```

##### 2. Copy Node Files to New Docker Host :

``` 
rsync -avzhHP --rsync-path="sudo rsync" -e "ssh -i key -o StrictHostKeyChecking=no" /var/lib/docker/volumes/mydexchain/ root@target_ip:/var/lib/docker/volumes/mydexchain/
```

##### 3. Start `MyDexChain` Docker Container on the New Host :

``` 
docker run -d --rm -p 2020:2020 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
```


##### 4. Follow the Blocks on the New Docker Host :

``` 
docker attach mydexchain
```

#### Windows

##### 1. Stop `MyDexChain` Node Docker Container:

``` 
docker kill mydexchain
```

##### 2. Copy Node Files to New Docker Host :

``` 
%USERPROFILE%\AppData\Local\Docker\wsl\data\ext4.vhdx --> to the new dockerhost
```

##### 3. Start `MyDexChain` Docker Container on the New Host :

``` 
docker run -d --rm -p 2020:2020 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
```


##### 4. Follow the Blocks on the New Docker Host :

``` 
docker attach mydexchain
```

### I am Getting Errors in Windows OS? 
Make sure `Use the WSL 2 based engine` is enabled in Docker General Settings.


### Where is the Docker Mount Volume Located in Windows OS? 
Mount folder is located under:

``` 
\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes
```

### Where is the Pyhsical Path Docker Mount Volume Located in Windows OS? 
Mount disk is located under:

``` 
%USERPROFILE%\AppData\Local\Docker\wsl\data\ext4.vhdx
```

### Help! It's not working for me!

No problem. Reach out to us by [opening an issue](https://github.com/mydexchain/mydexchain/issues/new)

## Roadmap

- We are hardly working on new features:
  - `Cloud Market Deployments`

---

[![Twitter](https://img.shields.io/twitter/follow/mydexchaintech?style=social)](https://twitter.com/mydexchaintech)
