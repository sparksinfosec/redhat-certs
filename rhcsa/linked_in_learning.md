# Prepare for the red hat certified system admin

## Cert Pre 1 Deploy, Configure, and manage 

### Introduction

* Breaking into system admin with Red Hat ex200 cert 
* What you should know 
    * version 9 exam 
    * Useful for linux admin with one year or more
    * Not for specific beginner 
    * Has some more beginner course suggests starting with Linux installation
    * RHEL 
    * version 9 
    * CentOS stream
    * Rocky Linux 
    * A guest running in a VIM
    * Chapter 1 will need linux on a physical machine 
    * Intel VT-x 
    * High speed internet 
    * 30-40 GB available disk space 
    * 8GB of RAM
    * With Virtual box you will want a server with GUI 
    * And want to make sure first user has root access
* About Red hat certs 
    * Deploying systems 
    * Processing files 
    * Operate running systems 
    * Automate using scripts 
* State of enterprise Linux
    * Fedora 
    * Red hat advanced server RHEL 
    * Fedora 
    * Fedora upstream 
    * REHL is based on stable versions of Fedora 
    * CentOS
    * CentOS is downstream to RHEL 
    * Free and not supported by red hat 
    * Think you should look at centos 
    * Centos Stream (between Fedora and RHEL)
    * Centos stream is the only supported now 
    * Fedora as a learning tool (not identical to RHEL)
    * Advanced experience with new tech 
    * Not an enterprise level tech 
    * CentOS stream as a learning tool 
    * Also not stable but very similar to enterprise (good for small scale projects)
    * CentOS replacements (RHEL)
    * Red hat developer subscription for individual
    * Rocky Linux 
    * AlmaLinux OS 
    * Oracle Linux

### Deploy Systems 

* Create a Bootable Enterprise linux 9 live usb drive on windows 
    * Download a linux iso image (doing rocky)
    * DVD link
    * Can make a bootable thumbdrive from it 
    * Thumb drive larger than 8 gbs 
    * Win32 disk imager 
    * Making a bootable USB with a linux image on it 
* Install enterprise linux on a physical machine 
    * Server with GUI
    * sudo hostnamectl set-hostname NEWHOSTNAME
* Virtualization on enterprise linux 
    * KVM 
    * Overcommiting virtual resources 
    * KVM provides 
        * Overcommiting of physical resources 
        * Agent on guest to communicate with hypervisor 
        * Disk I/O throttling 
        * Virtual CPU hot add
        * Nested virtualization
    * virt manager and virsh
    * Libvirt API manages 
        * Virtual CPUs 
        * VM memory 
        * Virtual storage 
        * Virtual networking 
    * KVM devices 
        * Fully virtualized 
        * Paravirtualized 
        * emulated 
        * Shared 
    * Storage resouce pools 
        * Remote shared disks 
        * Local 
    * Management tools 
        * VMM - GUI
        * Virsh - command line 
        * virtinstall
* Prepare the host for virtualization
    * sudo dnf install qemu-kvm libvirt virt-install virt-viewer virt-manager 
    * Start virtualization services 
    * for drv in qemu network nodedev nwfilter secret storage interface; do sudo systemctl start virt${drv}d{,-ro,-admin}.socket;done
    * Make sure to break these down and id what the services that are beings started (as well as the one liner itself)
    * Validate that virtualization is running 
    * virt-host-validate
    * LXC lines can be ignored 
    * Talk about the packages that were installed 
    * qemu-kvm
        * Provides the user level kvm emulator and facilitates communication between hosts and guest VMs 
    * libvirt
        * server and host side libraries for interacting with hypervisor and host systems 
    * virt-install 
        * a command line tool for installing VMs 
    * virt-viewer
        * a minimal tool for displaying a virtual machines console 
    * virt-manager
        * A graphical tool for administering VMs 
    * Mentions cock pit 
