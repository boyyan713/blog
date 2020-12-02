---
title: How to install Docker, Nvidia Docker and Docker Compose
date: 2020-10-11 18:12:42
tags:
 - Docker
categories: virtual environment
---

# Install Docker

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04
https://docs.docker.com/engine/install/ubuntu/ 

## Step 1 — Installing Docker
The Docker installation package available in the official Ubuntu repository may not be the latest version. To ensure we get the latest version, we’ll install Docker from the official Docker repository. To do that, we’ll add a new package source, add the GPG key from Docker to ensure the downloads are valid, and then install the package.

First, update your existing list of packages:

```bash
sudo apt update
```

Next, install a few prerequisite packages which let apt use packages over HTTPS:

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
 
Then add the GPG key for the official Docker repository to your system:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Add the Docker repository to APT sources:

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```
 
Next, update the package database with the Docker packages from the newly added repo:

```bash
sudo apt update
```
Finally, install Docker:

```bash
sudo apt install docker-ce
```

Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:

```console
(base) yanboyang713@boyang:~/Documents/docker-as-dev-environment$ sudo systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Fri 2020-10-09 15:28:29 CST; 1 day 2h ago
     Docs: https://docs.docker.com
 Main PID: 1701 (dockerd)
    Tasks: 21
   CGroup: /system.slice/docker.service
           └─1701 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Oct 09 15:28:28 boyang dockerd[1701]: time="2020-10-09T15:28:28.951155226+08:00" level=warning msg="Y
Oct 09 15:28:28 boyang dockerd[1701]: time="2020-10-09T15:28:28.951158322+08:00" level=warning msg="Y
Oct 09 15:28:28 boyang dockerd[1701]: time="2020-10-09T15:28:28.951164075+08:00" level=warning msg="Y
Oct 09 15:28:28 boyang dockerd[1701]: time="2020-10-09T15:28:28.951254105+08:00" level=info msg="Load
Oct 09 15:28:29 boyang dockerd[1701]: time="2020-10-09T15:28:29.081341203+08:00" level=info msg="Defa
Oct 09 15:28:29 boyang dockerd[1701]: time="2020-10-09T15:28:29.106837782+08:00" level=info msg="Load
Oct 09 15:28:29 boyang dockerd[1701]: time="2020-10-09T15:28:29.138925271+08:00" level=info msg="Dock
Oct 09 15:28:29 boyang dockerd[1701]: time="2020-10-09T15:28:29.139550992+08:00" level=info msg="Daem
Oct 09 15:28:29 boyang systemd[1]: Started Docker Application Container Engine.
Oct 09 15:28:29 boyang dockerd[1701]: time="2020-10-09T15:28:29.151309815+08:00" level=info msg="API
```
Installing Docker now gives you not just the Docker service (daemon) but also the docker command line utility, or the Docker client. We’ll explore how to use the docker command later in this tutorial.

## Step 2 — Executing the Docker Command Without Sudo (Optional)
By default, the docker command can only be run the root user or by a user in the docker group, which is automatically created during Docker’s installation process. If you attempt to run the docker command without prefixing it with sudo or without being in the docker group, you’ll get an output like this:

```
docker: Cannot connect to the Docker daemon. Is the docker daemon running on this host?.
See 'docker run --help'.
```
If you want to avoid typing sudo whenever you run the docker command, add your username to the docker group:

```
sudo usermod -aG docker ${USER}
```
To apply the new group membership, log out of the server and back in, or type the following:

```bash
su - ${USER}
```
You will be prompted to enter your user’s password to continue.

Confirm that your user is now added to the docker group by typing:

```console
(base) yanboyang713@boyang:~/Documents/docker-as-dev-environment$ id -nG
yanboyang713 adm cdrom sudo dip plugdev lpadmin sambashare microk8s docker

