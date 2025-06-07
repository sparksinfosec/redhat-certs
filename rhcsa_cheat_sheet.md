# Main RHCSA cheat sheet 

* To go along with sander videos 
    * Tried to be quick and command heavy to really study and work on key areas
* Gameplan
    * work on this guide once complete: study and get it in
    * kodekloud for practice test and some additional video knowledge where needed
    * Book/cert guide to read up in a few areas if needed
    * Understanding is key don't need to know how to do everything but need to know about it and be able to find resources during exam
    * Sign up for the exam after finishing this guide and studying it a bit (asap)

## Reminders for the exam 

* *ATTENTION TO DETAIL*
    * reread 
    * make sure the names of files are exact 
    * make sure to focus in on this as the grading is automated
* Do not rely on custom configs of your system 
* set -o vi (doing this for the exam?) 
    * Get in the habit to use this on the command line (but needs to be set)
* Make sure you practice in Vanilla linux system for practice exams 
    * good prep for the exam 
    * even if you need to set config items 
* Take your time
    * no need to get fancy - one at a time and check your work
* Need to finish and then go through the exam objectives and any test you can find
* Looking at reddit post and external sources about specific things to look at 
    * Like containers and autofs 

## Common review/reminders 

* Do not expect this to be very big but reminders from rwx rob and het reviews
* \ls 
    * run without the alias version
* exec bash -l 
* man -K (search all text in all man pages)
* source ~/.bashrc (reload the bashrc file after editing confirm this command)

## Cheat Sheet 

### 3.3 Virtual terminals 

* 3.3
    * Ctrl ALT #FN
    * who or w to see which users currently are active on which terminals 
    * chvt [number]
        * running with sudo 
    * sudo chvt 3 (changes to tty)
    * Follow up 
        * Look at all the virtual terminals (default graphical one)


### 4.1 Man pages 

* man [number] command (for specific section number)
* man -a command (all section numbers for the command)
* Sections (from man man)
    1. Executable programs or shell commands 
    1. system calls (functions provided by the kernel)
    1. library calls (functions within program libraries)
    1. special files (usually found in /dev)
    1. file formats and conventions, e.g. /etc/passwd
    1. games 
    1. miscellaneous (including macro packages and conventions), e.g. man(7)
    1. System administration commands (usually only for root)
    1. Kernel routines [Non Standard]
* man -k or apropos (search mandb)
    * sudo mandb (manually trigger a rebuild)
    * filter with grep for specific sections 
        * man -k user | grep 8

### 5.1 Using I/O redirection 

* 0: stdin
* 1: stdout
* 2: stdout
* > (write a result of a command to file stdout)
* >> (append)
* 2> (stderr out >> for append)
* < (stdin fetch input of a file)
* &> (redirect stdout and stderror command &> somefile)
    * &>> (append)
* some_command > output.file 2>&1 (redirect stderr to stdout and stdout into the file)A
* some_command >> output.file 2>&1 (append)
    * order matters and alittle more perfered than &> (&> is bash only)

### 5.4 Shell Expansion

* Globbing 
    * ls * (any character)
    * ls a?* (? for one single character * any character)
    * ls [a-e]* (range of specific characters)
* Other expansion
    * brace expansion 
        * touch file{1..9} adduser {lisa,linda,anna}
    * Tilde expansion: 
        * cd ~ 
    * command substituion:
        * ls -l $(which ls)
    * variable substitution
        * echo $PATH 
* For loop brief 
    * for i in {1..10};do echo $i;done
    * for i in {one,two,three};do echo $i;done
    * for i in $(seq 1 10);do echo $i;done (passing a command)
    * for i in `seq 1 10`;do echo $i;done (older way to pass a command)

### 5.8 Tuning the bash env 

* Config files for bash 
    * /etc/profile - generic bash startup file containing all system settings that are processed in a login shell
    * /etc/bashrc - processed while opeing a subshell
    * ~/.bash_profile - user specific version of /etc/profile 
    * ~/.bashrc - user specific version of /etc/bashrc 
    * Drop in files 
        * /etc/profile.d 
    * NO talk in the videos but remember /etc/skel
        * This is what new users will get in there home dir 
* Sidebar
    * alias
        * alias del'rm -rf'
        * unlias del 
    * Variable 
        * export color=green
            * or just color=green for local
        * $color (to call)
        * local vs global with the config files


### 6.1 exporling the system hierarchy 

* Starting point fo filesystem is the root dir 
* different devices may be integrated in the filesystem by using mounts 
* /etc
    * config files
* /usr 
    * /usr/bin /usr/sbin
    * executable commands on the system
    * sbin = super user binaries 
* /var 
    * temp files, variable data files 
    * /var/log
* /tmp
    * temp files (any user can write to)
* users home directory 
* man hier (man page for file system hierarchy standard)
    * man file-hierarchy (another great source)

### 6.2/Using essential file management commands/6.3 Finding files 

* Using essential file management commands 
* Finding files 
* Examples 
    * find / -name "hosts"
    * find / -type f -size +100 M (type: f for file: size above 100MB)
    * find /etc -exec grep -l student {} \; -exec cp {} find/contents/\; 2>/dev/null 
        * -exec running on the results of the find command
        * \; closes the -exac statement 
    * find /etc -name '*' -type f | xargs grep "127.0.0.1" (* xargs takes output of find command and uses it as input to the grep command)
        * Additional information for xargs 
        * Unix command which can be used to build and execute commands from standard input 

### 6.4 Mounting filesystems 

* Essnetial for the filesystem hierarchy
* To access a device it must be connected to a dir
    * Known as mounting the device 
* mount /dev/devicename /directory 
    * mount /dev/sdb1 /mnt 
* findmnt 
    * command shows all currently mounted devices 
* lsblk 
    * devices that are not mounted as well 
* umount 
    * disconnect the mount 

### 6.5 Using Links/6.6 Archiving and compression

* Using links 
    * ln TARGET LINK_NAME 
    * ln -s TARGET LINK_NAME 
        * so the existing file you are linking to - then the link you are creating
* Archive and Compression
    * -cvf 
        * c - create an archive 
        * v - verbose 
        * f - specify the file 
    * tar -cvf archive.tar /home (create an archive)
    * tar -tvf archive.tar (show content of an archive)
    * tar -xvf archive.tar (extact to the current dir)
        * -C to switch the output PATH 
    * Compression
        * gzip (-z)
        * bzip2 (-j)
        * xz (-J)
        * tar -czvf my_archive.tar.gz /home (create a compressed archive with gzip)

### 7.1 Exploring common text tools 

* Pagers 
    * less (better)
    * more (older less functionality)
    * head and tail 
        * -n # or -# 
        * head -1 or head -n 1 
        * tail -1 or tail -n 1 
* Print file content 
    * cat 
        * -A: shows all non pritable char
        * -b: number lines
        * -s: suppresses repeated empty lines 
    * tac (opposite of cat)
* Other common tools 
    * cut: filter output 
        * cut -d : -f 1 /etc/passwd
    * sort: sort output
        * cut -d : -f 1 /etc/passwd | sort 
    * tr: translates 
        * echo hello | tr [:lower:][:upper:]
        * echo hello | tr a-z A-Z
        * echo hello | tr a-l m-z 

### 7.2 Using grep 

* ps aux | grep ssh 
    * ps aux | grep ssh | grep -v grep (eclude the grep from results -v excludes)
* grep linda * 
* grep -i linda * 
    * case insensitive
* grep -A linda /etc/passwd 
    * Before and after 
    * -A 5 -B 5 (lines before and after can also be added into same command)
* grep -R root /etc 
    * recursive grep 
    * -Rl (all files without the specific lines content)


### 7.4 awk/7.5 sed 

* Exploring awk 
    * awk -F : '{print $4}' /etc/passwd 
    * awk -F : '/linda/ {print $4}' /etc/passwd
    * awk -F : '{print $NF}' /etc/passwd (last line)
    * ps -ef | grep -i null | awk '{print $2}' | xargs kill -9
* Using sed 
    * sed -n 5p /etc/passwd 
        * print line number 5
    * sed -i s/old/new/g ~/myfile 
        * global replace 
    * sed -i -e '2d' ~/myfile (-i interactive change is written to the file)

### 8.2 Switching user with SU/8.3 performing admin task with sudo/8.4 managing sudo config 

* switching user with su
    * su - username (or su - for root)
        * prompts for target users password 
        * bad practice 
* Performing admin tasks with sudo 
    * /etc/sudoers (edited with visudo command)
        * detailed admin privileges can be assigned 
    * sudo -i (open a root shell)
        * prompts for current users pw 
* Managing sudo config 
    * /etc/sudoers file
    * member of wheel group gets full sudo access 
        * %wheel ALL=(ALL) ALL (in sudoers file)
        * usermod -aG wheel myuser (adding a user to the wheel group)
    * %wheel ALL=(ALL) NOPASSWD: ALL (careful this makes sudo not require a password dangerous)
    * Defaults timestamp_type=global,timestamp_timeout=60 (extending the cached password token for 60 minutes)
    * Providing access for specific tasks 
        * Use drop in files 
            * vim /etc/sudoers.d/linda (adding a drop in file to sudoers.d dir)
        * linda ALL=/sbin/useradd, /usr/bin/passwd (allows passwd and useradd commands for sudo)
        * %users ALL=/bin/mount /dev/sdb, /bin/umount /dev/sdb (more specific args)
        * linda ALL=/usr/bin/passwd, ! /usr/bin/passwd root (able to change passwords but not root password)

### 8.5 Using ssh to log in remotely 

* systemctl status sshd (see if service is running)
    * SSH access is enabled and allowed through firewall by default
    * Root ssh access is often denied by default 
* ssh ip_address (connect with current local user account)
* ssh user@ip_address (connect with specific user account on target system)

### 9.1 understanding the purpose of user accounts/9.2 setting user properties 

* User accounts are used to provide people or processes access to system resources 
    * processes are using system accounts
    * people are using regular user accounts
    * Both need user accounts 
* User properties 
    * Managed in /etc/passwd 
        * Name: name of the account 
        * password: secret that is used for auth, maybe disabled 
        * UID: unique ID for users
        * GID: the ID of the primary group 
        * GECOS: additional non mandatory information about the user 
        * Home Directory: the env where users create personal files 
        * shell: the program that will be started after successful authentication
            * /bin/bash (for normal login)
            * /sbin/nologin (no login shell to disallow login)

### 9.3 Creating and managing users/9.4 defining user default settings

* Creating and managing users 
    * useradd: create user accounts 
    * usermod: modify user accounts
    * userdel: delete user accounts
    * passwd: set password 
    * --help 
* Defining user default settings 
    * Manage user default settings
        * useradd -D to specify default settings 
        * settings /etc/default/useradd apply to useradd only 
        * Default settings in /etc/login.defs
        * files in /etc/skel are created to user home dir upon creation
    * /etc/login.defs 
        * important options for user defaults 
        * PASS_MAX_DAYS 
    * /etc/skel 
        * files that are copied over to home dir on user creation

### 9.5 Limiting user access 

* Limit access 
    * user accounts can be temporarily locked 
        * usermod -L anna (lock user account anna)
        * usermod -U anna (unlock user account anna)
    * User accounts can be set to expire also
        * usermod -e 2032-01-01 bill (set bill user account to expire on 01-01-2032)
    * usermod -s /sbin/nologin myapp (set login shell for user myapp to nologin)
    * /etc/shadow
        * !! in password means never been set 
        * ! in front of the hash means it is locked 


### 9.6 Managing group membership/9.7 creating and managing groups

* Group membership 
    * each user must be a member of at least one group
    * Primary group members managed through /etc/passwd
    * user primary group becomes group-owner if a user creates a file
    * secondary groups can be defined as well
        * secondary group membership managed through /etc/groups
        * temp set primary group member using newgrp
        * us id to see which groups a user is a member of
* Creating and managing groups 
    * groupadd (to add groups)
    * groupdel (delete groups)
    * groupmod (modify groups)
    * lid -g groupname (list all users that are a member of a specific group

### 9.8 Setting password propteries 
    
* Encrypted password are stored in /etc/shadow
    * 3 pieces of information
        * hashing algo
        * random salt
        * encrypted hash of the user password
* Manage password settings
    * basic password requirements are set in /etc/login.defs
    * chage or passwd (run as root)
        * to change password settings for current users)
        * chage bob
        * chage -l bob (show set parameters)
        * passwd can do the same (--help)

### 10.2 Changing file ownership/10.3 Understanding basic permissions

* ugo (user-owner, group-owner, other)
* Changing file ownership
    * chown user[:group] file (set user-ownership optional group ownership)
    * chgrp group file (to set group ownership)
    * chown lisa newfile (change user ownership)
    * chown linda:sales newfiles/ (set user and group ownership)
    * chgrp wheel newfiles/ (change group owner)
    * chown :sales newfiles/ (change ownership group with chown)
* Understanding basic permissions 
    * read, write, execute 
    * Different meaning for files and directories 
        * Files 
            * read: open a file 
            * write: allow to modify the content of a file 
            * execute: allows you to run the file 
        * Directories
            * read: list files in a dir 
            * write: allows you to create or delete files
            * execute: allows you to cd and go into a directory 
    * Octals 
        * read: 4
        * write: 2 
        * execute: 1

### 10.5 Configuring shared directories/10.6 apoplying default permissions 

* Set group ID and sticky bit 
    * permission ensures that all files created in the shared group dir are group owned by the group owner of the dir 
    * Sticky bit (ensures only the user who is the owner of the file, or dir is allowed to delete the file)
    * chmod g+s (will apply SGID to the dir)
    * chmod +t mydir (assigns sticky bit to the directory)
    * Absolute mode (chmod 3770 mydir assigns SGID and sticky bit)
* Special permissions 
    * SUID has a numeric value of 4
    * SGID has a numeric value of 2 
    * Sticky bit has a numeric value of 1 
    * Sticky bit shows a T where execute permissions for others is
        * t indicates sticky bit aas well as execute (T indicates that only sticky bit is set)
    * SGID shows as an s at the position where you normally find the group execute permissions 
        * s indicates both SGID and execute are set 
        * S means only SGID is set 
    * SUID shows as an s on user permissions (execute)
        * s means both SUID and execute are set 
        * S means only SUID is set 
* Umask 
    * umask is a shell setting that subtracts the umask from default permissions 
    * default is set in /etc/bashrc 
    * set user-specific overrides in ~/.bashrc 
    * Default permission for files are 666
    * Default permission for dirs is 777
    * . .bashrc (source command)

### 11.3 Understanding NIC naming/11.4 Defining hostnames and host name resolution

* Understanding NIC naming 
    * device names 
        * IP address config needs to be connected to a specific network device 
        * ip link show (to see current devices)
        * ip addr show (to check their configs)
        * lo device for internal networking 
    * BIO device name 
        * classical naming is using device names like eth0, eth1 and so on
        * BIOS naming is based on hardware properties to give more specific information
            * em[1-N] - embedded NICS
            * eno[nn] - embedded NICS
            * p<slot>p<port> - for NICS on the PCI bus
* Defining host names and host name resolution
    * hostnamctl set-hostname
    * hostname is written to /etc/hosts
        * 10.0.0.11 server2.example.com server2 (IP, FQDN, shortname)
    * /etc/resolv.conf (contains DNS client config)
    * The order of hostname resolution is determined through /etc/nsswitch.conf

### 11.5 Analyzing network config 

* IP command 
    * replaces ifconfig (do not use)
    * ip addr (to manage address properties)
        * ip addr add dev ens33 10.0.0.10/24
    * ip link (to show link properties)
        * ip -s link 
    * ip route(to manage route properties)
        * ip route show
        * ip route add default via 10.0.0.1
    * THESE are NOT persistent (NETWORK MANAGER TO make persistent)

### 11.6 Understanding Network manager 

* Networkmanager is the systemd service that manages network config 
    * config is stored in files in /etc/NetworkManager/system-connections
        * Legacy files in /etc/sysconfig/network-scripts (still supported but deprecated)
    * Different apps are available to interface with networkmanager 
        * nmcli (powerful command lin utility)
        * nmtui offers a convenient text user interface
* Connection and devices 
    * Devices are network ints 
    * Connections are collections of config settings for a device, stored in the config file in /etc/NetworkManager/system-connection
    * ONe one connection can be active for a device 
