# RHEL-Clone-Docs
Cloning RHEL 7.7 VMs with virt-sysprep.

## Description
This Git Repository contains the steps and documentation to succesfuly clone RHEL 7 VMs using virt-sysprep.

## Links
[Virt-Sysprep Official Docs](http://libguestfs.org/virt-sysprep.1.html)

### Summary
The reason why we would use virt-sysprep (or similar tools), is to prepare a Linux VM to become our Master Image, and that way standarize your Linux Enviroment. Lets say you were task to create a Linux Virtual Enviroment, with 10 CentOS/RHEL 7.7 Hosts (Let's say all the same, RHEL/CentOS 7.7 Minimal Server Install, with SSH Server running accepting connections on port 22).

Instead of manually install CentOS/RHEL 7.7 on each Virtual Machine, with `virt-sysprep` you will install RHEL/CentOS once, and prepare it to be deployed multiple times over your Linux Virtual Enviroment. Once we can successfully clone / deploy Linux VM this way, we can work on things like building servers automatically from a front-end (Our own Dashboard for provissioning CentOS/RHEL 7.7 VMs). Virt-Sysprep allows us to unconfigure or reset a Linux VM configuration. 

### Notes
This Guide its based on RHEL 7.7

### WARNING
My recommendation is that you follow this document in a Test Virtual Enviroment, since Virt-Sysprep modifies files within your Linux VM Virtual Disk, and such changes could impact a Production Virtual Enviroment negatively.

Backup or snapshots or both, make sure any Virtual Disk you prepare with `virt-sysprep` its backed up.

Virt-Sysprep Official Documentantion recommends not running virt-sysprep as root. Make sure the Virtual Disk you running `virt-sysprep` on, its owned by the user you are logged in as.

### About My Simple Virtual Enviroment
I'm currently running RHEL 7.7 in a Virtual Box 6.0 VM which uses the Virtual Disk Image (*.vdi) format, from a Windows 10 Host.
I would have to get involved on this also, an Elementary OS VM thats also running on my Windows 10 Host.

### About Virt-Sysprep
Virt-Sysprep its used in two primary ways. See the following commands:
```bash
virt-sysprep [--options] -d domname
virt-sysprep [--options] -a disk.img [-a disk.img ...]
```

#### Domain Name (KVM)
Specify VM domain on KVM Host. If my hypervisor was KVM, I could use the above parameters passed to `virt-sysprep` to Sysprep the Disk Image of a VM running on the same host.

I wont dive into this option since it does not apply to us. We are on Virtual Box 6.0.

#### Disk Image
Specify Disk Image to run `virt-sysprep` on. Since we can use my RHEL 7.7 Virtual Disk Image in my Elementary OS VM (Sharing a folder from my Windows 10 Host), this is the way we are going to use `virt-sysprep`.

### Install Virt-Sysprep on Elementary OS
First of all, I have to make sure all my packages are up to date. For that I'm running the following:
```bash
sudo apt update && sudo apt upgrade -y
```
Since `virt-sysprep` is one of the tools part of Libguestfs (libguestfs is a set of tools for accessing and modifying virtual machine (VM) disk images.), we install it as follows (Debian/RHEL)
```bash
sudo apt-get install libguestfs-tools  # Debian/Ubuntu
sudo yum install libguestfs-tools      # Fedora/RHEL/CentOS
```

Now that `virt-sysprep` is installed, lets list all the default options enabled by default:
```bash
virt-sysprep --list-operations
```
The list contains how is your system going to be unconfigure / reset. Ready to be deployed multiple times. But there is more we can do.

Lets reset our RHEL image. Run virt-sysprep (modify files permissions if necessery, but its not recommended to run it as root):
```bash
virt-sysprep -a rhel-7.7-vdk.vdi
```

The output would show what's going to be performed on the image (Previous default options we saw before).