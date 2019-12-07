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