* NetworkManager permissions 
    * Permissions to modify settings in network manager are applied through dbus 
    * non privileged users that are logged in on the console can change network settings 
    * non privileged users that are logged in through ssh cannot
    * nmcli general permissions for an overview of current permissions
        * nmcli general permission (command for permissions)

### 11.7/11.8 Managing persistent network config with nmcli and nmtui 

* NMCLI
    * DO NOT USE on exam
    * Tab completion
    * nmcli con show (show current connections)
    * nmcli dev status (shows current network devices)
    * nmcli con add con-name mynewconnection ifname ens33 ipv4.addresses 10.0.0.10/24 ipv4.gateway 10.0.0.1 ipv4.method manual type ethernet (adding a new connection)
    * nmcli con up mynewconnection (activate the new connection)
    * nmcli con
        * nmcli con show mynewconnection (show all connection settings)
        * nmcli con mod (modify connection settings: use tab completion)
        * nmcli con reload (will reload the modified connection)
    * ipv4.method 
        * use ipv4.method manual (on connections that do not use DHCP)
        * Without this setting, a DHCP server will be contacted even if static config has been set 
* NMTUI
    * USE THIS FOR THE EXAM
    * nmtui (to run it)
        * options 
            * edit a connection
            * activate a connection
            * change hostname 


### 11.9 troublshooting networking 

* Verify connectivity 
    * ping to verify connectivity 
        * ping -c 4 myserver (send 4 packets and then stop)
        * ping6 2001::210 (uses ping6)
    * When using ping6 on link local addresses, you must include the NIC name in the command 
        * ping6 ff02::1%ens33
* Troublshoot routing 
    * ip route (print the routing table)
    * ip -6 route (shows IPv6 routing table)
    * tracepath example.com (shows the entire networking path)
    * tracepath6 example.com (does the same for IPv6 path if existing)
    * ss (used to analyze socket stats)
        * ss -tu (TCP and UDP etablished connections)
        * ss -tuna 
        * ss -tunap (names, additional information, ports)
        * ss -tulp (het tanis)

### 12.1 Understanding RPM packages 

* Managing RPM packages 
    * rpm command (for some package management tasks)
        * rpm -qa (shows all packages that are currently installed)
        * rpm -qf /usr/bin/ls (shows which package file was installed from)
        * rpm -ql (lists files installed from a package)
        * rpm -q --scripts (shows scripts executed while installing the package)
        * rpm -q --changelog (shows the change log for a package)
        * -q (query installed packages)
        * -p (package query an uninstalled package file)
    * Extracting RPM packages 
        * Extracting but not installing 
        * rpm2cpio mypackage-1.0.rpm | cpio -tv (show the contents of the package)
        * rpm2cpio mypackage-1.0.rpm | cpio -idmv (extracts package contents to the current dir)

### 12.2 Setting up repo access 

* Repos are a collection of RPM package files with an index that contains repo contents
* Repos through subscription manager, red hat satellite, online source, can also be local
* Manually Configuring repo access
    * dnf config-manager -enable repo_name (to add repo access)
    * Third part repos can be added using repo files in /etc/yum.repo.d or using dnf config-manager
    * dnf config-manager --add-repo="file:///repo/AppStream"
    * Or create the file in /etc/yum.repos.d
        * create AppStream.repo file in the dir 
        * [AppStream]
        * name=AppStream
        * baseurl=file:///repo/AppStream
        * gpgcheck=0

### Managing packages with dnf 

* Manage packages with dnf 
    * dnf list 'selinux*' (* Shows installed and available packages matching the search)
    * dnf search seinfo 
    * dnf search all selinux (be used to match names and description information)
    * dnf provides */Containerfile (* Find the packages providing the given option)
    * dnf install (install packages as well as dependencies)
    * dnf remove (removes packages as well as package dependencies (potentially dangerous))
    * dnf update (compares current package version with the package version listed in the repo and updates if necessary)
    * dnf update kernel (will install the new kernel and keep old as a backup)

### 12.4 Using dnf groups/12.5 exploring modules and application streams 

* Understanding groups 
    * dnf group is just a collection of packages 
    * regular group and env group 
    * env group is used to install a specific usage pattern, and may consist of packages and groups 
    * dnf group list (see a list of groups)
        * Some groups are normally only installed thru env groups and not separately, and will not show in dnf group list 
    * dnf group list hidden (see all groups)
    * dnf group info <groupname> (see packages within a group)
    * Packages are marked as mandatory, default, or optional 
    * while using dnf group install (only mandatory and default packages are installed)
    * dnf group install --with-optional (install optional packages also)
    * Group names often contain spaces so need double quotes 
* Exploring modules and application streams 
    * dnf uses modularity, meaning that different versions of the same package can be maintained in the same repo 
        * Useful for packages that have a lifetime that differs from core OS packages
    * RHEL 9 offers 2 main repos 
        * BaseOS has core OS content for RHEL 
            * packages share the OS lifecycle 
        * Appstream is used for packages that don't have the same lifecycle as RHEL 
    * Understanding AppStream Packages 
        * Appstream packages are offered as individual packages or as modules 
        * RHEL 9.0 no modules are provided by default, may be offered separately later
        * Modules, different streams can be offered where each package version has its own stream
        * Module profiles provide common installation patterns such as server, client, and more


### 12.6 managing dnf update and history

* Logs and trace history of everything that has happened
* /var/log/dnf.rpm.log (all transactions that dnf performed are logged here)
* dnf history (summary of all installations and removal transactions)
* dnf history undo 2 (undo might not be easy (inversion conflicts))

### 12.7 Using subsciption-manager

* Understanding subscription manager
    * Register the system with red hat and attach a subscription (otherwise no repos)
    * subscription-manager register (to register)
        * prompts for username 
    * subscription-manager attach --auto (need to attach a subscription)
    * subscription-manager unregister (to unregister a system)
    * dnf repolist (see the active repos)
* Understanding entitlement certificates 
    * After attaching subscription to a system, entitlment certs are created 
    * /etc/pki/product (indicates the installed red hat products)
    * /etc/pki/consumer (identifies the red hat account for registration)
    * /etc/pki/entitlement (indicates which subscription is attached)
    * rct command (check current entitlements)
        * rct cat-cert /etc/pki/entitlments

### 13.1 Exploring jobs and processes/13.2 Managing shell jobs 

* Understanding jobs and processes 
    * All task are started as process (Processes have a PID)
    * Common process management task scheduling priority and sending signals 
    * Some processes start multiple threads, individual threads cannot be managed 
    * Tasks that are started from a shell can be managed as jobs 
    * Shell jobs can be started in the foreground or background 
    * Processes require admin access (shell jobs are based on users and shells)
