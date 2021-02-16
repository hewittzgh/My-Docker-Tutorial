---
sort: 1
---

# Install Docker

> The Installation Tutorial is only for Ubuntu-x86-64/amd64, the official tutorial link for Ubuntu: [here](https://docs.docker.com/engine/install/ubuntu)  

> other platforms or linux distributions and architectures can check the [official website](https://docs.docker.com/engine/install) for relevant information.  

## Preparations Before Downloading

```tip
If you have ever downloaded an old version of Docker, you need to uninstall it first.  
```

```shell
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

It's OK if apt-get reports that none of these packages are installed.  

The contents of `/var/lib/docker`, including images, containers, volumes, and networks, are preserved. If you do not need to save your existing data, and want to start with a clean installation, then you need to run the following two steps.

```shell
# Step1: Uninstall the Docker Engine, CLI, and Containerd packages.
$ sudo apt-get purge docker-ce docker-ce-cli containerd.io
# Step2: Images, containers, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes.
$ sudo rm -rf /var/lib/docker
```
You must delete any edited configuration files manually.  


## Installation Methods

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

1. Set up the repository
Update the apt package index and install packages to allow apt to use a repository over HTTPS.
```shell
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```
Add Docker's official GPG key.
```shell
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.
```shell
$ sudo apt-key fingerprint 0EBFCD88
```
Output:
```shell
pub rsa4096 2017-02-22[SCEA]
9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88
uid[unknown] Docker Release (CE deb) <docker@docker.com>
sub rsa4096 2017-02-22[S]
```
Use the following command to set up the stable repository
```note
`arch=amd64` corresponds to **X86_64/amd64**  
`arch=armhf` corresponds to **armhf**  
`arch=arm64` corresponds to **arm64**  
```

    ```shell
    $ sudo add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) \
        stable"
    ```
2. Install Docker Engine  
- Method1: Update the apt package index, and install the latest version of Docker Engine and containerd.
```shell
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
- Method2: To install a specific version of Docker Engine, list the available versions in the repo, then select and install.
```shell
# Step1: List the versions available in your repo.
$ apt-cache madison docker-ce
```
Output:
```shell
  docker-ce | 5:18.09.1~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
  docker-ce | 5:18.09.0~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
  docker-ce | 18.06.1~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
  docker-ce | 18.06.0~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
  ...
```
```shell
# Step2: Install a specific version using the versioin string from the second column, for example, 5:18.09.1~3-0~ubuntu-xenial.
sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
```
- Verify: Verify that Docker Engine is installe correctly by running the hello-world image.
```shell
$ sudo docker run hello-world
```
```note
This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.
```
3. Upgrade Docker Engine
To upgrade Docker Engine, first run `sudo apt-get update`, then follow the installation instructions, choosing the new version you want to install.

## Uninstall Docker
The operation steps are the same as [Preparations Before Downloading](#preparations-before-downloading).

## Next Step : Configure Docker
```tip
Docker Engine is installed and running. The `docker` group is creared but no users are added to it. You need to use `sudo` to run Docker commands.
```
Continue to [next step](./Configure-Docker.md) to allow non-privileged users to run Docker commands and for other optional configuration steps.