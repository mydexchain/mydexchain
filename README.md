# MyDexChain

[![Releases](https://img.shields.io/badge/version-1.0.1-orange)](#)
[![Jenkins Build](https://img.shields.io/badge/build-passing-brightgreen)](#)
[![Docker Build](https://img.shields.io/badge/docker%20build-passing-brightgreen)](#)
[![Docker Image](https://img.shields.io/docker/image-size/mydexchain/mydexchain/latest?color=green)](#)
[![Docker Pulls](https://img.shields.io/docker/pulls/mydexchain/mydexchain?color=red)](https://hub.docker.com/repository/docker/mydexchain/mydexchain)
[![LICENSE](https://img.shields.io/badge/license-Apache-lightgray)](https://github.com/mydexchain/mydexchain/blob/master/LICENSE)

MyDexChain is the newest technology for `blockchain` and can be used as a payment gateway.

- [`MyDexChain`](https://mydexchain.io) : The official web page of MyDexChain
- [`DexLife`](https://mydexchain.io): MyDexChain Masterlife Web Page
- [`Academies`](https://mydexchain.io/#/dashboards/academy): MyDexChain Trainings and Education Centers

This guide is used by dozens of product teams at MyDexChain. Have a question or comment? [Open an issue!](https://github.com/mydexchain/mydexchain/issues/new)

- [Release Notes](#public-release-notes)
- [MyDexChain Node Requirements](#wrench-system-requirements)
- [Pre-Installation Steps](#package-pre-installation-steps)
- [Usage](#computer-usage)
- [FAQ](#books-faq)
- [Roadmap](#roadmap)

## MyDexChain Consensus
![MyDexChain Consensus](myDexChain_Logos/consensus.jpg?raw=true)

## Public Release Notes
##### 2.2.1
- Added Master Tracked (Now DeFi Supported)
- Docker Socket Extention fixed

##### 1.0.1
- Fixed PostgreSQL PID Lock Problem
- Fixed Block Logs 

## :wrench: System Requirements

- MyDexChain Node Minimum Requirements: **`2 Core`** of CPU **`4GB`** of Memory and **`100GB`** of HDD
- Tested Operation Systems `Windows Server 2016 or Later` || `Centos` || `Ubuntu` || `Amazon Linux`
- At Least `5mbit` of `Internet Connection` with Port `2020` Ingress from **Your IP** Allowed

## :package: Pre-Installation Steps

:warning: MyDexChain is fully docker compatible and please follow [Windows](https://docs.docker.com/docker-for-windows/install/), [Centos](https://docs.docker.com/engine/install/centos/), [Ubuntu](https://docs.docker.com/engine/install/ubuntu/), [Amazon Linux](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html), [MAC OS](https://docs.docker.com/docker-for-mac/install/) installation steps before running MyDexChain Node. After docker installation open a command line || terminal and run command to check the docker version.

```
docker -v
```

> **Output**: Docker version 20.10.0, build 7287ab3


## :computer: Usage

##### 1. Run MyDexChain:

MyDexChain docker file is stored in dockerhub and ready for use with command: (Please check the version and use as tag rather than latest)

```
docker run -d --rm -p 2020:2020 -p 3030:3030 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
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
"http://{DockerHostIP}:2020/setMasterTracker/{pool}&{hostname}&{percent}”
```
- `pool : MasterTracker Pool Name` 
- `hostname : MasterTracker Host Name`
- `percent : MasterTracker Pool Cost Percent % range (%1-%100)`
```
"http://{DockerHostIP}:2020/setJoinPool/{poolapikey}”
```
- `poolapikey : MasterTracker PoolApiKey` 

```
"http://{DockerHostIP}:2020/setDextracker/{dexTrackerNumber}&{dexhash}”
```
- `dexTrackerNumber : DexChain Tracker Number` 
- `dexhash: DexLife Transaction Hash`
```
"http://{DockerHostIP}:2020/setAcademy/{academyContract}”
```
- `academyContract : DexChain Academy Contract` 
```
"http://{DockerHostIP}:2020/setActivist/{address}&{dexhash}”
```
- `address : DexChain Address` 
- `dexhash: Dexchain Transaction Hash`
```
"http://{DockerHostIP}:2020/setProActivist/{address}”
```
- `address : DexChain Address` 
```
"http://{DockerHostIP}:2020/setDexClouder/{address}&{contract}”
```
- `address : DexChain Address` 
- `contract : DexStore Contract Address` 
```
"http://{DockerHostIP}:2020/setNickname/{nickName}”
```
- `nickName : DexChain Tracker Nickname` 
```
“http://{DockerHostIP}:2020/isWallet/{address}”
```
- `address: Dexchain Address`
```
"http://{DockerHostIP}:2020/balanceWallet/{address}"
```
- `address: Dexchain Address`
```
"http://{DockerHostIP}:2020/balanceToken/{address}&{contract}"
```
- `address: Dexchain Address`
- `contract: DexChain Contract Address (if null please set “mydexchain”)`
```
“http://{DockerHostIP}:2020/createWallet/{password}”
```
- `password: Dexchain Address password “Please Don’t Forget it”`
```
"http://{DockerHostIP}:2020/getLastBlock/"
```
- `Last Block`
```
"http://{DockerHostIP}:2020/getTransactionByDexHash/{dexhash}"
```
- `dexhash: Dexchain Transaction Hash`
```
"http://{DockerHostIP}:2020/getTransactions/{address}&{limit}&{orderby}”
```
- `address: Dexchain Address`
- `limit: number of records`
- `orderby: ASC or DESC `
```
"http://{DockerHostIP}:2020/getTransactionByBlock/{blockid}&{limit}&{orderby}”
```
- `blockid: Block ID (hex)`
- `limit: number of records`
- `orderby: ASC or DESC `
```
"http://{DockerHostIP}:2020/getTransactionByBlockOffset/{blockid}&{limit}&{orderby}&{offset}”
```
- `blockid: Block ID (hex)`
- `limit: number of records`
- `orderby: ASC or DESC `
- `offset: skip that many rows before beginning to return rows `
```
"http://{DockerHostIP}:2020/getmyTransactionByBlock/{blockid}&{limit}&{orderby}”
```
- `blockid: Block ID (hex)`
- `limit: number of records`
- `orderby: ASC or DESC `
```
"http://{DockerHostIP}:2020/sendTransaction/{sender}&{password}&{receiver}&{amount}&{fee}&{contract}&{description}"
```
- `sender : Sender Dexchain Address`
- `password: Dexchain Address password`
- `receiver: Receiver Dexchain Address`
- `amount: Amount of XMD`
- `fee: Fee of Transaction (IN / OUT)` 
- `contract: DexChain Contract Address (if null please set “mydexchain”)`
- `description: Statements of Transaction (if null please set “null”)`
```
"http://{DockerHostIP}:2020/getSendToken/”
```
- `Token: Unique Token GUID`
```
"http://{DockerHostIP}:2020/sendTransactionV2/{sendtoken}&{sender}&{password}&{receiver}&{amount}&{fee}&{contract}&{description}"
```
- `sendtoken : Unique Token GUID`
- `sender : Sender Dexchain Address`
- `password: Dexchain Address password`
- `receiver: Receiver Dexchain Address`
- `amount: Amount of XMD`
- `fee: Fee of Transaction (IN / OUT)` 
- `contract: DexChain Contract Address (if null please set “mydexchain”)`
- `description: Statements of Transaction (if null please set “null”)`


## :books: FAQ

### How Can I Calc Fee
Sample Fee Calculation


| Transaction Amount | Fee %         | Fee Amount |
| :----------------: | :-----------: |:---------: |
|               1000 |         0.003 |     3.00   |
|              10000 |        0.0003 |    +2.70   |
|             100000 |       0.00003 |    +2.70   |
|            1000000 |      0.000003 |    +2.70   |
|           10000000 |     0.0000003 |    +2.70   |
|          100000000 |    0.00000003 |    +2.70   |
|         1000000000 |   0.000000003 |    +2.70   |
|        10000000000 |  0.0000000003 |    +2.70   |
|       100000000000 | 0.00000000003 |    +2.70   |
|                    |               |            |
|                    |               |    24.60   |


25000 myDexChain Transaction = (1000 x 0.003) + (9000 x 0.0003) + (15000 x 0.00003) = 6.150 Fee

### Standard fee distribution
- %0,1 MasterTracker Bonus
- %0,1 DexClouder Bonus
- %0,1 DexConfirmer Bonus
### Commercial fee distribution
- %0,1 DexClouder ProActivist Bonus
- %0,1 DexClouder Academy ProActivist Bonus
- %0,1 DexClouder Activist Bonus
- %0,1 DexClouder Academy Activist Bonus
- %0,1 DexClouder Beauty Bonus


### What are the DRC (Dexchain Request Contract) Types
- `DRC-4 (Academy Contract)`
- `DRC-8 (Main Contract)`
- `DRC-16 (Token)` 
- `DRC-32 (Survey, Advertisement, Announcement)`
- `DRC-64 (Internet of Things)`
- `DRC-128 (Artificial Intelligent, Big Data)`

### Where Can I Run MyDexChain Node?
You can run MyDexChain Node on
- `Amazon Web Services`
- `Azure`
- `Google Cloud`
- `Your Own Server/Desktop`


### MasterTracker requirements;
(Only vaild after 01/05/2021 purchases)
- `A minimum value of 100 Dex Trackers must participate in the MasterTracker.`
- `Each Dexlife must be attached to 1 DexTracker.`
- `MasterTracker ServiceFee range is (%1-%100)`
- `DexTracker revenues will be given hourly.`


### How Can I Update to the Latest MyDexChain Version?
Run the command on Current DockerHost:

```
service docker start
```

```
docker kill mydexchain 
docker pull mydexchain/mydexchain
docker run -d --rm -p 2020:2020 -v -p 3030:3030 mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
```


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
docker run -d --rm -p 2020:2020 -p 3030:3030 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
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
docker run -d --rm -p 2020:2020 -p 3030:3030 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
```


##### 4. Follow the Blocks :

``` 
docker attach mydexchain
```


### How to Migrate the MyDexChain Node to Another Docker Host?
:warning: Before migrating your node be sure that docker is `installed on target`.

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
docker run -d --rm -p 2020:2020 -p 3030:3030 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
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
docker run -d --rm -p 2020:2020 -p 3030:3030 -v mydexchain:/var/lib/postgresql/ --privileged --log-driver=none --name mydexchain mydexchain/mydexchain:latest
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
