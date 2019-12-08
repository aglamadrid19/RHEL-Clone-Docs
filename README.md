# RHEL-Clone-Docs
Cloning RHEL 7.7 VMs with virt-sysprep.

## Description
This Git Repository contains the steps and documentation to succesfuly clone RHEL 7 VMs using virt-sysprep.

## Links
[Virt-Sysprep Official Docs](http://libguestfs.org/virt-sysprep.1.html)

### Summary
The reason why we would use virt-sysprep (or similar tools) is to automate most of the process after we clone a Linux VM to build new server. A good example is the MAC address, everytime we provision a new Linux VM, it gets assigned a new Virtual Ethernet Adapter. This new adapter would be assigned a newly generated MAC address, and some files in our Linux VM need to be modified before we can use it. Virt-Sysprep allows us to unconfigure or reset a Linux VM configuration, and this way deploy multiple systems based on one. The use of one tool for this purpose also helps keeping standard configurations across your enviroments, which also helps keeping your IT Infrastructure compliant. 

### Notes
This Guide its based on RHEL 7.7

### WARNING
My recommendation is that you follow this document in a Test Enviroment, since Virt-Sysprep modifies files within your Linux VM Virtual Disk, and such changes could impact a production enviroment negatively.

Backup or snapshots or both, make sure any Virtual Disk you prepare with virt-sysprep its backed up.

Virt-Sysprep Official Documentantion recommends not running virt-sysprep as root. Make sure the Virtual Disk you running virt-sysprep on its owned by the user you are logged in as.

### About the Enviroment
I'm currently running RHEL 7.7 in a Virtual Box 6.0 VM which uses the Virtual Disk Image format, from a Windows 10 Host.
I would have to get involved on this also, a Debian 10 VM thats also running on my Windows 10 Host.

### About Virt-Sysprep
Virt-Sysprep its used in two primary ways. See the following commands:
```bash
virt-sysprep [--options] -d domname
virt-sysprep [--options] -a disk.img [-a disk.img ...]
```

#### Domain Name (KVM)
Specify VM domain on KVM Host. If my hypervisor was KVM, I could use the following parameters passed to `virt-sysprep` to Sysprep the Disk Image of a VM running on the same host.

I wont dive into this option since it does not apply to us. We are on Virtual Box 6.0.

#### Disk Image
Specify Disk Image to run Virt-Sysprep on. Since we can use my RHEL 7.7 Virtual Disk Image in my Debian 10 VM (Sharing a folder from my Windows 10 Host), this is the way we are going to use Virt-Sysprep.

### 
