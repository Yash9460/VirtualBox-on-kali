# VirtualBox-on-kali

## Installing VirtualBox on Kali (Host)

You can install VirtualBox on Kali Linux, allowing you to use virtual machines (VMs) inside of Kali Linux. VirtualBox is free and open source. There are a few other software such as QEMU, KVM/Xen with virt-manager.

## Preparation

Before trying to install VirtualBox, please make sure your version of Kali Linux is up-to-date, and if required, reboot the machine.

    $ sudo apt update
    $ sudo apt full-upgrade -y
    $ [ -f /var/run/reboot-required ] && sudo reboot -f
    
## Download

 The first thing we are going to do is import VirtualBox’s repository key.

    $ wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- \
    $ | gpg --dearmor \
    $ | sudo tee /usr/share/keyrings/virtualbox-archive-keyring.gpg
    
 We then move onto adding VirtualBox’s repository. We add this to a separate file, so it does not interfere with Kali Linux’s main repository. We also will be making sure to state where the keyring is at so the files can be properly signed. Our CPU architecture is amd64. You may need to alter the example below if yours is different.

 One thing to bare in mind, Kali Linux is based on Debian, so we need to use Debian’s current stable version (even though Kali Linux is a rolling distribution). At the time of writing, its “buster”:

    $ echo "deb [arch=amd64 signed-by=/usr/share/keyrings/virtualbox-archive-keyring.gpg] http://download.virtualbox.org/virtualbox/debian buster contrib" \
    $ | sudo tee /etc/apt/sources.list.d/virtualbox.list
    
 As we have altered our network repository, we need to re-build the cache.
     
    $ sudo apt update
     
 As VirtualBox has various kernel modules (e.g. vboxdrv, vboxnetflt and vboxnetadp), we need to make sure they are kept up-to-date when Kali Linux’s kernel gets updated. This can be achieved using dkms.

    $ sudo apt install -y dkms
    
## Setup

 Now its time to install VirtualBox itself (along with its Extension Pack to expand VirtualBox’s advanced features).

    $ sudo apt install -y virtualbox virtualbox-ext-pack
    
 When prompted, read and accept the license.

 You can now find VirtualBox in the menu or start it via the command line.

    $ virtualbox
    
###    Yoohoo! you have successfully installed Virtual box in Kali linux :)
