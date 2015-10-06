# Docker Toolbox Vagrant

Using `docker-machine` to do local docker development just feels messy to me. Plus there are issues with networking that vagrant just smooths over.

## Setup Instructions

### Install Dependencies - Hardware

Ensure virtualization is enabled on your hardware. If you receive error messages during box boot like
`kernel not supported` or `enable AMD/VT-X Virtualization`, then you need to ensure your host hardware supports virtualization. (use your BIOS to enable)

### Install Dependencies - Software

The following packages are required to be downloaded and installed

- [Vagrant](https://vagrantup.com)
- [Docker Toolbox](https://https://www.docker.com/toolbox)

### Configure Your HOST

Once installation of vagrant and the Docker Toolbox is complete, you will be able to follow the following steps to finish setup:

1. Open the git bash tool installed with Docker Toolbox (or use Terminal for Mac)
2. clone this repository
5. Set your `https_proxy` and `http_proxy` environment variables for the git bash tool. (see [Set your environment variables](#set-your-environment-variables))
6. Copy the `configs/Vagrantfile` to ` ~/.vagrant.d/Vagrantfile`
7. Close and re-open the git bash tool. (Or source your `~/.bashrc`)
8. Run `vagrant plugin install vagrant-proxyconf`

### Set your environment variables

To set environment variables, you must edit your shell's profile, which can be done in several ways. With git bash shell, you can create or edit a file located at `~/.bashrc`
and include the lines below. Alternatively, if you don't know how to open the file for editing, or just want to set it and forget it.. you can type the commands into the git bash
command line tool.

Make sure that your password is urlencoded, by replacing any special characters with their urlencoded counterparts. In the example given below the users real password is `P@$$w0rd`,
but has been written using url encoded characters instead. The value of the proxy env var takes the following pattern: `http://username:password@proxyhost:proxyport`. Use the host/port values
given in the example below, and substitue the `user:password` with your own info. For help replacing special characters with their urlencoded values, paste them into the encoder at: [http://meyerweb.com/eric/tools/dencoder/]() (do not paste your whole password)

```bash
export myproxy=http://r2d2:P%40%24%24w0rd@in00pxy1.opr.statefarm.org:8000
export http_proxy=$myproxy
export https_proxy=$myproxy
export HTTPS_PROXY=$myproxy
export HTTPS_PROXY=$myproxy
```

### Vagrant instead of `docker-machine`

You can now provision any OS you wish, with any version of docker you wish, and connect to that using a private local IP address, instead of relying on `docker-machine` to do all of your `docker` server based commands. The best part is, that this machine is more easily managed and replicated, including cleanup. 

I've included a sample `Vagrantfile` at the root of this directory, so if you want, you can use this as a seed for docker development. You can choose to connect the docker client to the daemon running in vagrant by using `docker -H tcp://192.168.33.10`, or by ssh'ing into the vagrant box, and just using `sudo docker` for anything you wish. (Alternatively, you can just `sudo su -` to change to root user, and do everything without `sudo` prepended.

To get started with this Vagrantfile, just copy the `Vagrantfile` into a new directory of your choosing, and run `vagrant up`.