* Managing shell jobs 
    * command & (to start a job in the background
    * Move a job to the background 
        * stop it using Ctrl-z 
        * bg (to background the job)
    * jobs (for complete overview of running jobs)
    * fg [n] (to move number or last job to foreground)

### 13.3 Understanding process states 

* Understanding process states 
    * New process started (forked), scheduled and then it will get a runnable state (R)
    * In this state it will wait in the q to be scheduled
    * Runnable processes will get a time slice, which allows them to get a running state, in either kernel or user space 
    * Runnable processes can get preempted or rescheduled
        * In this case, they will return to a runnable state and wait in the q for a new time slice 
        * Runnable process can be stopped (Ctrl-z) and will show as TASK_STOPPED (T)
            * After being stopped it can recieve another signal to resume and return to a runnable state
* Understanding Waiting process states 
    * Waiting processes can have different flags
        * TASK_INTERRUPTIBLE (S): The process is waiting for hardware request, system resources access or signal 
        * TASK_UNITERRUPTIBLE (D): the process is waiting but does not respond to signals
        * TASK_KILLABLE (K): the process is waiting but may be killed
        * TASK_REPORT_IDEL (I): Used for kernel threads this process will not count for the load average 
* Understanding exit states 
    * When a process exits, briefly enter the EXIT_ZOMBIE (Z) state
    * Signals to the parent process that it exits and all resources except for the PID are released
    * Next stage the process will enter EXIT_DEAD (X) state
    * In this state it will be reaped and all remaining processes are cleaned up 
* Understanding Zombies 
    * A process becomes a zombie when it has completed it task
    * But parent process has not collected its execution status
    * Most important disadvantage is that zombie occupy a PID 
    * To get rid of the zombie, the parent process must collect the child execution status 
        * Send SIGNCHILD to the parent to ask the parent to reap the zombie
        * Kill the parent process 
        * When the parent is killed, the zombie becomes an orphan and will be adopted by the init process 

### 13.4 Observing process information with PS 

* Using ps 
    * ps command has two different dialects: BSD and system V 
    * Therefore ps -L and ps L are two different commands
    * ps aux (for an overview of all processes)
    * ps -fax (show hierarchical relationship between processes)
    * ps -fU linda (shows all processes owned by user linda)
    * ps -f --forest -C sshd (shows a process tree for a specific process/command)
    * ps L (show format specifiers)
    * ps -eo pid,ppid,user,cmd (use some of these specifiers to show a list of processes)


### 13.5 monitoring memory use/13.6 overserving CPU load/13.7 monitoring system activity with top

* Understanding memory use 
    * free -m (details about current memeory usage
    * /proc/meminfo (additional memory information)
    * drawing additional info to note
        * RAM - cache and application memory (used vs unused active vs inactive)
        * Dropped cached to free up ram (also swap space)
        * Write cache (write cache buffer is used committed to disk by pdflush kernel thread, not immediate)
* Checking CPU load 
    * uptime
    * CPU load is expressed as the average number of runnable processes over the last 1, 5, and 15 minutes
    * lscpu (check the number of cpus on the system - load should not exceed the number of CPU cores on the system)
    * Schedule processes in linux 
        * CPU - kernel allocates task to CPU - kernel scheduler - enter q - nice values for who enters scheduler
        * timslice and once over it will enter the q again (out of the cpu)
* Using top 
    * top (to start the dashboard)
        * f (to show the select from available display fields)
        * M (to filter memory usage)
        * W (save new display settings)

### 14.1 Using signals to manage process state

* Using signals 
    * A signal allows the OS to interrupt a process from s/w and ask it to do something
    * Interrupts are comarable to signals but generated from hardware 
    * man 7 signals (limited amount of signals can be used and are documented in this man page)
    * Standard signals 
        * SIGKILL (ordinary kill signal)
        * SIGTERM (force)
    * kill -9 (regular kill allows it to quit gracefully force maybe harmful)
    * killall dd (kill all dd commands/kill by name)
    * Zombie demo
        * ps aux | grep defunct (show all zombies)
        * kill -SIGCHLD processID (for the parent ID)
        * kill parent_processID (then you can kill the parent process after adopted by systemd)

### 14.2 managing process priority 

* Cgroups (not really in rhcsa)
* Managing nice 
    * nice and renice commands
    * values -20 up to 19 (negative nice values are increased priority, positive value are decreased priority)
    * Users can set their own processes to a lower priority, in increase need root
    * nice -n 19 dd if=/dev/zero of=/dev/null
    * Info about /sys dir in demo 
        * /sys/cpu/devices (setting to 0 or 1 good FYI)

### 14.3 using tuned profiles

* System tuning 
    * /proc/sys directory (different files in /proc/sys dir contain the current settings as its values)
    * Change current values by echoing a new value into the file 
        * cat /proc/sys/vm/swappiness
        * echo 40 > /proc/sys/vm/swappiness 
    * To make these changes persistent, write them to a file in /etc/sysctl.d 
        * cat >> swappiness.conf << EOF (starts a cat session that looks to end with EOF)
            * vm.swappiness = 40
            * EOF 
    * sysctl -a (all values)
    * sysctl vm.swappiness (look at specific variable)
* Understanding tuned
    * tuned-adm list (shows all current profiles)
    * tuned-adm profile virtual-guest (set another profile as default)
    * each profile contains a file with the name tuned.conf, has a wide range of performance related settings
    * reapply_sysctl = 1 (parameter in /etc/tuned/tuned-main.conf ensures that sysctl parameters win)
    * tuned-adm --help
* Creating custom profiles 
    * /etc/tuned (where custom profiles are stored)
    * need a tuned.conf in the corresponding dir and will be automatically picked up 
* Demo: using tuned
    * sudo dnf install -y tuned
    * systemctl enable --now tuned
    * tuned-adm list
    * echo vm.swappiness = 33 > /etc/sysctl.d/swappiness.conf
    * sysctl -p /etc/sysctl.d/swappiness.conf
    * sysctl -a | grep swappiness
    * mkdir /etc/tuned/myprofile
    * cat >> /etc/tuned/myprofile/tuned.conf << EOF
        * [sysctl]
        * vm.swappiness = 66
        * EOF
    * tuned-adm profile myprofile
    * tuned-adm profile
    * sysctl -a | grep swappiness
    * cat /etc/tuned/tuned-main.conf

### 14.4 managing user sessions and processes 

* ps -u username (show processes owned by a specific user)
* pkill -u username (to remove processes owned by a specific user)
* Using loginctl 
    * loginctl is a part of systemd, and manages users and sessions 
    * loginctl list-users
    * loginctl list-sessions
    * loginctl user-status <UID> (shows a tree of processes currently open by this user)
    * loginctl terminate-sessions (use to stop/drop session)
    * login terminate-user (used to stop user)

### 15.1 exploring system units/15.2 managing systemd services 

* Understanding systemd units 
    * First process after loading the kernel and manages everything
    * Used for starting services like ssh and web server
    * Items tarted by systemd are referred to as units
    * systemctl is the main management tool for systemd 
    * systemctl -t help (overview of all types of units that are available)
    * Understanding unit types 
        * service units are used to start processes 
        * socket units (monitor activity on a port and start the corresponding service unit when needed)
        * timer units (are used to start services periodically)
        * path units (can start service units when activity is detected in the file system)
        * mount units (are used to mount file systems)
    * Service units are often used to start daemon processes 
    * type=oneshot can be used to start any command through systemd 
* Checking out systemd units 
    * systemctl has great tab completetion
    * systemctl -t help (available unit types)
    * systemctl list-units 
    * systemctl list-units -t timer 
    * systemctl list-unit-files
* Managing systemd services 
    * systemctl status sshd
        * the active: line in the output shows the current status
        * the loaded: line in the output shows which config is loaded, whether the unit is enabled for auto starting 
    * Systemd unit management tasks 
        * systemctl status (get current status)
        * systemctl start (will start a unit that is not currently active)
        * systemctl stop (will stop the unit)
        * systemctl enable [--now] - used to flag unit for automatic starting upon system start
        * systemctl disable [--now] - used to flag the unit to be no longer auto started 
        * systemctl reload (will reload the unit config without restarting the unit)
        * systemctl restart (restarts the unit after which the process it manages will get a new PID)

### 15.3 Modifying systemd service config 

* systemctl edit unit.service (to edit unit files)
* systemctl show (to show available parameters 
* systemctl reload (may be required to reload the unit)
* systemctl cat httpd.service (cat the config file shows all config even if spread over multiple files
* systemctl show httpd.service (show tunables for the config file)
* systemctl edit httpd.service (may bring up nano)
    * export EDITOR=/usr/bin/vim
* Edit of the config file 
    * [Service]
    * Restart=always
    * RestartSec=5s 
    * save changes
    * Cat the config file again to see the override 
        * /etc/systemd/system/httpd.service.d/override.conf
* If not picked up automcatically you can always use systemctl daemon-reload 
    * Old school and shouldn't have to but helpful 
* systemctl restart httpd 

### 15.4 managing unit dependencies/15.5 masking services 

* Understanding unit dependencies '
    * automatic triggers - systemd units normally depend on other units 
    * systemctl list-dependencies (complete overview of all currently loaded units and their dependencies)
    * systemctt list-denependencies UNIT (to see dependencies for specific units)
* Masking services 
    * systemctl mask (to prevent admins from accidentally starting units)
        * some units cannot work simultaneously on the same system)
    * systemctl unmask (to remove unit mask)
    * creates a symbolic link to /dev/null (can not be started when masked)

### 16.2 scheduling tasks with systemd timer 

* Understanding system timers 
    * systemd has unit.timer files that go together with unit.service files to schedule services 
    * systemd timers should be enabled/started and NOT the service units 
    * systemctl list-units -t timer (see timers)
    * systemctl list-unit-files logrotate.* 
    * systemctl status logrotate.service 
    * systemctl status logrotate.timer
    * /etc/systemd/system 
        * adding a service and timer file here
    * Timer activation
        * OnCalendar option uses a rich language 
        * OnCalendar=*:00/10 (* runs every 10 minutes)
        * OnCalendar=2023-*-* 9:9,19,29:30 (run the service everyday in 2023 at 9:09:30, 9:19:30, and 9:29:30
        * OnUnitActivateSec (to start the unit at a specific time)
        * OnBootSec or OnStartupSec (to start unit at specific time after booting)
        * man 7 systemd-time
* See demo
* watch -ls -l /tmp/myfile.txt (way to repeat a command)

### 16.3 scheduling task with cron 

* Cron is an onlder UNIX scheduling option
* crond (daemon that check its config to run cron jobs periodically)
* Using cron
    * cron service checks it config every minute 
    * /etc/crontab (main managed config file)
    * /etc/cron.d/ (used for drop in files)
    * /etc/cron.{hourly,daily,weekly,monthly} (used as drop ins for script that need to be scheduled on a regular basis)
        * make sure these script have the execute bit set 
    * users specific cron jobs can be created using crontab -e 
    * crontab -e (create users specific cron jobs)
* Understanding crong time specification
    * minute, hour, day of month, month, day of the week 
    * 0 * * dec 1-5 (will run cron job every monday thru friday on minute 0 in Dec.)
    * /etc/crontab (has nice syntax examples)
    * do not edit /etc/crontab, put in drop in files at /etc/cron.d instead

### 16.4 understanding anacron/16.5 using at

* Understanding anacron
    * service behind cron that ensures that jobs are executed on a regular basis, but not at a specific time
    * /etc/cron.{hourly,daily,weekly,monthly} (takes care of the jobs in these dirs)
    * /etc/anacrontab (config)
    * want a task to run everyday but do not care when (use systemd timers instead)
* Scheduling derred user jobs 
    * atd service must be running
    * at <time> (schedule a job)
        * type one or more job specification in the at interactive shell 
        * ctrl-d to close this shell 
    * atq (for a list of jobs currently scheduled 
    * atrm (to remove jobs from the list 
    * Demo
        * at teatime 
            * touch /tmp/teatime 
            * ctrl-d close the shell 
            * see the job with atq
            * should run the touch command at 4pm (team time)

### 16.6 managing temp files 

* Understanding tmp files 
    * systemd-tmpfiles is started while booting, manages temp files and dirs 
    * Will create and delete tmp files automatically, according to the conf files in the following locations
        * /usr/lib/tmpfiles.d (rpm package files)
        * /etc/tmpfiles.d (custom config)
        * /run/tmpfiles.d (for system generated config)
    * Understanding systemd-tmpfiles 
        * systemd-tmpfiles (works with related services to manage temp files)
        * systemd-tmpfiles-setup.service (creates and removes temp files according to the config)
        * systemd-tmpfiles-clean.timer (calls the systemd-tmpfiles-clean.service to remove temp files)
            * by default 15 minutes after booting
            * and also on a daily basis
* Managing temp files 
    * man tmpfiles.d (provides detailed information and examples)
    * see demo

### 17.1 RHEL logging options

* Understanding logging 
    * systemd-journald (recieves log messages from different locations)
        * Kernel 
        * Early boot procedure
        * syslog events 
        * standard output and error from daemons
        * non persistent by default 
    * rsyslog service reads syslogs messages and write them to different locations
        * files in /var/log
        * according to output modules
    * Services may also write to /var/log 

### 17.2 using systemd-journald

* Viewing systemd journal messages 
    * systemctl status name.unit (provides easy access to the last messages that have been logged for specific device)
    * journalctl (print entire journal)
    * journalctl -p err (shows only messages with a priority error and higher)
    * journalctl -f (shows the last 10 lines and adds new messages while they are added)
    * journalctl -u sshd.service (shows messages for sshd service only)
    * journalctl --since "-1 hour";journalctl --since today (allows time specification)
    * journalctl -o verbose (add verbose messages)
    * Viewing boot logs 
        * journalctl -b (show current boot logs)
        * journalctl -xb (adds explanation text to the boot log messages)
        * journalctl --list-boots (shows all boots that have been logged (on persistent journal only))
        * journalctl -b 3 (show messages from the third boot log only)

### 17.3 Preserving the systemd journal

* systemd journal settings are in /etc/systemd/journal.conf
* storage=auto (ensures that persistent storage is happening automatically after creating the dir /var/log/journal)
* Other options are 
    * persistent: stores journals in /var/log/journal
    * volatile: stores journals in the temp /run/log/journal directory
    * none: does not use any storage for the journal at all 
* /etc/rsyslog.conf
* logger (command to write messages to rsyslog manually)
* /var/log (log files are normally in this dir)

### 17.5 using logrotate

* Understanding logrotate
    * /etc/logrotate.conf and /etc/logrotate.d (log rotation config files)
    * Look at demo 
* Look at lab for this lesson

### 18.1 Understanding disk layout 

* Disk allocation
    * Storing all your data on a disk need a partition
    * Two partitions 
        * MBR (older) master boot record 
        * GPT (Newer) GUID partition table
    * MBR
        * alittle more complicated (sector on disk)
        * No more than 4 partitions (64 bytes)
        * Small partition on /boot
        * If you need more than 4 partition creating an extended partition (fills rest of the disk)
            * Within the extended partition you can create logical partitions (allows for more than 4 essentially)
    * GPT 
        * Can have up to 128 partitions no need for extended partitions 


### 18.2 Exploring linux storage options/18.3 understanding GPT and MBR partitions 

* 3 Important systems for storage 
* Linux storage options 
    * patitions
        * used to allocate dedicated storage to a specific type of data
    * LVM (logical volume manager) logical volumes 
        * used as default installation of RHEL (adds flexibility to storage (resize, snapshots, and more)
    * Stratis 
        * next gen volume managing filesystem that uses thin provisioning by default 
        * Implemented in user space, which makes API access possible 
* Linux Block devices
    * lsblk (get an overview of current existing devices)
    * according to the driver that is used different block devices can be used 
        * /dev/sdx (common for SCSI and SATA disk)
        * /dev/vdx (is used in KVM virtual machine)
        * /dev/nvmexny (used for NVME device)
    * Understanding patition numbering 
        * on sd and vd devices, partitions are numbered in order 
            * /dev/sda2 (second partition on the first hard disk)
            * /dev/sdb1 (first partition on the second hard disk)
        * on nvme devices, partitions names are appended to the device
            * /dev/nvme0n1p1 (first partition on the first hard disk)
            * /dev/nvme0n3p2 (second partition on the third hard disk)
        * use lsblk to avoid confusion (reads the kernel partition table in /proc/partitions)
* Understanding GPT and MBR partitions 
    * Master Boot Record (MBR)
        * Part of the 1981 PC specifications - 512 bytes to store boot information - 64 bytes to store partitions
        * Room for 4 partitions only with a max size of 2 TiB (to use more extended and logical partitions are needed)
    * GUID partition tables (GPT) 
        * new partition table - more space to store partitions (overcome MBR limits)
        * 128 partitions max 

### 18.4 creating partitions with fdisk 

* Partitioning tools 
    * fdisk offers easy to advanced features (been around forever)
        * reworked to support MBR and GPT partitions 
        * on new disks, create GPT partitions using g 
    * gdisk was introduced to offer gpt support 
        * creates GPT partitions by default 
    * parted was introduced to make partitioning easier 
        * can be scripted easily (advanced features abit hidden)
* Understanding partition types 
    * partition types were important in the past currently partitions will work if the wrong partition type is set 
    * Low level ID of the OS and boot manager using specific partitions 
    * fdisk, use t to change the partition type 
    * Use aliases to set the appropriate partition type 
        * linux: standard linux 
        * swap: linux swap
        * uefi: uefi boot
        * lvm: logical volume manager 
        * Others available use l for a list 

### 18.5 creating and mount filesystems 

* Understanding linux filesystems
    * XFS is the default filesystem
        * fast and scaleable (Copy on write CoW - size increased not decreased)
    * Ext4 was default in RHEL 6 and is still used 
        * backward compatible to ext2 (OG linux filesystem) - jornal to guarantee data integrity
        * Size can be increased and descreased 
    * vfat offers multi os support (used for shared devices)
    * btrfs is new and advanced filesystem - not installed by default on RHEL
* Creating filesystems 
    * mkfs.
        * mkfs.xfs (xfs filesystem)
        * mkfs.ext4 (creates an ext4 filesystem)
        * mkfs.vfat (creates a vfat filesystem)
        * mkfs. TAB TAB great auto completion (make sure to specify the filesystem type)
* Mounting filesystem
    * After making the filesystem you can mount it in runtime using mount command 
    * Mount filesystem to a dir to make it accessible 
    * mount /dev/vdb1 /mnt 
    * umount to diconnect a device 
    * lsof /mnt (if you get an error about open files when unmounting with umount)
    * mount (command shows all mounted filesystem, including admin kernel mounts)
    * findmnt (command shows which filesystems is mounted where in the dir structure)

### 18.6 Mounting a partition through /etc/fstab 18.7 using UUID and labels 

* Understanding /etc/fstab
    * /etc/fstab is the main config file to persistently mount partitions
    * /dev/sdb1 /data ext4 defaults 0 0 (partition, mount point, filesystem, defaults, 0, 0)
    * /etc/fstab content is used to generate systemd mounts by the systemd-fstab-generator utility 
    * recommended to use systemctl daemon-reload after editing /etc/fstab
    * Avoiding problem while booting 
        * Making an error in fstab is bad 
        * error in /etc/fstab, you system will drop a troubleshooting shell while booting 
        * after adding lines to /etc/fstab use mount -a (all that has not been mounted yet will be)
        * findmnt --verify (verify syntax)
* Labels and UUIDs
    * Block devices may change (persistent naming(
    * UUID: auto generated for each device that contains a filesystem or anything similar 
    * Label: while creating the filesystem -L can be used to give it a label/arbitrary name
    * unique device names are created in /dev/disk/*
    * Managing persistent naming attributes 
        * blkid (shows all devices with their naming attributes)
        * tune2fs -L (use to set a label on an ext filesystem)
        * xfs_admin -L (used to set a label on an XFS filesystem
        * mkfs.* -L (used to set a label while creating the fileysystem)
    * blkid | awk '/sda/ {print $2}' (should get the UUID and can be put into /etc/fstab)
    * UUID=" " (quotes optional - instead of specific device/partition name in etc/fstab)

### 18.8 defining systemd mounts/18.9 creating a swap partition

* Systemd mounts 
    * lines in /etc/fstab are converted to systemd mounts 
        * checkl /run/systemd/generator for the automatically generated file 
        * mounts can be created using systemd.mount files (allow for more specific dependencies definition)
        * fstab is still the standard (systemctl cat tmp.mount for example)
* Creating swap 
    * managing swap 
        * swap is RAM emulated on disk 
        * set partition type to linux-swap
            * after creating the swap partition, use mkswap to create FS
            * swapon (activate)
        * Look at demo
            * create swap in fdisk 
            * mkswap partition
            * swapon partition
            * add to fstab
            * partition_or_UUID none (mount point) swap default 0 0 

### 19.1 Understanding Advanced storage solutions 

* RHEL advanced Storage solutions 
    * LVM logical volumes 
        * used during default installation of RHEL (adds flexibility to storage, resize, snapshots, and more)
    * Stratis
        * next gen volume managing filesystem that uses thin provisioning by default)
        * implemented in user space, which makes API access possible 
    * Virtual data optimizer 
        * Now integrated in LVM 
        * Focused on storing files in the most efficient way - deduplicated and compressed storage pools

### 19.2 exploring LVM setup/19.3 creating an LVM logical volume 

* How LVM is organized 
    * Volume group 
        * Behaves as an abstraction of all the storage you have (all devices go in the volume group)
        * Can be disk, partitions or any block device (many physical volumes together)
        * Logical volumes (LV)
        * These are the entities that you put the filesystem or swap on (these are what are mounted)
        * /dev/vgx/lvx
* Creating an LVM logical volume 
    * LVM creating procedure overview
        * Create a partition and set the partition type to lvm
        * can be don on complete disk or partitions
        * pvcreate /dev/sdb1 (to create the physical volume)
        * vgcreate vgdata /dev/sdb1 (to create the volume group)
        * lvcreate -n lvdata -L 1G vgdata (to create the logical volume)
        * mkfs /dev/vgdata/lvdata (to create a filesystem)
        * put it in /etc/fstab to mount it persistently (no need for UUIDs or Labels)
    * Understanding extents 
        * vgdisplay (show the properties of volume groups, including the extent size)
        * Extexts are the elementary blocks of LVM allocation (can be defined while defining the VG)
        * vgcreate -s 8M vgdata /dev/sdb1 (to create a volume group with an extent size of 8MB)
            * all of the LVM logical volumes built from the volume group will use the same extent size 
    * Look at the demo
        * /dev/vgdata/lvdata /lvdata vfat defaults 0 0 (in etc/fstab)

### 19.5 resizing LVM logical volumes/19.6 reducing volume groups 

* Resizing logical volumes 
    * vgs (verify the volume group has unused disk space)
    * lvextend (to add one more PVs to the VG - pool volume?)
    * lvextend -r -L +1G (to grow the LVM logical volume, including the filesystem it is hosting)
        * resize2fs (resize utility for ext filesystem)
        * xfs_growfs (can be used to grow XFS filesystem)
        * shrinking is possible on ext4 filesystem, not on xfs 
    * demo
* Reducing volume groups 
    * demo 


### 20.1 Understanding storage stack / 20.2 creating stratis volumes 

* Look at 20.1 understanding storage stack
* Creating stratis volumes 
    * Stratis volumes always use XFS (thin provisioned by nature)
    * Volume storage is allocated from the stratis pool (each stratis volume needs min size of 4GiB)
* Managing stratis 
    * stratisd and stratis-cli packages 
    * Great tab completion
    * To mount stratis volumes 
        * use UUID 
        * include x-systemd.requires-stratisd.service (as mount option along with default)
    * LOOK at demo for this 

### 20.3 Using stratis snapshots 

* Understanding strais snapshots 
    * demo 

### 21.1 exploring boot procedure / 21.2 modifying grub2 runtime parameters

* Boot procedure (important for troubleshooting)
    * all starts at the firmware 
    * from the firmware the boot device is allocated 
    * on the boot device is the boot sector
    * then grub is the boot loader 
    * loads the linux kernel
    * initramfs 
    * systemd (manager of everything)
    * early state
    * services 
    * while services are being loaded the shell is being dropped 
* Modifying grub2 runtime parameters 
    * from grub2 boot menu press e to edit runtime boot options 
        * end of the line that starts with linux 
        * systemd.unit=emergency.target
        * systemd.unit=rescue.target
        * c to enter grub2 command mode 
            * from command mode type help for an overview of available options 

### 21.3 changing grub2 persisten parameters/21.4 managing systemd targets/21.5 setting the default systemd target 

* Modifying grub2 persistent parameters 
    * /etc/default/grub (edit persistent grub2 parameters)
    * grub2-mkconfig -o /boot/grub2/grub.cfg (compile changes to grub.cfs)
    * grub2-mkconfig -o /boot/efi/efi/redhat/grub.cfg (for efi system)
    * Figure out if you are on an efi system
        * lsblk (boot disk only has a boot partition not a boot/efi partition than MBR)
        * /boot/efi (then you are on efi)
* understanding systemd targets 
    * Systemd target is a group of unit files 
        * emergency.target
        * rescue.target 
        * multi-user.target
        * graphical.target 
    * systemctl list-dependencies
* Setting the default systemd target 
    * systemctl get-default (see the current default target)
    * systemctl set-default (to set a new default target)

### 21.6 Boot into a specific target 
    * grub2 boot prompt use systemctl.unit=xxx.target to boot into a specific target (think this is systemd.unit=xxx.target)
    * to change between targets on a running system use systemctl isolate xxx.target 

### 22.1 Using troubleshooting modes/22.2 changing the root password 

* Changing a lost root user password 
    * enter grub menu while booting 
    * linux line
    * init=/bin/bash (at the end of the line)
    * mount -o remount,rw / (mount the root filesystem so you can read write)
    * passwd root (change the root password)
    * touch /.autorelabel
    * exec /usr/lib/systemd/systemd

### 22.3 using the boot debug shell/22.4 troubleshooting filesystem issues 

* Understanding the early boot debug shell 
    * If something goes wrong in the early boot procedure it may be useful to have an option to open debug shell
    * debug-shell.service is provided 
    * Starts a root shell that can be accessed on TTy9 without having a root password 
    * systemctl enable --now debug-shell.service
    * WHile booting acess a virtual terminal on tty9
        * Ctrl-Alt-F9
    * systemctl disable --now debug-shell.service 
* Troubleshooting filesystem issues 
    * mount -a (to mount all filesystems in /etc/fstab that have not been mounted yet)
    * findmnt --verify (to verify syntax)
    * rebooting after changes to /etc/fstab

### 22.5 fixing network issues/22.6 managing performance issues/22.7 troubleshooting s/w issues 

* Understanding common network issues 
    * wrong subnet mask 
    * wrong router
    * DNS not working: verify /etc/resolv.conf
    * ip addr show 
    * ip route show 
    * ping 
    * cat /etc/resolv.conf
* managing performance issues 
    * Four key areas 
        * memory 
        * cpu load 
        * disk load 
        * netowk 
        * top and killing processes 

### 22.8 fixing memory shortage

* vmstat

### 23.2 exploring essential script components 

* #!/bin/bash (she bang)
* # comments 
* Args and variables 
    * key=value 
    * $variable 
    * positional parameters $0 $1 $2 
    * color=red 
    * echo color (prints out the word color)
    * echo $color (prints the variable color)

### 23.3 executing conditional code with if and test 

* if ... then ... else statement
* [ condition ]
* man test 
* example 
    * if [ $1 = "hello" ]; then
    * echo something
    * else 
    * echo something else
    * fi 
* $? (get the exit code of the last command echo $?)

### 23.4 using for and while 

* understanding for and while 
    * while is used to run commands as long as a specific condition is true
    * for is used to iterate over a series of elements 
* bash -x script (debug mode)
* for i in $1/*.txt (*)
* for i in list, command, {range};do something;something else;done 
* while true;do something;done 
* Make sure you review and bring in a better example of these three options

### 24.1 understanding ssh key based login/24.2 setting up ssh key based login

* ssh-keygen (create a public/private key pair)
    * passphrase (entered in everytime)
* ssh-copy-id (copies the public key over to the target server)

### 24.3 caching ssh keys 

* ssh-agent /bin/bash (allocates space in the bash shell to cache the private key passphrase)
* ssh-add (adds the current passphrase to the cache)
* Look at demo

### 22.4 Defining ssh client config/24.5 exploring common ssh options 

* Understanding ssh client options 
    * ssh -X enable XForwarding (forwarded sessions are subject to X11 security extension controls)
    * ssh -Y (enables trusted X forwarding)
    * ssh client options can be set persistently in /etc/ssh/ssh_config or ~/.ssh/ssh_config
* Exploring common ssh options 
    * server options are set in /etc/ssh/sshd_config 
        * port 22 
        * PermitRootLogin
        * PubKeyAuthentication
        * PasswordAuthentication
        * X11Forwarding
        * AllowUsers 

### 24.6 copying files securely/24.7 Synchronizing files securely 

* scp copying files securely 
    * scp file1 file2 student@remoteserver/home/server
    * scp source target 
    * sftp 
* Synchronizing files securely 
    * rsync 
        * -r (recursively synch the entire dir tree)
        * -l (synch symbolic links)
        * -p (preserve symbolic links)
        * -n (will do a dry run before actually synchronizing) 
        * -a (archive mode, which is equivalent to -rlptgoD)
        * -A (archive mode and also synch ACLs)
        * -X (will synch SELinux context as well)

### 25.1 exploring HTTP config/25.2 creating a basic web site

* Exploring apache config 
    * httpd (apache web server)
    * main http config file is /etc/httpd/conf/httpd.conf
    * additional drop in files can be stored in /etc/httpd/conf.d 
    * default document root is /var/www/html (htdocs? - looks for index.html file in dir)
    * dnf install httpd 
    * systemctl status httpd 
* Creating a basic web site 
    * drop the index.html file in /var/www/html 
    * /var/log/httpd (access_log and error_log)

### 26.2 using SELinux modes 

* SELinux modes and states 
    * disabled or enabled 
    * Two different modes when enabled 
        * enforcing (normal mode)
        * permissive (just logging not blocking anything)
        * setenforce (change between permissive and enforcing)
        * getenforce (show current state)
        * edit /etc/sysconfig/selinux (to manage the default state of SELinux)
    * Managing SELinux states while booting 
        * enforcing=0 (start in permissive mode)
        * enforcing=1 (start in enforcing mode)
        * selinux=disabled 
        * selinux=1 (enable)
        * accessed through grub bootloader prompt 

### 26.3 exploring SELinux components 

* Exploring SELinux components 
    * SELinux works with context labels 
    * context labels define specific permissions 
    * Context labels are applied to source objects and target objects 
    * Source objects are 
        * users 
        * processes 
    * Target objects 
        * files and dirs 
        * ports 
* Managing SELinux 
    * Context management is about applying context to mostly files, dirs, and ports 
    * You will need to apply a context that matches a specific rule 
    * Source and targets 
    * labels like myapp_t (label dictates what it is allowed to do)

### 26.4 using file context labels 

* Understanding context labels 
    * every object is labeled with a context label 
    * user: user speific context 
    * role: role specific context 
    * type: flags which type of opertation is allow on this object 
    * type is the only one to matter for RHCSA 
    * -Z option to show current context information
* Understanding default file context 
    * When files are created in a dir they typically inherit the context of the parent dir 
    * When files are copied they typically inherit the context of the parent directory 
    * When files are moved, they keep the OG context 
* Managing file context labels 
    * semanage fcontext (to set file context label)
        * writes the context to the SELinux policy but is not written to the filesystem)
    * semanage fcontext -a (to set a new context label)
    * semanage fcontext -m (modify an existing context label)
    * restorecon (enforce the policy setting on the filesystem)
    * touch /.autorelabel (to relabel all files to the context that is specified in the policy)
    * man semanage-fcontext (for docs)
    * semanage fcontext -l -C (show only setting that have changed in the current policy)

### 26.5 finding the right context / 26.6 managing SELinux port access 

* Finding the right context 
    * selinux-policy-doc (man doc)
    * Look at the demo for this
* Managing ports 
    * Network prots are also provided with an SELinux context label 
    * SELinux policy is configed to allow default port access 
    * semanage port (to apply the right label to the port for non default port access)
    * semanage-port (man page great examples)
    * Look at the demo for sshd example 

### 26.7 Using booleans 

* Using booleans 
    * Easy to use config switch to enable or disable specific parts of SELinux policy 
    * semanage boolean - or getsebool -1 (overview of all booleans)
    * setsebool -P boolean [on|off] (to set booleans)
    * semanage boolean -l -C (to see all booleans that have a non default setting)
    * demo

### 26.8 analyzing selinux log messages/26.9 troubleshooting SELinux 

* Using sealert
    * SELinux uses auditd to write log messages to the audit log 
    * journalctl | grep sealert 
    * run sealert command with UUID message to get specific troubleshooting 
* Troubleshooting SELinux 
    * setenforce=0 (set selinux to 0 to see if SELinux is in fact the reason something is blocked)
    * grep AVC /var/log/audit/audit.log (see raw audit messages)
        * Look at source context and target context
    * dnf install selinux-policy-doc (for additional man pages)
    * journalctl | grep sealert (read the alert message generated) 
    * demo

### 27.1 Analyzing service config with ss/27.2 managing RHEL firewalling 

* Monitoring network sockets with ss 
    * Network socket is a connection endpoint, consisting of an IP address followed by a port 
    * UNIX sockets, enpoints in communication with service on Linux/UNIX
    * ss is the standard tool to show socket information
        * ss (show all connections)
        * ss -tu (shows connected TCP and UDP sockets)
        * ss -tua (adds sockets that are in listening state)
        * ss -tln (show tcp sockets that are in listening state only without resolving hostnames)
        * ss -tulpn (shows TCP and UDP sockets in listening state and adds process names or PID to output)
* managing RHEL firewalling 
    * firewalld is a service, managed by systemd, RHEL uses as front end to manage nftables firewalls

### 27.3 exploring firewalld componets/27.4 config a firewall with firewall-cmd 

* Understanding firewalld components 
    * Firewall uses different components to make firewalling easier
        * Service: main component contains one or more ports as well as optional kernel modules that should be loaded 
        * Zone: a default config to which network cards can be assigned to apply specific settings
        * Ports: optional elements to allow access to specific ports 
        * Additional components are available as well, but no used often in base firewall config 
        * firewall-cmd --list-all (services, and interfaces they are accessible on)
* Configuring a firewall with firewall-cmd 
    * Using firewall-cmd 
        * firewall-cmd command is used to write firewall config
        * option --permanent to write to persistent (but not to runtime)
        * Without --permanent the rule is written to runtime (but not to persistence)
    * systemctl status firewalld 
    * firewall-cmd --list-all 
    * firewall-cmd --get-services (list all services available)
    * firewall-cmd --add-service http
    * firewall-cmd --add-service http --permanent 


### 28.1 exploring solutions for automatic installation/28.2 creating a kickstart file 

* Creating a kickstart file 
    * after install, anaconda-ks.cfs is created and saved in the root users home dir 
    * ksvalidator (to verify the file syntax after manually editing)
    * Common kickstart file options
        * url --url="http:/myserver/..." (specifies which url to access for the installation media)
        * repo --name="myrepo" --baseurl=... (how to access repos)
        * text forces text mode installation
        * vnc --password=password (enables the VNC viewer for remote access to the installation)
        * clearpart --all --drive=sda,sdb (removes all partitions)
        * part /home --fstype=ext4 --label=home --size=2048 --maxsize=4096 --grow (creates and mounts a partition)
        * autopart (automatically creates root, swap and boot partitions)
        * network --device=ens33 --bootproto=dhcp (config the primary network int)
        * firewall --enabled --service=ssh,http (enable and open firewall)
        * timesource --ntp-server pool.ntp.org (set up NTP)
        * rootpw --plaintext secret (config plain text password)
        * selinux --enforcing (activates SELinux)

### 28.3 using a kickstart file for automatic installation/28.4 installing virtual machine 

* Using a kickstart file 
    * typically the kickstart file is provided on an installation server 
    * Before starting the install the client indicates where to get the kickstart file from 
        * use ks=http://somewhere/ks.cfg (to access from a web server)
        * ks=hd:LABEL=MYLABEL:/directory/file (to access from a device (such as USB) only works with LABEL or UUID)
        * Or use the interfgace provided by the installation program (as in virtual machine manager)
* 28.4 installing virtual machine 
    * Look at demo not sure this is related to RHCSA 

### 29.1 exploring linux time/29.2 setting time with timedatectl 

* Exploring linux time 
    * hwclock is used to set hardware time
    * also use it to synch time 
        * hwclock --systohc
        * hwclock --httosys
        * date (set and show time)
        * timedatectl (used to manage time and time zone config)
* Setting time with timedatectl 
    * using timedatectl 
        * timedatectl is a new utility that allows you to manage all aspect of system time 
            * timdatectl status (will show all time properties currently used)
            * timedatectl set-time (used to change the time)
            * timedatectl set-timezone (is used to change the timezone)
            * timedatectl set-ntp (enables or disables NTP time synchronization)
        * To synch time using NTP and NTP service must be configed
            * RHEL uses chrony

### 29.3 Managing an NTP client 
    
* Managing an NTP client 
    * chronyd is the default RHEL NTP service 
    * /etc/chrony.conf to specify synch paramters 
        * pool 2.rhel.pool.ntp.org iburst (configs a pool of NTP servers)
        * server myserver.example.com (confs a single NTP time source)
        * iburst to permit fast synch
        * After modifying its contents, use systemctl restart chronyd to restart chronyd service 
        * chronyc sources to verify proper synchronization

### 30.1 Config a base NFS server/30.2 Mounting NFS shares 

* Config a base NFS server
    * Not in RHCSA
    * Config a base NFS server 
        * dnf install nfs-utils 
        * mkdir -p /nfsdata /home/ldap/ldapuser{1..9}
        * echo "/nfsdata *(rw,no_root_squash)" >> /etc/exports (*)
        * echo "home/ldap *(rw,no_root_squash)" >> /etc/exports (*)
        * systemctl enable --now nfs-server
        * for i in nfs mountd rpc-bind;do firewall-cmd --add-service $i --permanent;done
        * firewall-cmd --reload 
* Mounting NFS shares 
    * NFS client 
    * nfs-utils is installed 
    * showmount -e nfsserver (show exports)
    * mount nfsserver:/share /mnt (to mount)

### 30.3 understanding automount/30.4 config automount

* Autofs server/understanding automount
    * /etc/auto.master (ID the dir that automount should manage and the file that is used for additional mount information)
        * /data /etc/auto.nfsdata
        * in /etc/auto.nfsdata you will ID the subdir on which to mount, and what to mount exactly
        * files -rw nfsserver:/nfsdata
    * ensure the autofs service is started 
        * systemctl enable --now autofs 
        * /etc/auto.misc for syntax examples 
* configuring automount 
    * dnf install -y autofs 
    * cd /etc/
    * vim auto.master
    * IN auto.master file 
        * /nfsdata /etc/auto.nfsdata
        * /etc/auto.misc (provides some syntax examples)
    * vim auto.nfsdata 
        * files -rw nfsserver:/nfsdata
    * systemctl enable --now autofs
    * ls /
        * should see the /nfsdata dir
    * cd /nfsdata
        * ls -al 
        * cd files 
        * mount | tail -3

### 30.5 setting up automount for home directories 

* Understanding wildcard mounts 
    * Automount is common for home dir access 
        * NFS server is providing to home dirs, and then home dir is automounted by a user while logging in
        * to support different dirs names in one automount line, wildcards are used 
        * * -rw nfsserver:/home/ldap/&
        * demo for this 

### 31.1 understanding containers 

* Understanding containers 
    * containers are like an app on a smartphone, it is a package that contains all that is needed to run an application
    * Solution for dependency challenges 
    * Containers are started from container images 
    * Container and linux 
        * Containers rely on features provided linux OS 
            * Control groups set limits to the amount of resources that can be used 
            * Namspaces provide isolation to ensure the container only has access to its own data and config 
            * SELinux enforces security security
    * Understanding rootless containers 
        * Containers need a userID to be started on the host computer 
        * root containers are started by the root user 
        * Rootless containers are started as a non root user 
            * Rootless containers can generate a UID gynamically or be preconfiged to use a specific UID 
            * Rootless containers have a few limitations - no unlimited access to the filesystem
            * can not bind to privileged network ports 
    * Containers and microservices 
        * Complex apps typically composed of multiple containers 
        * normally containers run one application - better manageability 
        * To manage microservices, orchestration platforms like k8 or Red Hat Openshift are used
    * Understanding red hat container tools 
        * podman manages containers and container images 
        * buildah is an advanced tool to create container images
        * skopeo is an advanced tool to manage copy delete and sign images 

### 31.2 managing images 

* Using images and registries
    * Container images are used to package container applications with all their dependencies 
    * OCI specification compatibility so that iamges can be used in different env (podman or docker)
    * Container images are offered through registries 
* Using registries 
    * Public registries such as hub.docker.com provide access to community provided container images 
    * private registeries can be created to host container images internally 
    * quay.io (images optimized for use in red hat env)
    * Red hat distributes cerified images that are accessible only with red hat credentials 
        * registry.red.hat.io (is for the official red hat products)
        * registry.connect.redhat.com (is for third party products)
        * Red hat container catalog (https:catalog.redhat.com) is a web interface to the red hat images)
* Accessing red hat registries 
    * red hat registries can be accessed with a red hat account 
    * developer accounts (https://developers.redhat.com) do qualify 
    * podman login registry.redhat.io (to login to a registry)
    * podman login registry.redhat.io --get-login (to get your current login credentials)
    * /etc/containers/registries.conf (registry access is configed in)
        * registries that do not ahve an SSL cert in [registries.insecure]
        * user specific registries.conf file can be created as ~/.config/containers/registries.conf
* Using containerfiles
    * a containerfile (previously known as dockerfile) is a text file with instructions to build a container image
    * ContainerFiles have instructions to build a custom container based on a base image such as the UBI image
    * UBI is the universal base image, an image that red hat uses for all of its products 
    * Demo
        * dnf install container-tools 
        * git clone https://github.com/sandervanvugt/rhcsa (getting a containerfile)
        * podman info
        * cd rhcsa
        * podman images (should not have any)
        * podman login registry.access.redhat.com 
        * pdoman build -t mynam . (building images from the container file)
        * podman images (should show an image now)
        * Don't need to create a container file but know how to use an existing one
        * podman info

### 31.3 Running containers 

* Running containers 
    * podman run to run a container
    * Will search for the image in the configed registries (if found, it will pull the image and run the container)
    * podman ps (verify that the iamge currently is running)
    * podman ps -a (also show containers that are stopped)
    * podman inspect (to see what is inside an image or container)
* Understanding container commands 
    * when started with podman run, the container runs its default command 
    * run an alt command it can often (not always) be specified as a command line arg
        * podman run ubi8 sleep
    * run an image from a specific registry specify the complete image name
    * command line options for the specific podmna command need to be specified b4 the name fo the image 
* Common podman commands 
    * podman search (searches registries for images)
    * podman run (runs a conatiner)
    * podman stop (stops a currently running conatiner)
    * podman ps (shows information about containers)
    * podman build (builds an image from a container file)
    * podman images (list images)
    * podman inspect (shows container or image details)
    * podman pull (pulls an image from the registry)
    * podman exec (executes a command in a running conatainer)
    * podman rm (removes a container)
    * demo
* Troubleshooting containers 
    * Troubleshooting containers is often troubleshooting the containers primary command 
    * Some containers run to completion and there is nothing to troubleshoot
    * podman inspect conatiner (to see which command it started)
    * podman run -it ... (to start the container with an interactive shell)
    * podman logs (to explore logs created by container)


### 31.4 mapping ports and config variables 

* Managing env variables 
    * Some images require site specific information to be passed while running 
    * -e KEY=VALUE (to pass these values thru env variables while running the container)
    * podman run -name mydb -e MYSQL_ROOT_PASSWD=password quay.io/centos7/mariadb-103-centos7
* Config application access 
    * container access happens through port mapping
    * a port conatiner host is exposed and forwards traffic to the conatiner port 
    * Port mapping can be set while starting the container but not on a container that has already been started
    * rootless containers can only map to non privilged port (higher than 1024)
    * Demo
    * podman run -d -p 8080:80 registry.access.redhat.com/ubi/nginx-120
    * podman port -a 
    * sudo firewall-cmd --add-port=8080/tcp --parmanent 
    * sudo firewall-cmd --reload

### 31.5 providing persistent storage 

* Managing storage 
    * Container storage is ephemeral by nature 
    * persistent storage can be provided
        * creating a dir on the container host and bind-mounting that dir in the conatiner 
        * podman run -d ... -v /hostdir:/containerdir
        * When bind mounting dir on the host file ownership on these dirs is important 
        * If a container is started by the root user UIDs and GUIDs on the host match the UIDs and GIDs in the container
        * For a rootless container you will need to make sure that the UID of the user that runs the conatiner app is owner of the bind-mount dir
        * podman inspect (on the image to find out which user this is)
* Rootless containers and namespaces
    * rootless containers are launched in a namespace
    * The namespace provides isolation, allowing the container inside the namespace to have root access which does not exist outside the namespace 
    * Means that inside the conatiner namespace is different UIDs are used than outside of the namespace
    * To ensure that access is working all right UIDs are mapped between the namespace and the host OS 
    * podman unshare command can be used to run commands inside the container namespace
    * podman unshare cat /proc/self/uid_map (to get the UID mapping)
        * See the container root user maps to your host ordinary UID
* Understanding non root access user mapping 
    * TO set appropriate dir ownership on bind mounting dirs for rootless containers, additional work is required 
    * First find the UID of the user that runs the main application
        * podman inspect imagename
        * podman exec containername grep usernam /etc/passwd 
    * podman unshare chown nn:nn directoryname (set the container UUID as the owner of the dir on the host)
    * Directory name must be in the user home dir b/c otherwise it would not be part of the user namespace 
    * podman unshare cat /proc/self/uid_map (to verify mapping)
    * verify the mapped user is owner of the host using ls -ld /directoryname 
    * demo
* Config SELinux for shared directories 
    * To bind mount a host dir in the container the container_file_t SELinux context type must be used
    * If ownership on the host dir has been configed all right use the :Z option to auto set this context
        * podman run ... -v /home/student/mydb:/var/lib/mysql:z ...
    * DEMO

### 31.6 starting containers as systemd service 

* Autostarting containers 
    * Auto start containers in a standalone situation 
    * Create systemd user unit files for rootless containers and manage them with systemctl 
    * Running systemd services as a user
        * systemd user services start when a user sessions is open
        * closed when user session is stopped 
        * loginctl enable-linger (to change this behavior and start user services for a specific user (requires root))
        * loginctl enable-linger linda
        * loginctl show-user linda
        * loginctl disable-linger linda 
    * managing container using systemd services 
        * create a regular user account to manage all containers 
        * use podman to generate a user systemd file for an existing container
        * before, mkdir ~/.config/systemd/user;cd ~/.config/systemd/user
        * podman generate systemd --name myweb --files --new 
        * to generate a service file for a root container, do it from /etc/systemd/system
* Understanding podman generate ---new 
    * podman generate --new option will create a new container when systemd unit is started
    * Delete the container when the unit is stopped 
    * without --new the container is not newly created or deleted when stopped 
* Creating user unit files
    * podman generate to create user specific files in ~/.config/systemd/user
    * Edit the file that is generated and change the WantedBy line to read WantedBy=default 
    * Manage them using systemctl --user 
        * systemctl --user daemon-reload
        * systemctl --user enable myapp.service (requires linger)
        * systemctl --user start myapp.service 
        * NOTE: systemctl --user only works when logged into a console or SSH not sudo or su sessions
        * DEMO
* Survive all challenges 
    * login as the user that should start the container, not su or sudo
    * set a password to do so
    * mkdir -p ~/.config/systemd/user
    * podman generate --new 
    * Make sure the container-name.service file has WantedBy=default.target
    * man podman-generate
    * man podman-generate-systemd

### 31.7 building images from containerfiles 

* sudo dnf provides */Containerfile (*)
* sudo dnf install buildah-tests
* sudo find / -name "Containerfile" (list of container files to look at as an example)
* sudo find / -name "Containerfile" exec ls -l {} \; (look at the size)
* podman build -t runmap rhcsa/ (build the image from a container file)
* podman images (see images)
podman run localhost/runmap:latest

## Objectives 

### Understanding and use essential tools 

* Access a shell prompt and issue commands with correct syntax 
    * Using virtual terminal 
        * Ctrl-ALT-Fn
        * chvt number
    * Using command line 
        * command --help 
    * find command 
        * find / -name "hosts"
        * find / -type f -size +100M
        * find . -perm /4000
        * find /etc -exec grep -l student {} \; -exec cp {} find/contents/\; 2> /dev/null
        * sudo find / -name "Containerfile" -exec ls -l {} \; (look at the size)
        * find /etc/ -name '*' -type f | xargs grep "127.0.0.1" (*)
    * awk 
        * awk -F: '{print $4}' /etc/passwd
        * awk -F: '/linda/ {print $4}' /etc/passwd
        * awk -F: '{print $NF}' /etc/passwd 
        * ps -ef | grep -i null | awk '{print $2}' | xargs kill -9 
    * Bash ENV
        * /etc/profile (generic bash startup file containing all system setting that are processed in a login shell)
        * /etc/bashrc (processed while opening a subshell)
        * ~/.bashrc (user specific version of /etc/bashrc)
        * ~/.bash_profile (user specific version of /etc/profile)
        * Drop in files /etc/profile.d
        * /etc/skel (files that are copied to home directory of user upon creation)
    * Other commands reminders
        * tail -f (-F) file 
        * less (pager)
        * WHICH/FILE/TYPE
            * which command (find the source)
            * file file (to see what type of file)
            * type command (see if its built in)
            * alias
                * alias del='rm -rf /'
                * unalias del 
                * making these persistent
        * ksvalidator 
            * anaconda file in root home dir 
* use input output redirection (>, >>, |, 2>, etc)
    * > (write a result of a command to a file)
    * >> (append to a file)
    * 2> (stderr redirection)
    * < (redirect stdin input to a file)
    * | (redirect stdout of a command to stdin of the next command)
    * &> (redirect stdout and stderror command &> somefile)
        * &>> (append)
        * some_command > output.file 2>&1 (redirect stderr to stdout and stdout into the file)A
        * some_command >> output.file 2>&1 (append)
            * order matters and alittle more perfered than &> (&> is bash only)
* Use grep and regular expression to analyze text 
    * grep to find text in files or output
        * grep -v (exclude search results)
        * grep -i (insensitive)
        * grep -A5 -B5 (after and before lines)
        * grep -R (recursively search dirs)
    * regular expressions 
        * man 7 regex 
        * grep -E (extended regular expressions)
        * ^ (beginning of the line)
            * grep '^|' myfile 
        * $ (end of the line)
            * grep 'anna$' myfile
        * \b (end of word)
            * grep '^lea\b' myfile
            * find lea, but not leanne
        * zero or more times
            * grep 'n.*x' myfile (*)
        * one or more times (extended regex)
            * grep -E 'bi+t' myfile
        * ? zero or one times (extended regex)
            * grep -E 'bi?t' myfile
        * \n{3\} n occurs 3 times
            * grep 'bon\{3\}nen' myfiles
        * string must be a word
            * grep '\banna\b' myfile
        * . one character
            * grep '^.$' myfile
        * either option
            * grep -E '( svm | vmx )' /proc/cpuinfo
* Access remote systems using ssh 
    * ssh user@ip_address
    * ssh ip_address (connect to the same user that you are on the local machine)
    * Make sure to look at /etc/hosts in order to config hostname instead of IPs (rhcsa_guide)
* login and switch users in multiuser target 
    * su - (switch to a user and will be prompted for there password)
        * su -c "whoami" (specific command)
    * sudo -i (open a root shell)
    * /etc/passwd, /etc/shadow, /etc/sudoers
* archive, compress, unpack, and uncompress files using tar, gzip, and bzip2 
    * tar tf archive.tar (list content)
    * tar cf archive.tar file1 (create tar archive)
    * tar xf archive (extract)
    * tar xf archive.tar -C /tmp/ (extract to specfic directory)
    * sudo with extract to restore permission and ownership
    * Compress and uncompress with tar
        * tar czf archive.tar.gz file1 (gzip create)
        * tar cjf archive.tar.bz2 (bzip2 create)
        * autocompress
        * tar caf archive.tar.gz file1 (auto compress based on file compression)
        * tar xf archive.tar.gz (extract does not need a compression - test this)
    * Compress with bzip2 and gzip
        * gzip file1
        * bzip2 file1
        * gunzip file1.gz
        * bunzip2 file.bz2
        * Keeping the original file -k or --keep (otherwise file is deleted and new compressed file is made)
* create and edit text files 
    * touch file
    * vi file 
    * Cat EOF trick
        * cat >> /etc/yum.repo.d/Appstream.repo << EOF
        * > [AppStream]
        * > name=AppStream
        * > baseurl=file:///repo/AppStream
        * > gpgcheck=0
        * > EOF
* create, delete, copy and move files and directories 
    * cp source destination
    * cp -r srouce destination (recursive cp of the dir)
    * mv source destination (can also rename)
    * rm filename 
    * rm -r dir/ (remove recursively)
        * rmdir (removes a dir also)
* create hard and soft links 
    * ls -il (inode number)
    * ln /etc/hosts myhosts 
    * ln -s myhost symhost
    * ln [target] [linkname]
    * ln path_to_target path_to_link_file
    * Only hardlink to files not folders (only files on same filesystem)
* List, set, and change standard ugo/rwx permissions 
    * ls -l 
    * chown user:[group] file (to set user-ownership)
    * chgrp group file (to set group ownership)
    * chown lisa:sales newfiles/ (change user and group)
    * chown :sales newfile/ (change group ownership with chown)
    * RWX
        * within files and dirs 
            * files 
                * read: open a file
                * write: allow to modify the content of the file 
                * execute: allows you to run the file
            * directories 
                * read: list files in a dir 
                * write: allows you to create or delete files 
                * execute: allows you to cd and go into directory 
        * Octals
            * read: 4
            * write: 2 
            * execute 1
        * u,g,o (user, group, others)
            * u+, g+, o+
            * + r, w, x, rw, rwx
            * u-, g-, o- (remove permissions)
        * Exact permissions
            * u=, g=, o= (wipes everything set them to an exact value)
* locate, read and use system docs including man, info, and files in /usr/share/doc 
    * who [OPTION] ... [ FILE | ARG1 ARG2 ]
        * [ ] optional ... multiple options
        * | OR indicator 
    * --help (man has more information)
    * man man
    * man -k (-K to go through them)
    * sudo mandb (rebuild man pages)

### Create simple shell scripts 

* Conditionally execute code (use of: if, test, [], etc.)
    * Basic shell script info
        * #!/bin/bash (she bang for scripts)
        * # comments 
        * making it executable
        * running with path ./script.sh
        * bash -x script (debug mode)
        * echo $? (exit code of the last command)
        * cat /etc/cron.hourly/0anacron (to get an example of scripting)
    * if, test, []
        * help if 
        * help test 
        * man test 
        * if some_condition;then fi 
        * conditions [ ]
            * rocket_status=$(rocket-status $mission_name)
            * if [ $rocket_status = "failed" ]; then
                * rocket-debug $mission_name
            * elif [ $rocket_status = "success" ];then
                * do_something
            * else
                * do_something
            * fi
        * Conitional operators 
            * = (matching strings exactly)
            * != (strings are not equal)
            * -eq (number is equal)
            * -ne (numbers are not equal)
            * -gt -lt (greater than and less than numbers)
            * [[ ]] (only in bash)
            * [ COND1 ] && [ COND2 ]
            * [ COND1 ] || [ COND2 ]
            * [[ COND1 || COND2 ]]
            * [ -e FILE ] (if files exists)
            * -d FILE (if file exists and is a dir)
            * -s FILE ( if file exists and has a size greater than 0
            * -x FILE (if the file is executable)
            * -w FILE (if file is writable)
* Use looping constructs (for, etc.) to process file, command line input 
    * For loop brief
        * for i in {1..10};do echo $i;done
        * for i in {one,two,three};do echo $i;done
        * for i in $(seq 1 10);do echo $i;done (passing a command)
        * for i in `seq 1 10`;do echo $i;done (older way to pass a command)
        * can also just list them without anything
            * for i in test test1 test2 test3;do echo $i;done
        * for (( i=0 ; i <= 100; i++ ));do echo $i;done
        * for i in *;do echo $i;done (* this will grab everything in the dir like gitcheck)
    * while loop
        * while [ conditional ];do something;done
        * executes as long as the condition is true
    * example while loop might be good
        * while true; do (infinite)
            * echo "1: shutdown"
            * echo "2: restart"
            * echo "3: exit menu"
            * read -p "Enter your choice: " choice
            * if [ $choice -eq 1 ];then
                * shutdown now
            * elif [ $choice -eq 2 ];then
                * shutdown -r now
            * elif [ $choice -eq 3 ];then
                * break (break out of the loop)
            * else
                * contiune (go to the top of the loop if something other than 1,2,or 3 is entered)
            * fi
        * done
* Process script inputs ($1, $2, etc)
    * command line args: $1, $2 and so on
        * $0 (name of the script)
        * for args above 9th ${10}
        * $@ (all args as a single string seperated by spaces)
        * $# (total number of args passed)
    * read -p "Enter in something" choice (read input into a variable called choice)
        * read variable (without the prompt)
* Processing output of shell command within scripts 
    * Specify exit codes within a script 
        * exit 1 (within the script and can exit the script with a specific code like under else statement)
    * break statement (breaks and exits the loop whether while or for)
    * contiune statement 
        * execution back to the beginning of the loop

### Operate running systems 

* Boot, reboot, and shutdown a system normally 
    * Reboot and shutdown
        * systemctl reboot (need sudo/root)
        * systemctl poweroff (need sudo/root)
        * System refuses to reboot or shutdown normally
            * not recommended unless absolutely needed 
            * sudo systemctl reboot --force 
            * sudo systemctl poweroff --force 
            * Can pass force twice if really needed (sudo systemctl reboot --force --force)
        * shutdown 02:00 (24 hour format 00:00 to 23:59 (midnight to 11:59) schedule shutdown)
        * sudo shutdown +15 (shutdown in 15 minutes)
        * sudo shutdown -r 02:00 (reboot at 2am)
        * sudo shutdown -r +15 (reboot in 15 minutes)
        * sudo shutdown -r +1 'Scheduled restart to do an offline-backup of our database' (wall message)
        * shutdown -c (cancel)
        * shutdown --show (to see scheduled shutdowns)
* boot systems into different targets manually 
    * systemctl get-default 
    * systemctl set-default multi-user.target (sudo)
    * rebooting 
    * sudo systemctl isolate graphical.target (change directly into the graphical from multi-user)
        * this does not change the default however multi-user will still be the default
    * Useful targets 
        * emergency.target
        * read only file system (mount -o remount,rw /)
        * rescue.target (few more than emergency and root must have passwd)
* interrupt the boot process in order to gain access to a system
    * getting to grub boot screen
        * e (to get to the grub options - esc or arrows up and down to get grub)
        * system.unit=xxx.target (boot specific target)
            * in the linux kernel line add system.unit=rescue.target (boot into the rescue target)
    * Modifying persistent grub2 parameters 
        * /etc/default/grub (config file to edit)
        * after making changes compile changes to grub.cfg
            * grub2-mkconfig -o /boot/grub2/grub.cfg
            * grub2-mkconfig -o /boot/efi/EFI/redhat/grub.cfg
            * lsblk to see if boot partition is boot/efi (that means efi and the second option is needed)
        * sudo grub2-install /dev/vda > /home/bob/grub.txt 2>&1 (from kodekloud look at this more)
    * Debug Shell 
        * systemctl enable --now debug-shell.service
        * Ctrl-Alt-F9 (while booting to get into tty9)
        * systemctl disable --now debug-shell.service 
    * resetting the root password 
        * enter grub menu while booting (ESC to grub - e to enter grub menu)
        * Linux kernel load line (starts with linux)
        * init=/bin/bash (to the end of the line - alt you can change the ro to rw to not have to automount)
        * mount -o remount,rw / (make the filesystem read writeable)
        * passwd root (change the root password)
        * touch /.autorelabel (selinux config)
        * exec /usr/lib/systemd/systemd (reload exec /sbin/init as an alt)
* Identify CPU/memory intensive processes and kill processes 
    * ps 
        * ps aux (show all with user information)
        * process commands wrapped in brackets (kernel processes running in privileged area)
    * top 
        * Shows most CPU intensive ones 
        * q to exit
        * arrows and pager buttons 
        * ps aux (all users)
        * ps fax (all forest)
        * ps lax (all long listing to see nice)
        * ps -U user (see processes for a specific user - ps -fU user)
        * ps u 1 (process ID - ps 1)
        * pgrep -a bash (might be helpful but look at both with regular grep)
    * Signals 
        * kill -L 
        * kill -9 PID 
        * kill PID (sends SIGTERM by default)
        * pkill bash (kill all processes under this name)
    * Background and foreground
        * Ctrl-C (stop a shell job or process running in the terminal)
        * Ctrl-Z (stop a process)
        * jobs
        * fg [n] (number or without number the last job)
        * bg [n] 
        * sleep 300 & (start it in the background)
    * lsof 
        * lsof -p PID (all open files for a specific process - might need sudo to see info)
        * lsof /var/log/messages (what is using this specific file might need sudo)
    * loginctl 
        * loginctl list-users (shows users)
        * loginctl list-sessions (show sessions)
        * logictl userstatus <UID> (show a tree of processes currently open by this user)
        * loginctl terminate-session (stop sessions)
        * loginctl terminate-user (stop users)
* Adjust process scheduling 
    * Nice and renice
        * Need sudo to lower value 
            * ps lax (long listing to see nice)
        * nice -n 11 bash (start the bash process with a nice value of 11)
        * renice 7 8209 (renice nice_value process_ID existing process renice)
* manage tuning profiles 
    * reapply_sysctl = 1 (in /etc/tuned/tuned-main.conf)
    * tuned-adm
        * tuned-adm list (list all profiles)
        * tuned-adm active (show active profile)
        * tuned-adm profile balanced (change to the balanced profile)
        * tuned-adm profile-info (get info about a profile no option shows current)
        * tuned-adm recommend 
        * tuned-adm verify
        * tuned-adm auto_profile
        * tuned-adm profile_mode
        * tuned-adm profile virtual-host powersave (two profile options)
    * Dynamic tuning 
        * /etc/tuned/tuned-main.conf
        * set Dynamic Tuning = 0 to 1 
    * Creating custom profiles 
        * Custom tuned profiles are stored as dirs in /etc/tuned
            * EACH profile should have a tuned.conf (containing the requested performance settings)
            * /etc/tuned/myprofile/tuned.conf 
                * tuned-adm profile myprofile 
    * sysctl
        * sysctl -a (all runtime paramters)
        * /etc/sysctl.d/*.conf (*) (.conf is required)
        * Create a file with vm.swappiness=29 in /etc/sysctl.d (reboot it will be persistent)
        * sudo sysctl -p /etc/sysctl.d/swap-less.conf (to load it right now)
* preserve system journals 
    * /etc/systemd/journald.conf (systemd journal settings)
        * create the dir /var/log/journal 
        * storage=auto (ensures that persistent storage it happening automatically)
            * persistent: stores journals in /var/log/journal
            * volatile: stores journals in the temp /run/log/journal dir
            * none: does not use any storage for the journal at all 
    * /etc/rsyslog.conf
        * rsyslog config authpriv.* shows where they are going (IM input modules)
    * journalctl 
        * journal deamon lets us analyze logs in a better way
        * journalctl /bin/sudo 
        * journalctl -u sshd.service (shows messages for sshd.service only/unit)
        * journalctl (all logs -e for end)
        * journalctl -f (follow mode)
        * journalctl -p (TAB TAB will show priorities you can use to search)
        * journalctl -b (shows current boot logs)
            * journalctl -b 0 (current boot - and can use other numbers)
        * journalctl --since "-1 hour"
        * journalctl -o (verbose)
        * logger -p err hello
    * /etc/logrotate.conf
        * systemctl list unit-files -t timer 
        * systemctl status logrotate.timer
        * systemctl cat logrotate.service 
        * /etc/logrotate.conf 
        * man logrotate (has great config examples)
* start, stop, and check the status of network services
    * ss and netstat
        * ss -ltunp
            * -l (listening)
            * -t (tcp connection)
            * -u (UDP connections)
            * -n (numeric values)
            * -p (processes - needs sudo)
            * ss -tunlp (can be reorders)
        * check status, start, stop services
            * systemctl status sshd.service (look at the status)
            * sudo systemctl stop sshd.service (stop the sshd service)
            * systemctl start sshd.service
            * systemctl disable sshd.service (disable at boot)
            * systemctl enable sshd.service (enable at boot)
        * ps and lsof 
            * ps PID (to look at the process)
            * lsof -p PID (look at open files for the service)
        * netstat -ltunp (almost the same as ss)
            * ss is the new version (good to know but stick with ss)
* securely transfer files between systems 
    * scp 
        * scp source target 
        * scp aaron@192.168.1.27:/home/aaron/myfile.tgz /home/aaron/myfile.tgz (copy file from remote to local)
        * scp /home/aaron/my_archive.tar aaron@192.168.1.27:/home/aaron/myarchive.tar (copy from local to remote)
        * scp aaron@1920.158.1.27:/home/aaron/familyphoto.jpg aaron@192.168.1.58:/home/aaron/familyphoto.jgp (copy between to remote systems source to target)
        * man scp
    * sftp (look at kode kloud notes for more basics)
    * rsync (sync files)
        * rsync -a path_to_local user@IP_address:/path_to_remote
        * rsync -a local_dir/ local_dir/
        * rsunc -a * server:/home/student/
        * Most common options 
            * -r (recursive sync the entire dir tree)
            * -l (sync symbolic links)
            * -p (preserve symbolic links)
            * -n (dry run before sync)
            * -a (archive mode)
            * -A (archive mode and also sync ACLs)
            * -X (sync SELinux context as well)


### Configure local storage 

* List, create, and delete partitions on MBR and GPT disk 
    * list partitions 
        * lsblk 
        * sudo fdisk --list /dev/sda (list partitions on sda)
        * Partition numbering 
            * /dev/sda2 (first hard disk (block device) second partition)
            * /dev/sdb1 (second hard disk (block device) first partition)
            * /dev/nvme0n1p1 (first partition on the first hard disk)
            * /dev/nvme0n3p2 (second partition on the third hard disk)
            * /dev directory 
    * cfdisk (and fdisk)
        * sudo cfdisk /dev/sdb 
            * GPT vs DOS (DOS is MBR in the cfdisk utility)
            * Free Space > NEW
            * Partition size: 8G (or whatever you want)
            * Left and right up and down
            * Resize a existing partition
            * Sort (reorder based on where they are on the storage device)
            * Type (to look at the partition type)
            * NEED to write (apply the changes - are you sure yes or no)
            * QUIT to exit and wipe all changes 
        * STILL LOOK AT FDISK and work with it abit
    * MBR and GPT
        * GPT is more often
        * Master Boot record
            * Extended and logical partitions (max partitions without extended and logical)
        * GPT (GUID partition table)
            * 128 partitions max, newer, more space for partitions
* create and remove physical volumes 
    * Read the digital ocean article 
    * pvcreate
* assign physical volumes to volume groups 
    * PV = physical volume 
    * VG = Volume group 
    * LV = Logical Volume 
    * PE = Physical Extent 
    * sudo lvmdiskscan (show what disk and partitions are available and used in LVM structure)
    * pvcreate /dev/sdb1 (pvcreate /dev/sdc)
    * sudo pvs (see the pv groups and info)
    * vgcreate vgdata /dev/sdb1 (create the volume group - vgcreate my_volume /dev/sdc)
        * vgcreate -s 8M vgdata /dev/sdb1 (create a VG with an extent size of 8MB)
    * vgextend my_volume /dev/sde (add an additional PV to an existing VG)
    * sudo vgs (look at the volume group info)
    * vgreduce my_volume /dev/sde (remove sde from the my_volume VG)
    * sudo pvremove /dev/sde (remove the PV all together)
* create and delete logical volumes 
    * sudo lvcreate -n lvdata -L 1G vgdata (create with name and -L=size)
        * sudo lvcreate --size 2G --name partition1 my_volume
        * sudo lvs (LV information)
    * sudo lvresize --entents 100%VG my_volume/partition1 (resize the partition to 100%)
        * sudo lvresize --size 2G my_volume/partition1 (resize it back to 2G)
    * lvdisplay 
    * sudo mkfs.xfs /dev/my_volume/partition1 (add a FS to the LV)
        * sudo lvresize --resizefs --size 3G my_volume/partition1 (resize with a fs on it)
    * lvremove (to remove a LV?)
    * IN FSTAB
        * /dev/vgdata/lvdata /lvdata vfat defaults 0 0 
* configure systems to mount file systems at boot by UUID or label 
    * blkid (should show the UUID)
    * labels created during creation of the file system (mkfs.xfs -L backup /dev/sda1)
        * xfs_admin -L cow /dev/sda1 (add the cow label to a device already created)
    * On fstab
        * UUID="UUID" /mount_point ext4 defaults 0 0 (quotes not required)
        * UUID=UUID none swap defaults 0 0 
        * LABEL=cow /xfs xfs defaults 0 0 
        * last number is for when the disk should be checked for errors (0 = never, 1 first, 2 after 1s are checked)
* Add new partitions and logical volumes, and swap to a system non destructively 
    * swap
        * lsblk 
        * blkid (to see UUID)
        * swapon --show (see swap space currently being used)
        * cfdisk (create a partition type swap)
        * sudo fdisk --list (-l) /dev/sda (see the partition information)
        * sudo mkswap /dev/vdb3 (create the swap filesystem)
        * sudo swapon --verbose /dev/vdb3
        * swapoff /dev/vdb3 (removing the swap)
        * /dev/sda7 (or UUID) none swap defaults 0 0 (in fstab)
            * findmnt --verify 
            * mount -a (or swapon -a in this case)
        * swapon -a (activate all swap enables all swap in fstab)
        * dd command 
            * fallocate -l 1G example.txt (make a 1G file called example.txt)
            * making a swap file from dd 
            * sudo dd if=/dev/zero of=/swapfile bs=1M count=2048 status=progress (shows status this would be 2 GB)
            * sudo chmod 600 /swapfile
            * mkswap /swapfile
            * swapon /swapfile
            * Not sure about fstab
    * Stratis
        * sudo dnf install stratisd stratis-cli (start and enable the service)
        * sudo stratis pool create my-pool /dev/vda
        * sudo stratis pool list (see information)
        * sudo startis blockdev (see block device info)
        * sudo stratis fs create my-pool myfs1 (create a filesystem)
        * sudo stratis fs (info about the fs)
        * FSTAB
            * create a mount point if needed 
            * /dev/stratis/mypool/myfs /mnt_point xfs x-systemd.requires=stratisd.service 0 0 
            * mount -a (findmnt --verify, reboot)
        * add storage device to the stratis pool 
            * sudo stratis pool add-data my-pool /dev/vdd
        * filesystem snapshot with stratis 
            * sudo stratis fs snapshot my-pool myfs1 myfs1-snapshot 
            * sudo stratis fs rename my-pool myfs1 myfs1-old (rename the fs1 filesystem)
            * sudo stratis fs rename my-pool myfs1-snapshot my-fa1 (rename the snapshot to my-fs1)
            * sudo umount /mnt_point 
            * sudo mount /mnt_point (remount the newly renamed fs)

### Create and configure file systems 

* create, mount, unmount, and use vfat, ext4, and xfs filesystems
    * mkfs.ext4
    * mkfs.xfs
    * mkfs.vfat 
    * man mkfs.xfs
    * xfs_admin (admin xfs fs)
    * tune2fs (admin ext fs ext4)
    * mkfs.xfs -L (create the label as well as the FS)
    * maybe look at lvmvdo
* mount and unmount network file systems using NFS
    * Server config (may not be needed
        * dnf install fns-utils 
        * mkdir -p /nfsdata /home/ldap/ldapuser{1..9}
        * echo "/nfsdata *(rw,no_root_squash)" >> /etc/exports (*)
        * echo "/home/ldap *(rw,no_root_squash)" >> /etc/exports (*)
        systemctl enable --now nfs-server
        * for i in nfs mountd rpc-bind;do firewall-cmd --add-service $i --permanent;done
        * firewall-cmd reload
    * Make sure nfs-utils are installed
    * shoudmount -e nfserver (show exports available)
    * mount nfsserver:nfsdata /mnt (mounting the specific share nfs data)
* configure autofs 
    * dnf install -y autofs 
    * /etc/auto.master
        * /nfsdata /etc/auto.nfsdata (the NFS share - and the config file auto.nfsdata)
    * /etc/auto.misc (provides some examples)
        * /etc/auto.nfsdata 
            * files -rw nfsserver:/nfsdata 
    * systmctl enable --now autofs 
    * Automount for home dirs 
        * wildcard
        * * -rw nfsserver:/home/ldap/&
        * showmount -e nfsserver
        * vim /etc/auto.master
        * /homes /etc/auto.homes
        * vim /etc/auto.homes 
            * * -rw nfsserver:/home/ldap/&
        * systemctl restart autofs 
* extend existing logical volumes 
    * lvextend
        * lvextend -r -L +1G (to grow the LVM including the filesystem its hosting)
        * shrinking is possible on ext4 not on xfs
        * vgextend vgfiles /dev/sde2 (add a new PV to the VG)
        * lvextend -r -l +50%FREE /dev/vgfiles/lvfiles 
        * DEMO sanders
            * 2 partitions create with a size of 1G each lvm partitions type
            * vgcreate vgfiles /dev/sde1
            * lvcreate -l 255 -n lvfiles /dev/vgfiles
            * mkfs.ext4 /dev/vgfiles/lvfiles
            * df -h 
            * vgs 
            * vgextend vgfiles /dev/sde2 (add a new PV to the VG)
            * lvextend -r -l +%0%FREE /dev/vgfiles/lvfiles
        * Remove a VG from a PV 
            * pvmove -v /dev/sdf2 /dev/sdf1 (move all used extents from sdf2 to sdf1)
            * vgreduce vgdemo /dev/sdf2
* Create and configure set GID directories for collaboration
    * Config shared group dirs
        * chmod g+s dir
        * chmod 2770 mydir (assign sGID)
    * Additional info 
        * SUID
            * 4 (numeric value)
            * u+s (relative value)
            * User executes file with permissions of file owner
            * No meaning on dirs
        * SGID
            * 2 (numeric value)
            * g+s (relative value)
            * User executes file with permissions of group owner (on files)
            * Files created in dir get the same group owner (on dirs)
        * Sticky bit
            * 1 (numeric value)
            * +t (relative value)
            * No meaning on files
            * Prevents users from deleting files from other users (on dirs)
* Diagnose and correct file permission problems 
    * ls -l
    * chmod/chown
        * chown user:[group] file (to set user-ownership)
        * chgrp group file (to set group ownership)
        * chown lisa:sales newfiles/ (change user and group)
        * chown :sales newfile/ (change group ownership with chown)
        * chown steve newfile/ (just change the user owner only)
    * setfacl (might not be needed)
        * sudo setfaxl --modify user:aaron:rw exampleFile
        * Presence of ACLs indicated by a plus sign in the permission listing 
        * sudo setfacl --modify mask:r-- exampleFile
        * sudo setfacl --modify group:whell:rw exampleFile
        * sudo setfacl --modify user:aaron:--- exampleFile
        * sudo setfacl --remove user:aaron exampleFile
        * sudo setfacl --remove group:wheel exampleFile
        * sudo setfacl --recursive -m user:aaron:rwx dir1/ 
        * sudo setfacl --recursive --remove user:aaron dir1/
    * Append only and immutable attributes (might not be needed)
        * sudo chattr +a newfile (now can only append to)
        * sudo chattr -a newfile (remove append)
        * sudo chattr +i newfile (immutable unmodifiable -- even root cannot delete or alter the file)
        * lsattr newfile (view file attributes)
        * sudo chattr -i newfile (remove)
    * getfacl (might not be needed)
        * getfacl exampleFile
    * umask
        * /etc/bashrc 
        * ~/.bashrc (userspecific)
        * source ~/.bashrc (reload the bashrc)
    * Default permissions for: Files = 666 and Dirs = 777 (umask is subtracted from this)
    * first digit is the user permissions
    * second digit refers to the group permissions
    * Last refers to default permissions set for others
    * Deafult umask setting of 022 gives 644 to all new files and 755 for all new dirs
    * Table
        * 0
            * Applies rw to files
            * Everything to dirs
        * 1
            * rw to files
            * rw to dirs
        * 2
            * r to files
            * rx to dirs
        * 3
            * r to files
            * r to dirs
        * 4
            * w to files
            * wx to dirs
        * 5
            * w to files
            * w to dirs
        * 6
            * nothing to files
            * x to dirs
        * 7
            * nothing to files
            * Nothing to dirs
 

### Delpoy, configure, and maintain systems 

* Schedule tasks using at and cron
    * Using cron
        * Cron service checks its config every minute
            * /etc/crontab (main config)
            * /etc/cron.d (drop in files)
            * /etc/cron.{hourly,daily,weekly,monthly} (used as a drop in for scripts that need to be scheduled on a regular basis)
            * Make sure execute bit is set
        * crontab -e (creating user specific cron jobs)
            * crontab -l (to see the crontab for current user: sudo crontab -l for root)
            * crontab -e -u jane (edit janes crontab)
            * crontab -r (remove crontab all together)
            * crontab -r -u jane (remove janes crontab)
        * Understanding cron time specification
            * minute, hour, day_of_month, month, day_of_week
                * minute (0-59)
                * hour (0-23)
                * day of month (1-31)
                * month (1-12) OR jan,feb,mar,apr
                * day of week (0-6) (sunday=0 or 7) or sun,mon,tue,wed,thu,fri,sat
                * Others
                    * * (match all possible values)
                    * , (match multiple values 15,45)
                    * - (range of values 2-4)
                    * / (specifies steps */4 = every four hours (*))
                * which touch (to find the full path)
                    * USE THE FULL path
                * * * * * * user-name command_to_be_executed
            * 0 * * dec 1-5 (run cron job every monday thru friday on minute zero in december)
            * 10 * * * * (every 10 minutes)
                * 10 * * * * logger HELLO (full command job)
            * /etc/crontab (nice syntax example for time specification)
            * Do not edit /etc/crontab directly, use /etc/cron.d instead
        * anacron
            * Not a specific time (have a job that needs to be run but do not care when)
            * takes care of jobs in /etc/cron.{hourly,daily,weekly,monthly}
                * No extension on the script 
                * make sure its executable - place it in one of the cron.daily dirs
                * config in /etc/anacrontab
            * anacron -T (test the syntax)
    * at 
        * atd (service that must be running to run jobs only ONCE)
        * at time (to schedule a job)
            * Type one or more job specifications in the at interactive shell
            * Ctrl-D to close this shell
            * at 15:00 (24 hour time - 3pm)
            * at 'August 20 2022'
            * at 'now + 30 minutes'
            * at 'now + 3 hours'
            * at 'now + 3 weeks'
        * atq (for a list of jobs currently scheduled)
        * at -c 20 (id from atq to see what the job is specifically doing)
        * atrm ID (remove jobs from the list)
        * at teatime (4pm at the devs)
            * touch /tmp/teatime (in the file)
            * ctrl-d (to close the shell) 
            * atq (to look at the jobs)
* start and stop services and configure services to start automatically at boot 
    * Checking out systemd units 
        * Great tab completion
        * systemctl -t help 
        * systemctl list-units -t timer
        * systemctl list-units 
        * systemctl list-unit-files
        * systemctl list-units --type service --all (list all service unit files)
    * Starting and Stopping services 
        * sudo systemctl start sshd.service (start a service - bring it up)
        * sudo systemctl stop sshd.service (stop a service)
        * sudo systemctl restart ssh.service (restart - can be disruptive)
        * sudo systemctl reload sshd.service (reload the config without stoping/starting)
        * sudo systemctl reload-or-restart sshd.service (reload if supported restart if not)
        * sudo systemctl is-enabled sshd.service (see if its enabled or not)
        * sudo systemctl disbale sshd.service (disable will not come up on boot)
        * sudo systemctl enable sshd.service (enable to start at boot)
        * sudo systemctl enable --now sshd.service (enable and start the service)
        * sudo systemctl disable --now sshd.service (disable and stop the service)
        * sudo systemctl mask atd.service (prevent other services from starting this service - can not start or enable service)
        * sudo systemctl unmask atd.service (unmask the service)
    * editing services (quick)
        * sudo systemctl cat sshd.service (see the service file)
            * systemctl show httpd.service (show available parameters)
        * sudo systemctl edit httpd.service (being up the editor: export EDITOR=/usr/bin/vim to get vim)
        * sudo systemctl revert httpd.service (revert to vendor config)
        * sudo systemctl list-dependencies UNIT (to see dependencies for any unit)
* configure systems to boot into specific targets automatically 
    * systemctl get-default
    * systemctl set-default multi-user.target (sudo)
    * rebooting
    * sudo systemctl isolate graphical.target (change directly into the graphical from multi-user)
        * this does not change the default however multi-user will still be the default
    * Useful targets
        * emergency.target
        * read only file system (mount -o remount,rw /)
        * rescue.target (few more than emergency and root must have passwd)
* configure time service clients 
    * hwclock
        * hwclock --systohc
        * hwclock --hctosys
        * date (command to show and set time)
        * timedatectl (used to manage time and time zone config)
    * setting time with timedatectl 
        * timedatectl status (show all time properties currently used)
        * timedatectl list-timezone (list all timezones)
        * timedatectl set-time (used to change the time)
        * timedatectl set-timezone (used to change the timezone)
        * timedatectl set-ntp (enables or disables NTP time sync)
    * managing a NTP client
        * chronyd (default RHEL 9 NTP service)
            * dnf install chrony (install chrony)
            * systemctl status chronyd.service 
            * sudo timedatectl set-ntp true (in case timedatectl status shows no good and chronyd is active)
        * /etc/chrony.conf (specify synch parameters)
        * pool 2.rhel.pool.ntp.org iburst (configs a pool of NTP servers)
            * server myserver.example.com (config a single NTP time source)
            * pool pool.ntp.org iburst (for a pool)
            * iburst (to permit fast sync)
        * systemctl restart chronyd (restart the service after config change)
        * chronyc sources (verify proper sync)
* install and update software packages from red hat network, a remote repo, or from the local system
    * Managing RPM packages
        * rpm -qa (show all packages that are currently installed)
        * rpm -qf filename (shows from which package filename was installed)
        * rpm -ql (list files installed from a package)
        * rpm -q --scripts (show scripts executed while installing the package)
        * rpm -q --changelog (shows the change log for a package)
        * rpm2cpio mypackage-1.0.rpm | cpio -tv (show contents of the package)
        * rpm2cpio mypackage-1.0.rpm | cpio -idmv (extract package contents to the current dir)
    * Managing packages with dnf 
        * sudo dnf repolist 
            * sudo dnf repolist --all
            * sudo dnf repolist -v (verbose option)
            * sudo subscription-manager repos --enable Repo_ID
            * sudo subscription-manager repos --disable Repo_ID
        * dnf list 'selinux*' (*) (list installed and available packages matching search)
        * dnf search seinfo (search)
        * dnf search all seinfo (search summary?)
        * dnf provides */Containerfile (*) (searches package file list for the package that provides a specific file)
        * dnf info (shows information aboutt the package)
        * dnf install (install packages as well as any dependencies)
        * dnf remove (removes package as well as dependencies)
        * dnf check-update (check-upgrade as well)
        * dnf update (compares current package version with package version listed in the repo and updates)
        * dnf update kernel (install the new updated kernel keep old one as backup)
        * Get a package via curl or wget 
            * sudo dnf install ./file_path
            * sudo dnf remove nomachine
            * sudo dnf autoremove (dependencies that are left behind when packages are removed)
        * History 
            * dnf history 
            * dnf history undo 2 (inversion conflicts might not be easy/possible)
    * Groups and modules 
        * dnf group list hidden (dnf group list also shows groups and hidden groups (all))
        * dnf group info <groupname> (see packages within a group)
        * Mandatory and default packages are installed 
            * --with-optional (to install optional packages also)
        * Spaces for group name so quotes are important
        * Modules 
            * sudo dnf module list (show modules available)
            * sudo dnf module list php (show specific information for specific module
            * sudo dnf module install nodsjs:14/development (install version 14 development profile)
            * sudo dnf module list install nodejs (should see 14 now)
            * sudo dnf module reset nodejs (reset the profile)
    * REPOs - RH Network, remote repo, or local system
        * Setting up repo access *Important* 
            * /etc/yum.repos.d/ (REPO files .repo files)
            * Manual Repo file 
                * /etc/yum.repos.d/repo.repo
                * [AppStream] (required short name)
                * name=Appstream (long name not required but needed)
                * baseurl=file:///repo/BaseOS (file where the repo and packages are)
                    * baseurl=https://download.docker.com/linux/rhel/gpg
                    * ftp://path/to/repo
                    * http:// user : password @www.example.com/repo/
                * enabled=1 (needs to be enabled)
                * gpgcheck=1 (gpgcheck)
                * gpgkey=https:download.docker.com/linux/rhel/gpg (gpg key to look at)
                * STEPS: 
                    * create the file manually (/etc/yum.repos.d/whatever.repo)
                        * Make sure the names, baseurl, enabled, and gpg is set correctly)
                        * Then you should be able to see them via dnf repolist (dnf repolist --all)
                        * enable and disable (dnf repolist --enable Repo_ID - dnf repolist --disable Repo_ID)
            * Using dnf config-manager
                * man dnf-config-manager (man dnf.conf maybe helpful)
                * dnf config-manager --enable name_of_repo (ACCESS REPO thru subscription manager (no on exam likely)
                * sudo dnf config-manager --add-repo="file:///repo/AppStream"
                * Good to know but stick with manual creation on exam
    * Subscription manager 
        * subscription-manager register (register with RHEL dev account)
        * subscription-manager attach (subscription-manager --attach auto also?)
        * subscription-manager unregister
        * /etc/pki/product (indicates the installed RHEL products
        * /etc/pki/consumer (IDs the RH account for registration)
        * /etc/pki/entitlment (indicates which subscription is attached)
        * rct (command to check current entitlements)
        * rct cat-cert /etc/pki/entitlements/ID.pem 
* modify the system bootloader 
    * Modifying persistent grub2 parameters
        * /etc/default/grub (config file to edit)
        * after making changes compile changes to grub.cfg
            * grub2-mkconfig -o /boot/grub2/grub.cfg
            * grub2-mkconfig -o /boot/efi/EFI/redhat/grub.cfg
            * lsblk to see if boot partition is boot/efi (that means efi and the second option is needed)
        * sudo grub2-install /dev/vda > /home/bob/grub.txt 2>&1 (install grub2 onto a device)


### Managing basic networking 
* configure IPv4 and IPv6 addresses 
    * Network config commands 
        * ip link show (ip link | ip -s link (show link properties))
        * ip addr show (ip a - shows IP address)
        * ip route show (ip route | ip r (show default route/route properties))
    * NetworkManager 
        * /etc/NetworkManager/system-connections
        * systemd service that manages network config 
        * /etc/sysconfig/network-scripts/ (legacy files still supported but deprecated)
        * nmcli general permissions
    * Hostname and DNS
        * /etc/hosts (hostname file)
            * IP_address name_to_resolve (192.168.0.1 dbserver (now ping and ssh to the name))
        * /etc/resolv.conf (for DNS resolution)
            * nameserver IP_address 
        * /etc/nsswitch.conf (determines the order of hostname resolution)
    * Configure IPv4 and IPv6 addresses 
        * nmtui
            * options 
                * edit a connection
                * activate a connaction
                * change hostname
            * setting hostname here as well
            * reboot for changes 
                * sudo nmcli device reapply enps03 (to reapply changes instantly)
    * Device names 
        * BIO device name 
            * em[1-N] (embedded NICs)
            * eno[nn] (for embedded NICs)
            * p<slot>p<port> (for NICs on the PCI bus)
            * If driver does not reveal network device properties classical naming is used (eth0, eth1, so on)
    * NMCLI (just in case - only one connection can be active per device)
        * nmcli con show (show current connections)
        * nmcli dev status (show current network devices)
        * nmcli con add con-name mynewconnection ifname ens33 ipv4.addresses 10.0.0.10/24 ipv4.gateway 10.0.0.1 ipv4.method manual type ethernet
        * nmcli con up mynewconnection (activate the new connection
        * nmcli con show mynewconnection (connection settings)
        * nmcli con mod (modify connection settings AUTO complete)
        * nmcli con reload (reload the modified connection)
        * Config Routes with NMCLI
            * sudo ip route add 192.168.0.0/24 via 10.0.0.100
            * sudo ip route del 192.168.0.0/24
            * sudo ip route add default via 10.0.0.100 (del instead of add to delete)
            * sudo nmcli connection modify enp0s3 +ipv4.routes "192.168.0.0/24 10.0.0.100"
            * sudo nmcli connection modify enp0s3 -ipv4.routes "192.168.0.0/24 10.0.0.100" (delete)
            * sudo nmcli device reapply enp0s3 (reapply the settings)
* Configure hostname resolution
    * Hostname and DNS
        * /etc/hosts (hostname file)
            * IP_address name_to_resolve (192.168.0.1 dbserver (now ping and ssh to the name dbserver))
        * /etc/resolv.conf (for DNS resolution)
            * nameserver IP_address (nameserver 192.169.0.1 (can be multiples))
        * /etc/nsswitch.conf (determines the order of hostname resolution, files dns)
    * hostnamectl set-hostname nfserver (change the hostname to nfserver)
        * Can be set through nmtui as well 
* Configure network services to start automatically at boot 
    * Network manager 
        * sudo systemctl status NetworkManager.service (sudo systemctl status NetworkManager (capital is important))
        * sudo dnf install NetworkManager
            * sudo systemctl enable --now NetworkManager (enable and start the service)
    * Auto start at boot 
        * nmcli connection show (see the connections)
        * Name of the connection
        * sudo nmcli connection modify enp0s3 autocnnect yes (name of the connection enp0s3)
    * Troubleshooting
        * ip route (show route)
        * ip -6 route (show IPv6 route)
        * tracepath example.com (show entire networking path)
            * tracepath6 example.com (does the same for IPv6 path)
        * ping -c 4 myserver (ping 4 times then stop(
        * ping6 ipv6_address (test connectivity)
* restrict network access using firewall-cmd/firewall
    * Firewalld - firewall-cmd command 
        * Understanding firewalld
            * Firewalld uses different components to make firewalling easier 
            * Service: main component contains one or more ports as well as optional kernel modules that should be loaded
            * Zone: default config to which network cards can be assigned to apply specific settings 
            * Ports: optional elements to allow access to specific ports
        * Firewall-cmd command
            * systemctl status firewalld
            * firewall-cmd --list-all (list all currently configed)
            * firewall-cmd --get-services (all services/service names)
            * --permanent (important)
            * firewall-cmd --add-service http
            * firwall-cmd --add-service http --permanent 
                * firewall-cmd --add-port=80/tcp (adding a port similar to --add-service=http)
            * sudo firewall-cmd --remove-service=http (remove the service or port number --remove-port=)
            * firewall-cmd --get-default-zone (look at default zone - will usually be public)
            * firewall-cmd --set-default-zone=public (set the default zone)
            * sudo firewall-cmd --info-service=cockpit (get info about a specific service)
            * Trusted zone
                * sudo firewall-cmd --add-source=10.11.12.0/24 --zone=trusted (add an IP address to a trusted zone)
                * firewall-cmd --get-active-zones (see the zones that are filtering traffic)
                * sudo firewall-cmd --remove-source=10.11.12.0/24 --zone-trusted
            * sudo firewall-cmd --runtime-to-permanent (make current rules permanent - or rerun the command with --permanent)

### Manage users and groups 

* create, delete, and modify local user accounts 
    * /etc/passwd (user file)
    * /etc/shadow (password file)
    * useradd: create user accounts 
        * sudo useradd john (create a new user named john)
        * sudo useradd --system sysacc (add a system account)
        * useradd -D (defaults)
        * sudo useradd -s /bin/othershell -d /home/otherdir john (create user with different default shell and home dir)
        * sudo useradd -s /bin/othershell john (create user john with non default shell)
        * sudo useradd -u 1100 smith (create user with custom UID)
        * ls -ln (numeric uid for permissions)
    * usermod: modify user accounts 
        * usermod -aG wheel myuser (to add myuser to the group wheel (wheel group is default sudoers))
        * sudo usermod -d /home/otherdir -m john (change the home dir for john and move it)
        * sudo usermod -l jane john (change the username from john to jane)
        * sudo usermod -s /bin/othershell jane (change the login shell)
        * sudo chage -d 0 jane (expire the password - must be changed next login)
            * sudo chage -d -1 jane (unexpire password)
            * sudo chage -M 30 jane (expire password in 30 days) 
            * sudo chage -M -1 (never expire)
            * sudo chage -l jane (look at the settings --list)
            * id and whoami commands 
    * userdel: delete user accounts
        * sudo userdel -r john (delete and remove home dir and files)
    * Manage user default settings 
        * useradd -D (list or change defaults)
        * /etc/default/useradd (applies to useradd only)
        * /etc/login.defs (system wide)
            * some important options use as password aging controls 
        * /etc/skel (files that are created in user home dir upon creation)
* change passwords and adjust password aging for local user accounts 
    * passwd (change password for user: passwd linda, passwd root, by itself will change current user)
    * /etc/login.defs (changing password age controls here PASS_MAX_DAYS)
    * Limit access 
        * usermod -L anna (lock user anna account)
        * usermod -U anna (unlock user anna account)
        * usermod -e 2032-01-01 bill (expire bill user account 01-01-2032)
            * YEAR-MONTH-DAY
            * sudo usermod -e "" bill (remove the expiration date)
        * sudo passwd -u root (passwd -l (to lock))
        * /sbin/nologin (as the shell for non interactive users)
            * usermod -s /sbin/nologin myapp (change the shell for myapp user to /sbin/nologin)
        * if passwd in /etc/shadow starts with ! than it is locked 
            * !! in /etc/shadow means the pw has never been set 
* Create, delete, and modify local groups and group membership 
    * /etc/group
    * Primary vs secondary groups 
        * can only have one primary GID 
        * Can have as many secondary as you want 
    * group management 
        * sudo groupadd developers (add group called developers)
        * sudo usermod -aG developers steve (add steve to the developers group)
        * groups steve (see what groups steve is a part of)
        * sudo usermod -g developers steve (change steves primary group to developers)
        * sudo groupmod -n programmers developers (change developers to programmers --new-name)
        * sudo groupdel programmers (will throw error if it is somebodies primary group)
        * gpasswd (alt to add to groups)
            * sudo gpasswd -a john developers (add john to the developers group)
            * sudo gpasswd -d john developers (remove user john from the developers group)
* config superuser access 
    * sudo -i (get root shell with sudo access)
    * su - (switch to root requires root password)
    * sudo passwd root (change the root password)
    * sudo passwd -u root (unlock the root password)
    * sudo passwd -l root (lock the root passwd --lock (make sure you have sudo access or can lock yourself out)
    * /etc/sudoers 
        * config file for sudo access 
        * default wheel group 
            * usermod -aG wheel steve (add steve to the wheel group)
        * visudo (edit sudoers file)
        * %wheel ALL=(ALL) ALL
        * %wheel ALL=(ALL) NOPASSWD: ALL (do not do but no password for all sudo commands)
        * Defaults timestamp_type=global,timestamp_timeout=60 (add an hour to the cached token for sudo password)
        * Should use drop in files 
        * lisa ALL=/bin/mount /dev/sdb, /bin/umount /dev/sdb (Lisa can mount and umount the specific args /dev/sdb)
        * %users ALL=/usr/bin/passwd, ! /usr/bin/passwd root (users in group users can change passwords BUT NOT change the password for root)
            * adding a file to /etc/sudoers.d/linda (with the specific commands)

### Manage security 

* Configure firewall settings using firewall-cmd/firewalld 
    * Firewalld - firewall-cmd command
        * Understanding firewalld
            * Firewalld uses different components to make firewalling easier
            * Service: main component contains one or more ports as well as optional kernel modules that should be loaded
            * Zone: default config to which network cards can be assigned to apply specific settings
            * Ports: optional elements to allow access to specific ports
        * Firewall-cmd command
            * systemctl status firewalld
            * firewall-cmd --list-all (list all currently configed)
            * firewall-cmd --get-services (all services/service names)
            * --permanent (important)
            * firewall-cmd --add-service http
            * firwall-cmd --add-service http --permanent
                * firewall-cmd --add-port=80/tcp (adding a port similar to --add-service=http)
            * sudo firewall-cmd --remove-service=http (remove the service or port number --remove-port=)
            * firewall-cmd --get-default-zone (look at default zone - will usually be public)
            * firewall-cmd --set-default-zone=public (set the default zone)
            * sudo firewall-cmd --info-service=cockpit (get info about a specific service)
            * Trusted zone
                * sudo firewall-cmd --add-source=10.11.12.0/24 --zone=trusted (add an IP address to a trusted zone)
                * firewall-cmd --get-active-zones (see the zones that are filtering traffic)
                * sudo firewall-cmd --remove-source=10.11.12.0/24 --zone-trusted
                * * sudo firewall-cmd --runtime-to-permanent (make current rules permanent - or rerun the command with --permanent)
* manage default permissions
    * Make sure to review the File permission section for others
    * umask
        * /etc/bashrc
        * ~/.bashrc (userspecific)
        * source ~/.bashrc (reload the bashrc)
    * Default permissions for: Files = 666 and Dirs = 777 (umask is subtracted from this)
    * first digit is the user permissions
    * second digit refers to the group permissions
    * Last refers to default permissions set for others
    * Deafult umask setting of 022 gives 644 to all new files and 755 for all new dirs
    * Table
        * 0
            * Applies rw to files
            * Everything to dirs
        * 1
            * rw to files
            * rw to dirs
        * 2
            * r to files
            * rx to dirs
        * 3
            * r to files
            * r to dirs 
        * 4
            * w to files
            * wx to dirs
        * 5
            * w to files
            * w to dirs
        * 6
            * nothing to files
            * x to dirs
        * 7
            * nothing to files
            * Nothing to dirs
* configure key based authentication for ssh
    * Configs 
        * /etc/ssh/sshd_config
            * Daemon config 
            * man sshd_config 
            * Port 22 
            * PermitRootLogin
            * PubKeyAuthentication
            * PasswordAuthentication
            * X11Forwarding
            * AllowUsers (specific users)
        * /etc/ssh/ssh_config (main client config)
            * /etc/ssh/ssh_config.d (drop in for client config)
            * ~/.ssh
                * adding a config file for specific users 
                * ~/.ssh/config 
                * Host centos
                    * Hostname 1.2.3.4
                    * Port 22 (not needed)
                    * User aaron
                    * chmod 600 (for the config file)
                * man ssh_config
    * Keys
        * ssh-keygen (create the pub/private key)
            * should see the keys at ~/.ssh
        * ssh-copy-id user@server
            * Moves the pub key to the user home dir ~/.ssh/authorized_keys
        * Edit the authorized_key file manually 
            * Copy the public key 
            * ssh over to the server and edit the authorized key file
            * known_hosts file
                * ssh-keygen -R IP_of_server (remove the fingerprint from known hosts)
                * Delete entire file to remove all finger prints
    * Caching passphrase 
        * ssh-agent /bin/bash
        * ssh-add 
* set enforcing and permissive modes for SELinux
    * getenforce (show current state)
    * setenforce (toggles between enforcing and permissive)
    * /etc/sysconfig/selinux (to manage the default state of SELinux)
    * While booting 
        * enforcing=0 (will start in permissive mode)
        * enforcing=1 (will start in enforcing mode)
        * selinux=disable (disable)
        * selinux=1 (enable)
    * ls -Z (to see the context on files)
        * id -Z (security context for the user)
        * sudo semanage login -l (see how security context mapping is done)
        * sudo semanage user -l (roles that each user can have on the system)
    * ps axZ (process with SELinux)
* restore default file contexts 
    * semanage fcontext -a (se a new context label)
    * semanage fcontext -m (modify an existing context label)
    * restorecon (enforce the policy setting on the filesystem)
    * touch /.autorelabel (relabel the files to the context specified in the policy)
    * man semanage-fcontext (documentation)
    * semanage fcontext -l -C (show settings that have changed in the current policy)
    * man pages for selinux-policy-doc
    * semanage fcontext -a -t http_sys_content_t "/web(/.*)? (*)
    * restorecon -Rv /web
* manage SELinux port labels
    * semanage port -a -t ssh_port_t -p tcp 2022
    * man semanage-port 
* Use boolean settings to modify system SELinux settings 
    * semanage boolean -l (overview of booleans)
    * getsebool -a (overview of bools)
    * setsebool -P boolean [on|off]
    * semanage boolean -l -C (see all booleans that have a non default setting)
* Diagnose and address routine SELInux policy violations 
    * grep AVC /var/log/audit/audit.log (see raw audit messages)
    * journalctl | grep sealert 
        * taking the message with UUID and run it to see the advice
        * sealert -l UID
    * troubleshooting 
        * If you think SELinux is to blame turn to permissive and test 
        * dnf install selinux-policy-doc
        * dnf provides */sealert (may need to restart auditd or machine to make functional)

### Manage containers 

* find and retrieve container images from a remote registry 
    * /etc/containers/registries.conf (registry access config file)
        * ~/.config/containers/registries.conf (user specific config)
    * podman search (search the registers for images)
    * podman pull (pulls an image from a registry)
    * podman images (list images)
    * podman build -t mymap . (build from a containerfile)
        * podman image (should show there)
    * podman info 
* inspect container images 
    * podman inspect (show container or image details)
* perform container management using commands such as podman and skopeo
    * Common podman commands
        * podman search (searches the registries for images)
        * podman run (runs a container)
            * podman run -d --name sleepy docker.io/redhat/image
            * podman run -it 
        * podman stop (stops a currently running container)
        * podman ps (shows information about containers)
            * podman ps -a
        * podman build (builds an image from a containerfile)
        * podman images (lists images)
        * podman inspect (shows container or image details)
        * podman pull (pulls an image from the registry)
        * podman exec (executes a command in a running container)
        * podman rm (removes a container)
    * skopeo
        * skopeo inspect image (inspect remote images)
        * skopeop inspect --config image
        * skopeo copy docker://quay.io/image docker://regiry.kodekloud.com/image
        * skopeo copy oci:busybox_ocilayout:latest dir:myemptydir (copy locally)
        * skopeo delete docker://localhost:500/localimage
        * skopeo sync --src docker --dest dir registry.kodekloud.com/busybox /media/usb
        * man skopeo
* perform basic container management such as running, starting, stopping, and listing running containers 
* Run a service inside a container 
    * Mapping ports and config variables 
        * podman run --name mydb quay.io/centos/mariadb
        * podman run --name mydb -e MYSQL_ROOT_PASSWD=password quay.io/centos/mariadb
    * Port access/config application access 
        * podman run -d -p 8080:80 registry.access.redhat.com/ubi9/nginx
        * podman port -a (display information for all running containers)
        * sudo firewall-cmd --add-port=8080/tcp --permanent
* configure a container to start automatically as a systemd service 
    * Running systemd services as a user (need a container running)
        * loginctl enable-linger (start user services for a specific user requires root)
            * loginctl enable-linger linda (enabled linger)
            * loginctl show-user linda (verify it is enabled)
            * loginctl disable-linger linda (disbale)
        * Make dir 
            * mkdir ~/.config/systemd/user (creating the dir for the systemd file)
            * podman generate systemd --name myweb --files --new (need to be in the .config/systemd/user dir - generate the files in that dir (does the container need to be running?))
            * /etc/systemd/system (to generate a service file for a root container)
            * podman generate (--new is important)
                * WantedBy edit
                * WantedBy=default.target
            * systemctl --user (only works when logged in on console or ssh and does not work in sudo or su)
                * ssh user@localhost (can not su or sudo to that user - so need to ssh or console the user)
                * systemctl --user daemon-reload (reload the daemon)
                * systemctl --user enable myapp.service (requires linger enable the service)
                * systemctl --user start myapp.service (start the service)
                * systemctl --user status myapp.service (see the status of the service)
            * verify 
                * ps fax | grep user (logged into a different user to verify - or search ps command)
                * ps faux | less (user information)
        * man podman-generate-systemd
            * man podman-generate
* attach persistent storage to a container 
    * podman run -d ... -v /hostdir:/containerdir
    * Rootless 
        * find the UID of the user that runs the main application
            * podman inspect imagename (probably better)
            * podman exec containername grep username /etc/passwd 
        * Next
            * podman unshare chown nn:nn directoryname (set the container UID as teh owner of the dir on the host)
            * directoryname (must be in the user home dir because it would not be a part of the user namespace)
        * podman unchare cat /proc/slef/uid_map (verify mapping)
        * ls -ld /directoryname (verify the mapped user is the owner on the host)
        * SELinux config 
            * :Z (option to auto set the context 
            * podman run ... -v /home/student/mydb:/var/lib/mysql:Z 