```

If you need to add a user to the docker group that you’re not logged in as, declare that username explicitly using:

```bash
sudo usermod -aG docker username
```

The rest of this article assumes you are running the docker command as a user in the docker group. If you choose not to, please prepend the commands with sudo.

Let’s explore the docker command next.

## Install Docker Compose
Docker Compose relies on Docker Engine for any meaningful work, so make sure you have Docker Engine installed either locally or remote, depending on your setup.

    On desktop systems like Docker Desktop for Mac and Windows, Docker Compose is included as part of those desktop installs.

    On Linux systems, first install the Docker Engine for your OS as described on the Get Docker page, then come back here for instructions on installing Compose on Linux systems.

    To run Compose as a non-root user, see Manage Docker as a non-root user.
### Install Steps
On Linux, you can download the Docker Compose binary from the Compose repository release page on GitHub. Follow the instructions from the link, which involve running the curl command in your terminal to download the binaries. These step-by-step instructions are also included below.

1. Run this command to download the current stable release of Docker Compose:
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
2. Apply executable permissions to the binary:
```bash
sudo chmod +x /usr/local/bin/docker-compose
```
**Note**: If the command docker-compose fails after installation, check your path. You can also create a symbolic link to /usr/bin or any other directory in your path.

For example:
```bash
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
1. Optionally, install command completion for the bash and zsh shell.
2. Test the installation.
```bash
$ docker-compose --version
docker-compose version 1.27.4, build 1110ad01

```
# Nvidia Docker (NVIDIA Container Toolkit)
![](https://cloud.githubusercontent.com/assets/3028125/12213714/5b208976-b632-11e5-8406-38d379ec46aa.png)
## Introduction
The NVIDIA Container Toolkit allows users to build and run GPU accelerated Docker containers. The toolkit includes a container runtime library and utilities to automatically configure containers to leverage NVIDIA GPUs.

Product documentation including an architecture overview, platform support, installation and usage guides can be found in the documentation repository.

## Install Nvidia Docker
### Pre-Requisites
Make sure you have installed the NVIDIA driver and Docker engine for your Linux distribution Note that you do not need to install the CUDA Toolkit on the host system, but the NVIDIA driver needs to be installed.
#### NVIDIA Drivers
Before you get started, make sure you have installed the NVIDIA driver for your Linux distribution. The recommended way to install drivers is to use the package manager for your distribution but other installer mechanisms are also available (e.g. by downloading .run installers from NVIDIA Driver Downloads).

##### On Ubuntu LTS
1. The NVIDIA driver requires that the kernel headers and development packages for the running version of the kernel be installed at the time of the driver installation, as well whenever the driver is rebuilt. For example, if your system is running kernel version 4.4.0, the 4.4.0 kernel headers and development packages must also be installed.

The kernel headers and development packages for the currently running kernel can be installed with: 

```bash
sudo apt-get install linux-headers-$(uname -r)
```
2. Ensure packages on the CUDA network repository have priority over the Canonical repository. 
```bash
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID | sed -e 's/\.//g')
$ wget https://developer.download.nvidia.com/compute/cuda/repos/$distribution/x86_64/cuda-$distribution.pin
$ sudo mv cuda-$distribution.pin /etc/apt/preferences.d/cuda-repository-pin-600
```
3. Install the CUDA repository public GPG key. Note that on Ubuntu 16.04, replace https with http in the command below. 
```bash
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/$distribution/x86_64/7fa2af80.pub
```
4. Setup the CUDA network repository.
```bash
echo "deb http://developer.download.nvidia.com/compute/cuda/repos/$distribution/x86_64 /" | sudo tee /etc/apt/sources.list.d/cuda.list
```
5. Update the APT repository cache and install the driver using the cuda-drivers meta-package. Use the --no-install-recommends option for a lean driver install without any dependencies on X packages. This is particularly useful for headless installations on cloud instances.
```bash
$ sudo apt-get update

$ sudo apt-get -y install cuda-drivers
```
##### Secure UEFI Boot

An issue that often arises when attempting to install Nvidia drivers on Linux involves a motherboard setting known as Secure UEFI Boot. In order for the driver installation to be successful it is necessary to disable this setting on most motherboards.

The procedure for carrying this out is highly specific to each particular motherboard. Hence it is difficult to provide detailed instructions that apply to a range of system configurations.

In broad terms it will be necessary to enter the BIOS as the machine boots up. This can usually be achieved by pressing the Del or F10 key. Once in the BIOS it is necessary to navigate to the section that determines boot settings. To disable Secure UEFI Boot it sometimes involves backing up and removing certain keys while in other instances it is simply a boolean setting that is easily modified.

If this feature is not disabled then in all likelihood trouble will arise subsequent to the Nvidia driver installation. Issues may occur when attempting to login in to Ubuntu after bootup. The problem is particularly difficult to resolve as it often involves an inability to load the Ubuntu GUI!

### Installing on Ubuntu and Debian
1. Setup the stable repository and the GPG key:
```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)

curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -

curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

```
**Note**
To get access to experimental features such as CUDA on WSL or the new MIG capability on A100, you may want to add the experimental branch to the repository listing:

```bash
curl -s -L https://nvidia.github.io/nvidia-container-runtime/experimental/$distribution/nvidia-container-runtime.list | sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
```
2. Install the nvidia-docker2 package (and dependencies) after updating the package listing:
```bash
sudo apt-get update

sudo apt-get install -y nvidia-docker2
```
3. Restart the Docker daemon to complete the installation after setting the default runtime:
```bash
sudo systemctl restart docker
```
4. At this point, a working setup can be tested by running a base CUDA container:
```console
(base) yanboyang713@boyang:~$ sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi
[sudo] password for yanboyang713: 
Sun Oct 11 11:24:35 2020       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 455.23.05    Driver Version: 455.23.05    CUDA Version: 11.1     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  GeForce RTX 2070    On   | 00000000:01:00.0  On |                  N/A |
| 33%   36C    P8    11W / 175W |    293MiB /  7979MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
+-----------------------------------------------------------------------------+

```
