# Quick review of important points 

* Pulled together from RHCSA Cert Guide 
* Meant to be a quick and easy reference point compared to more comprehensive notes and labs in prep for the RHCSA 

## Basic/Essential Tools 

* Redirection
    * > (same as 1>)
        * Redirects STDOUT
        * Overwrites the file being written too 
    * >> (same as 1>>)
        * Redirects STDOUT in append mode
    * 2> (Redirects STDERR)
    * 2>&1
        * Redirects STDERR to the same destination as STDOUT
        * Combined with normal output redirection
        * ls > out_file 2>&1 
    * < (same as 0<)
        * Redirects STDIN
* History 
    * history (shows all)
    * Ctrl r (Search something from history Ctrl r again to move between search results)
        * Note searching via vi commands (set -o vi)
    * !number (automatically executes the command)
    * !sometext (executes automatically)
    * history -d number (remove specific history number)
    * history -c (clear history)
    * history -w (remove current history (history -c) and the content of the .bash_history file)
* Environment Configuration Files 
    * /etc/profile
        * this is the generic file that is processed by all users upon login
    * /etc/bashrc
        * This file is processed when subshells are started
    * ~/.bash_profile
        * In this file, user specific login shell variables can be defined
    * ~/.bashrc
        * In this user specific file, subshell variables can be defined
* Using /etc/motd and /etc/issues
* Finding Help 
    * man -f keyword 
    * apropos 
    * Man page categories 
        * 1: Executable programs or shell commands 
        * 5: File Format and conventions
        * 8: System admin commands 
    * mandb (update man database)
    * info (pinfo)
    * /user/share/doc

## Essential File Management Tools 

* FHS (Filesystem Hierarchy Standard)
    * man 7 file-hierarchy
    * /
        * Specifies the root dir. This is where the file system starts
    * /boot
        * Contains all files and dirs that are needed to boot the linux kernel
    * /dev
        * Contains device files that are used for accessing physical devices. This dir is essential during boot
    * /etc
        * Contains config files that are used by programs or services on your server
        * Essential during boot
    * /home
        * Used for local user home directories
    * /media, /mnt
        * Contains dirs that are used for mounting devices in the file system tree
    * /opt
        * Used for optional packages that may be installed on your server
    * /proc
        * Use by the proc file system
        * This is a file system structure that gives access to kernel information
    * /root
        * specifies the home dir of the root user
    * /run
        * contains process and user specific information that has been created since the last  boot
    * /srv
        * May be used for data by services like NFS, FTP, and HTTP
    * /sys
        * Used as an interface to different hardware devices that are managed by the linux kernel and associated processes
    * /tmp
        * Contains temp files that may be deleted without any warning during boot
    * /usr
        * contains subdirs with program files, libraries for these programs files, and documentation about them
    * /var
        * Contains files that may change in size dynamically, such as log files, mail boxes, and spool files
* Understanding Mounts 
    * mount
    * df -Th
    * findmnt
* Managing Files 
    * Wildcards 
        * * (astrick) refers to an unlimited number of any characters
            * ls * shows all files in the current dir (except hidden files)
        * ?
            * Used to refer to one specific character that can be any character
            * ls c?t would match cat and cut
        * [auo]
            * refers to one character that may be selected from the range that is specified        between square brackets
            * ls c[auo]t would match cat, cut, and cot
    * Managing and working with dirs 
        * pwd
        * cd 
        * mkdir
        * rmdir (removes if the dir is empy and does not contain any files)
    * Working with absolute and relative pathnames 
