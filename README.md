# Deep Dive

## Requirements

### ChefDK

ChefDK includes several utilities for creating and managing chef resources.  To install it, navigate [here](https://docs.chef.io/install_dk.html#get-package-run-installer) and complete the ___Get Package, Run Installer___ and ___Set System Ruby___ sections.

### VirtualBox / Vagrant

VirtualBox and Vagrant will provide you with a virtual machine to provision using this cookbook.  You can download VirtualBox [here](https://www.virtualbox.org/wiki/Downloads) and Vagrant [here](https://www.vagrantup.com/downloads.html).

Once those are installed, install a couple of vagrant chef plugins:

```bash
$ vagrant plugin install vagrant-berkshelf
$ vagrant plugin install vagrant-omnibus
```

This will start a VirtualBox vm using the cookbook to provision it.  Most importantly, this shares the `deep-dive` directory with the vm.  Any changes made to files within this directory are mirrored in the coupled OS.

### Vagrant

After installing `vagrant` and the chef plugins, you can start a vagrant vm by running:

```bash
$ vagrant up
Starting vm ...
Bringing machine 'default' up with 'virtualbox' provider...
    default: The Berkshelf shelf is at "/Users/user/.berkshelf/vagrant-berkshelf/shelves/berkshelf20160506-3919-1cap0ms-default"
==> default: Sharing cookbooks with VM
==> default: Importing base box 'ubuntu/xenial64'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'ubuntu/xenial64' is up to date...
...
```

Once your vm is running, you can ssh in and poke around:

```bash
$ vagrant ssh
$ ls -l
total 4
drwxr-xr-x 1 vagrant vagrant 4096 Jun 27 13:43 deep-dive
```