* Install Linux interactively in a guest VM
    * Bridge connection needs a interface 
    * ip addr show 
    * Make sure there is a virtbr0 interface 
    * Rocky linux the dvd iso 
    * boot iso = over the internet 
    * Boot ISO = used to install the OS from another source (can also be used to enter rescue mode)
    * Binary DVD = discs required to install and use the OS (can also be used to enter rescue mode)
    * Virt manager GUI
    * Bridged mostly pretty similar 
    * Setting up the OS in first VM
    * Setting the host name so you can tell them apart 
    * sudo hostnamectl set-hostname 
* Use kickstart files to automate installs 
    * Automate installs 
    * Used by red hat 
    * Support by red hat and ubuntu
    * Kickstart file 
        * Create partitions 
        * create users 
        * Configure network settings
        * Install software 
        * Set other configuration items 
    * File in the roots user home directory (saved there after a successful install)
    * To get you started 
    * sudo cp /root/anaconda-ks.cfg ~
    * (moving it to the users home directory)
    * sudo chown user1:user1 anaconda-ks.cfg
    * Copy it over to the main host
    * scp user@IPAddress:~/acaconda-ks.cfg ~/Downloads
    * Grab the file from the ip address in the specific dir and move it over to home downloads 
    * viewing it less 
    * -N line numbers in less 
    * # Comments 
    * Root password $6 (encoded with sha 512) Open ssl to create a new hash and insert it into the file 
    * Kickstart prerequisites 
        * Installation media 
        * ISO image or NFS server or FTP/HTTP server
        * VM disk image 
        * Kickstart file 
        * kickstart delivery method 
        * Web server, ftp server, 
        * --extra-arg="int.ks=http:IPaddress/ks.cfg"
        * Inject the kickstart file into the vr ram disk 
        * --initrd-inject=ks.cfg -extra.args="int.ks=file:/ks.cfg"
* Install linux unattended in a guest vm
    * VM installation using kickstart
    * Installed OS environment 
        * Create users
        * configure network 
        * configure disks
        * install software
    * Installation environment 
        * Kickstart file 
        * DVD ISO image 
        * hard disk image 
    * virt-install <option> 
    * sudo virt-install --name rhhost-ks --memory 2048 --disk path=/var/lib/lib/libvirt/images/rhhost-ks.qcow2,format=qcow2,size=20 
    * qcow2 format 
    * Create the disk image ahead of time 
        * sudo qemu-img create -f qcow2 -o size=10G rhhost-ks.qcow2
        * Alittle more manually but more flexible with disk options
    * Back to the virt-install command 
        * sudo virt-install --name rhhost-ks --memory 2048 --disk path=/var/lib/lib/libvirt/images/rhhost-ks.qcow2,format=qcow2,size=20 --location="$HOME/DOWNLOADS/ROCKY LINUX INSTALL ISO --initrd-inject="$HOME/DOWNLOADS/anacode file" --extra-arg"inst.ks=file:/acandona file inst.ip=dhcp inst.console=ttyS0,115200n8" --os-variant=rhel9.1 --machine=q35 --boot=uefi
    * Install many VMs with this method and modify the kickstart file as well
* Manage virtual machines
    * GUI virt manager 
    * View graph and show different stats 
    * Click on the machine and can you virtual machine in the window to manage the VM
    * VM details 
    * virsh
        * sudo virsh list
        * sudo virsh help | less
        * Subcommand type 
        * Domains 
        * sudo virsh help domains 
        * Looking at these commands and subcommand categories 
        * Taking snapshots 
        * virsh without arguments 
        * interactive mode 
        * list --all (shows all vms even if not running 
        * dominfo rhhost1 (info of the vm rhhost)
        * shutdown rhhost1 (shutdown)
        * start rhhost1 (starting the VM)
        * console rhhost1 (starting a console)
        * Control [ (to end the console)
        * autostart 
        * Start a vm automatically when the host boots us 
        * autostart rhhost1 
        * creating a clone 
        * VM has to be shut down to make a clone 
        * quit to exit interactive mode 
        * sudo virt-clone --auto-clone --original rhhost1 --name rhhost2 
        * look at the list again virsh list --all 

### System config and services 

* Understand the linux boot process 

