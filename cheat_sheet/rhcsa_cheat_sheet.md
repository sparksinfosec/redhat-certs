# Quick review of important points 

* Pulled together from RHCSA Cert Guide 
* Meant to be a quick and easy reference point compared to more comprehensive notes and labs in prep for the RHCSA 

## Part 1 Performing Basic System Management Tasks

* Installing Red hat enterprise linux 
* Using essential tools 
* Essential file management tools 
* Working with text files 
* Connecting to Red Hat Enterprise Linux 
* User and Group Management 
* Permissions Management 
* Configuring Networking 

### Basic/Essential Tools 

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

### Essential File Management Tools 

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
    * Listing files and dirs 
        * ls -l (long listing)
        * ls -a (shows all including hidden files)
        * ls -lrt
            * -t option shows sorted based on modification date 
            * Most recently modified last because of -r option
        * ls -d (shows the names of dirs)
        * ls -R (recursive)
    * Copying files and dirs 
        * cp /path_to_file /path_to_destination
        * -R option
            * recursively copy an entire subdir
        * -a (copy in archive mode ensure permissions are kept when copied)
        * Copy hidden files 
    * Moving files and dirs 
        * mv 
            * Can rename file as well
        * mkdir
    * Deleting files and dirs 
        * rm 
            * -f (force)
            * -r (recursive)
            * -i (interactive)
* Using links 
    * Symbolic and Hard links 
    * ln (to create links)
        * -s (for symbolic)
    * Safely removing links 
* Working with archives and compressed files 
    * Creating archives with tar 
        * tar -cf archivename.tar /files-you-want-to-archive
        * -v (verbose)
        * You need at least read permissions on the file and execute permissions on teh dir the file resides in 
        * Originally tar did not use dash (-) in front of options
            * still supported 
        * -r (add a file to an existing archive)
        * -u (update an existing archive, write newer versions of files)
    * Monitoring and extracting tar files 
        * -t (see what files are in the archive before extracting)
        * tar -xvf /archivename.tar (extract contents, default current dir)
        * -C (targetdir)
            * tar -xvf archive.tar -C /tmp
        * star utility 
        * tar -xvf /archivename.tar file-you-want-to-extract (extract one file out of a archive)
    * Using Compression
        * gzip or bzip2 
        * Compressing after an archive (home.tar.gzip)
        * xz utility 
        * gunzip and bunzip2
        * Use with tar 
            * -z (gzip)
            * -J (xz)
            * -j (bzip2)
            * Don't need to use option when extracting (tar should recognize)
    * Overview of tar options
        * c (create an archive)
        * v (show verbose output)
        * t (show content of an archive)
        * z (compress/decompress gzip)
        * j (compress/decompress bzip2)
        * J (compress/decompress xz)
        * x (extract an archive)
        * u (updates an archive only newer files will be written to the archive)
        * C (change the output dir of the command)
        * r (appends files to an archive)

### Working with text files 

* Essential tools for managing text content 
    * less (opens the file in a page)
    * cat (dumps the content of the text file to the screen)
    * head (shows the top of the text file)
    * tail (shows the bottom of the text file)
    * cut (used to filter specific columns or characters)
    * sort (sort contents)
    * wc (counts the number of lines, words, and characters in a text file)
* Head and tail 
    * -n (adjust number of lines (default of 10))
    * -f (refreshes the display with new lines are added to the file tail -f /log/file)
* Cut 
    * -d (delimiter)
    * -f (field)
* Sort 
    * -n (numeric order)
    * -r (reverse)
    * sort -k3 -t : /etc/passwd (field 3 separator :)
* wc 
    * Output defaults 
        * number of lines 
        * number of words
        * number of characters
* Regex 
    * ^ (start of line)
    * $ (end of line)
    * Escaping in regex 
    * Wild cards and multipliers 
        * . (wildcard)
        * [ ] (range of specific characters)
        * * (matches zero or more of the previous character)
        * ? (matches zero or one of the previous character)
    * Extended Regular expressions 
        * -E (grep)
        * + (one or more times)
        * ? (zero or one)
    * Most significant regex 
        * ^text (matches lines that start with specific text)
        * text$ (matches lines that end with specific text)
        * . (wildcard anysingle character)
        * [abc] (range match a, b, or c)
        * ? (extended regex match zero or one of the preceding character)
        * + (extended regex match one or more of the preceding character)
        * * (match zero to infinite number of previous character)
        * \{2\} (match extactly two of the previous character)
        * \{1,3\} (match a min of one and a max of three of the previous characters)
        * colou?r (match zero or one of the previous character)
        * (...) (used to group multiple characters so that regex can be applied to the group
* Grep 
    * -i (NOT case sensitive)
    * -v (show lines that do not contain the regex)
    * -r (searches files in the current dir and all subdirs)
    * -e (lines matching more than one regex, used before each regex)
    * -E (Extended regex)
    * -A <number> (show <number> of lines after the matching regex)
    * -B <number> (show <number> of lines before matching regex)
* awk and sed 
    * awk -F : '{ print $4 }' (-F delimiter $4 field)
    * awk -F : '/user/ { print $4 }' /etc/passwd (searches for text user and print 4th field of matching lines)
    * sed -n 5p /etc/passwd (print the 5th line from the password file)
    * sed -i s/old-text/new-text/g ~/file (replace old-text with new-text globally)
        * -i (write results to file default is STDOUT)
    * sed -i -e '2d' ~/file (delete a line based on specific line number)
    * sed -i -e '2d;20,25d' ~/file (delete lines 2 and 20-25 in file)

### Connecting to RHEL 9

* Working on a local console 
    * Console (the env the user is looking at)
    * terminal (env that is opened to the console and provides access to nongraphical shell typically bash)
    * You can have multiple terminals open on a console, you can not have multiple consoles open in one terminal 
* sudo -i (open a root shell ask for users password)
* su - (ask for root's password)
* Exercise 5-1 Working with several terminal windows simultaneously (part 1 line 1477)
* Working with multiple terminals in a nongraphical env 
    * In nongraphical env you only have one terminal interface 
    * Virtual terminal 
    * Terminal windows with key sequences Alt-F1 thru Alt-f6
        * F1 (gives access to GNOME display manager (GDM graphical login))
        * F2 (provides access to the current graphical console)
        * F3 (gives access to the current graphical console)
        * F4-F6 (gives access to nongraphical consoles)
        * Additional TIP: chvt (chvt 4, chvt3, chvt 1)
    * virtual console tty1 
    * /dev/tty1 (corresponding device files, /dev/tty1 - /dev/tty6)
    * graphical env requires Ctrl-Alt-Function
* Understanding pseudo terminal devices 
    * Every terminal in a Linux env has a device file 
    * /dev/tty1 - /dev/tty6
    * Referred to using numbers in the /dev/pts dir 
* Booting, rebooting, and shutting down systems 
    * Important for exam as you need to make sure to reboot and changes are persistent 
    * Experienced admins can often trigger the right parameter to force a process to reread its configs 
    * There are some scenarios that will require a reboot
        * To recover from a serious problem such as server hang or kernel panic 
        * To apply kernal updates (important one)
        * To apply changes to kernel modules that are being used currently and therefore cannot be reloaded easily 
    * When a server is rebooted all processes that are running need to be shutdown properly 
    * memory buffers 
    * systemd
        * First process that is started when the server starts 
        * Also responsible for managing all other processes, directly or indirectly 
        * needs to make sure all processes are stopped properly 
    * Few commands 
        * systemctl reboot (or reboot)
        * systemctl halt (or halt)
        * systemctl poweroff (poweroff)
    * Halt vs poweroff 
        * The difference between these two commands is that poweroff talks to power management on the machine to shut off power on the machine 
        * This often does not happen using halt 
    * NOTE emergency reset option
        * force a reset from a root shell 
        * echo b > /proc/sysrq-trigger
        * resets the machine without saving anything (only use if no other option)
* Using SSH and related utilities 
    * SSH (secure shell)
    * Default port of 22 
    * sshd server process and a ssh client 
    * Not blocked by firewall 
    * ssh -p <portnumber> (specify a port for ssh 
    * ssh clients: putty, mobaxterm, kitty, mremoteng, bitvise, and xshell
    * Password is the default config 
    * ssh will default to the local user also 
    * ssh root@server (specify a specific user)
    * systemctl status sshd (show the sshd process is currently up and running)
    * -v (verbose on ssh)
    * public key fingerprint in ~/.ssh/known_hosts 
    * ssh -Y (graphical)
    * Common SSH options 
        * -v (verbose help troubleshoot)
        * -Y (graphical applications support)
        * -p <PORT> (specify a non default port)
    * /etc/ssh/ssh_config 
        * FowardX11 yes 
        * set default forward graphical applications thru an ssh session
* Securely transferring files between systems 
    * scp (command if you want the files copied)
    * rsync (command to sync files)
    * sftp (FTP command line syntax to transfer files using sshd)
    * Using SCP to securely copy files 
        * similar to the cp command 
        * scp /etc/hosts server2:/tmp (cp /etc/hosts to /tmp dir on server2)
        * scp root@server2:/etc/passwd ~ (connect to server2 as root, copy /etc/passwd to local home dir)
        * -r (recursive copy of an entire subdir structure)
        * scp -r server2:/etc/ /tmp (copy all of /etc/ on server2 to /tmp locally)
        * -P (specify non default port)
* Using SFTP to securely transfer files 
    * scp = cp 
    * sftp = FTP like interface 
    * Requires sshd process on remote server
    * put and get commands 
    * Local dir is important: files will be stored in the current local dir 
    * When uploading will be searched for in the local dir 
* Using rsync to synchronize files 
    * ssh to synchronize files between remote dir and local dir
    * Advantage is taht only differences need to be considered 
    * Delta sync 
    * Common rsync options 
        * -r (sync the entire dir tree)
        * -l (copies symbolic links as symbolic links)
        * -p (preserves permissions)
        * -n (performs only a dry run, does not actually sync anything)
        * -a (archive mode, ensures all subdir tress and all files properties will be syncd)
        * -A (uses archive mode, and in addition syncs ACLs)
        * -X (sync SELinux context as well)
* Config key based auth for ssh 
    * password as usually bad practice 
    * .ssh/authorized_keys 
    * to create a key pair 
        * ssh-keygen
    * copy public key over to target server 
        * ssh-copy-id 
    * Public key goes to remote server 
    * When authenticating using key pairs, the user generates a hash derived from the private key 
    * Exercise 5-5 connecting to a remote server with public/private keys 
        * line 1701 part 1 
* Summary 
    * Learned the difference between consoles, terminals, and shells 
    * Set up terminal sessions locally as well as remotely 
    * SSH to connect to remote server and how to securely copy files between servers 
* Define key terms 
    * console 
    * terminal 
    * subshell
    * reboot
    * systemd 
    * key based login
    * public key 
    * private key 

### User and Group Management 

* Following topics are covered:
    * Understanding different user types 
    * creating and managing user account
    * creating and managing group accounts 
* RHCSA objectives 
    * Create, delete, and modify local user accounts 
    * Change passwords and adjust password aging for local user accounts 
    * Create, delete, and modify local groups and group membership
    * Config superuser access 
* Understanding different user types 
    * Privileged and unprivileged users 
    * root (default privileged user)
    * All other non admin tasks an unpriviledged user should be used 
    * RHEL 9 root user account is often disable (during install this can be enabled)
    * sudo when admin privileges are needed 
    * id (command)
        * Get information about a user account
        * See details about the current user
        * OR can specify the user id user_name
    * Working as root 
        * super user 
        * Some task require root privileges 
        * examples include 
            * installing software 
            * managing users 
            * creating partitions on disk devices 
            * generally speaking all tasks that involve direct access to devices need root permissions 
        * Logging in directly as root is not recommended 
        * Elevating permissions is recommended 
    * Methods to run tasks with elevated permissions 
        * su
            * opens a subshell as a different user, with the advantage that commands are executed as root only in the subshell
        * sudo 
            * allows authorized user to work with admin privileges 
        * PolicyKit 
            * enables you to set up graphical utilities to run with admin privileges 
    * Using su 
        * Requires root password (or password of user you are switching too)
        * su (by itself root is implied)
        * Acquire the credentials of the target user 
        * subshell that is started when using su is an env of the target user account 
            * But env settings for that user account have not been set 
        * If you need complete access to the entire env of the user account (su -)
            * Starts a login shell (all scripts that make up the user env are processed)
        * su - is better than using su 
    * Sudo 
        * Admin can config sudo access to grant specific user admin permissions to perform specific tasks 
        * This approach is considered more secure (admin permissions only while running specific commands)
        * Can set a user as admin during installation
        * Can also add user as a member of the wheel group 
        * Add user to group wheel 
            1. usermod -aG wheel user (Add user to wheel group via usermod)
            1. visudo (make sure the line: %wheel ALL=(ALL) ALL is in the sudoer file)
        * Can also use visudo to edit /etc/sudoers and gives user access to specific commands 
            * linda ALL=/usr/sbin/useradd, /usr/bin/password
            * NOTE this allows linda to change password for all user even root 
            * linda ALL=usr/sbin/useradd, /usr/bin/passwd, ! /usr/bin/passwd root
            * Allows linda to change password for all user except root 
        * Assign sudo privileges to individual users or groups of users, visudo (edit /etc/sudoers file)
        * TIP: When using sudo and entering a password a token is generated 
            * By default token is valid for 5 minutes 
            * using visudo (edit the /etc/sudoers file)
            * Defaults timestamp_timeout=240 (extends the timeout to 240 minutes)
        * Best practice is to use drop in files in the dir /etc/sudoers.d
        * TIP: sudo with pipes 
            * sudo sh -c (can use any command containing a pipe as its arg)
    * PolicyKit
        * GUI 
        * Don't need to know policykit 
        * GOOD TO KNOW pkexec command tho 
        * pkexec (command as an alt to sudo in case you ever completely lose sudo access to a system)
* Creating and managing user accounts 
    * System accounts and normal accounts
        * Typically two types of user accounts 
        * normal user accounts for people who need to work on a serer and who need limited access to the resouces on that server 
            * Typically authed thru a password 
        * System accounts that are used by services the server is offering
        * Both type of accounts share common properties (which are kept in the files /etc/passwd and /etc/shadow)
        * Fields are separated from each other by a colon 
    * Breaking down /etc/passwd fields 
        * Username 
            * Unique name for each user 
            * Important to match a user to pw (passwords stored in /etc/shadow)
            * No spaces in a username 
            * General convention to use lowercase letters 
        * Password 
            * Old days the hash password was stored here 
            * Now stored in /etc/shadow 
        * UID 
            * Each user has a unique ID (UID)
            * Numeric ID 
            * UID really determines what a user can do 
            * When permissions are set for a user, the UID (not the username) is stored in the file metadata
            * UID 0 is reserved for root 
            * Lower UIDs (typically up to 999) are used for system accounts
            * Higher UIDs (from 1000 on by default) are reserved for people who need to connect a dir to the server 
            * Range of UIDs that are used to create regular accounts is set in /etc/login.defs 
        * GID 
            * Each user is a member of at least one group 
            * This group is the primary group 
            * This group plays a central role in permission management 
            * Users can be members of additional groups which are admin'd in the file /etc/group
        * Comment Field 
            * IS OPTIONAL 
            * Used to add comments for user accounts 
            * GECOS field (General Electric Comprehensive Operating System)
        * Directory 
            * Initial dir that user is placed in after logging in
            * Also referred to as the home dir 
            * Used to store personal files and programs (if used by a person/normal user)
            * For a system user account, this is the env where the service can store files it needs while operating 
        * Shell 
            * Program that is started after the user successfully connects to a server 
            * /bin/bash (default linux shell)
            * For system user accounts, it will typically be a shell like /sbin/nologin
            * /sbin/nologin denies access to the user (silently)
            * Ensures that if an intruder logs into the server they cannot get any shell access
            * Optionally, can create an /etc/nologin.txt file 
            * In which case only root will be able to log in but other users will see the contents of this file when their logins are denied)
    * A part of the user properties are stored in /etc/passwd
    * Another part of the config is stored in /etc/shadow 
        * Set properties of the password
        * Only root and processes running as root have access to /etc/shadow
    * Fields from the /etc/shadow file 
        * Login name 
            * /etc/shadow does not contain any UIDs (username only)
            * Opens up the possibility for multiple users using the same UID but different password (not recommended)
        * Encrypted password 
            * Contains all that is needed to store the password in a secure way 
            * If empty no password is set (user cannot login)
            * If the field starts with an ! login is current disabled
        * Days Since Jan 1, 1970 that the password was lasted changed (epoch)
        * Days before password maybe changed 
            * Allows system admins to use stricter password policy 
            * Typically this field is set to the value 0
        * Days after which password must be changed 
            * Max validity period of password 
            * 99,999 (274 years) is the default 
        * Days before password is to expire that user is warned 
            * Warn a user a forced password change is upcoming 
            * 7 days (default)
        * Days after password expires that account is disabled 
            * Enforce a password change 
            * After expiration of the pw, user can no longer log in
            * After account reaches max validity period, acocunt is locked 
            * Allows for a grace period in which the user can change their passwrod but only during login process 
            * Set in days, unset by default 
        * Days since Jan. 1 1970 that account is disabled 
            * Admin can disable an account on a specific date 
            * No default value 
        * A reserved field, which was once added "for future use"
        * Most of the password properties can be managed with the passwd or chage command 
    * Creating Users 
        * You can edit the contents of /etc/passwd and /etc/shadow
        * vipw (risk making an error that makes logging in impossible to anyone)
        * useradd (utility that you should use for creating users)
        * userdel (to remove users)
        * userdel -r (remove a user and the complete user env)
    * Modifying the config files 
        * Not recommended 
        * Errors can mess up login and locking problems if multiple admins are trying to modify at the same time 
        * vipw (open an editor interface on your config file)
        * Does not check syntax 
        * vipw -s (for /etc/shadow file)
        * vigr (edit contents of /etc/group)
        * Good to know, but useradd and groupmod are better options 
    * Using useradd
        * useradd (probably most common tool for adding users)
        * Ability to add a user account from the cmd by using many of its parameters
        * useradd -m -u 1201 -G sales,ops linda (create a user named linda)
            * Who is a member of the secondary group sales and ops 
            * UID of 1201
            * add a home dir to the user as well 
    * Home directory 
        * All normal users will have a home dir (store personal files)
        * System accounts the home dir often contains the working env for the service account 
        * Likely not required to change home dir settings related to system accounts
        * Created automatically from RPM post installation scripts when installing software packages
        * /etc/skel (skeleton dir files are copied to user home dir when created)
        * Determine how the env is set up (also config files)
    * Default Shell 
        * Program that is started after successful login/auth (most regular users noramally have a default shell)
        * /bin/bash (normally)
        * System users should not have an interactive shell as the default shell
        * /sbin/nologin (for most system users)
        * useradd or usermod (-s option to set or change default shell)
        * usermod -s 
        * useradd -s 
        * useradd caroline -s /sbin/nologin (user caroline will not be able to log in)
    * Managing User Properties 
        * cmd tool or work directly in the config file using vipw
        * usermod (command for modifying user properties)
        * Can be used to set all properties of users as stored in /etc/passwd and /etc/shadow
        * One task it does not do well: SETTING PASSWORDS (usermod has an -p option)
        * Just use passwd 
    * Config files for user management defaults 
        * useradd (some default values are assumed)
        * These default values are set in two config files: /etc/login.defs and /etc/default/useradd 
    * Some significant properties that can be set from /etc/login.defs
        * MOTD_FILE:
            * Defines the file that is used as the message of the day file 
        * ENV_PATH:
            * Defines the $PATH variable (list of dirs that should be searched for exe files after logging in
        * PASS_MAX_DAYS, PASS_MIN_DAYS, and PASS_WARN_AGE:
            * Defines the default password expiration properties when creating new users 
        * UID_MIN:
            * Indicates the first UID to use when creating new users 
        * CREATE_HOME:
            * Indicates whether or not to create a home dir for new users 
    * Managing password properties 
        * Two commands to change password properties for users (/etc/shadow): chage and passwd 
        * passwd -n 30 -w 3 -x 90 linda (set the pw for linda to a minimal usage period of 30 days)
            * an expiry after 90 days 
            * Warning generated 3 days before expiry 
        * Many tasks using passwd can be done with chage also 
        * chage -E 2025-12-31 bob (have account for user bob expire Dec 31 2025)
        * chage -l (see current password management settings)
        * chage has a interactive mode 
        * chage anna (prompt for all the password properties you can set interactively)
    * Creating a user ENV 
        * When a user logs in, an env is created 
        * ENV consists of variables that determine how the user is working (such as $PATH)
        * To construct the user env a few files play a role 
            * /etc/profile (Used for default settings for all users when starting a login shell)
            * /etc/bashrc (Used to define default settings for all users when starting a login shell)
            * ~/.profile (Specific settings for one user applied when starting a login shell)
            * ~/.bashrc (Specific settings for one user applied when starting a subshell)
        * When user log in files are read in this order
        * Variables and other settings that are defined iin these files are applied 
        * If variables are set in more than one file, last one wins 
* Creating and Managing group accounts 
    * Every user has to be a member of at least one group 
    * Understanding Linux Groups 
        * Two different kind of groups 
        * Primary Group 
            * Every user must be a member of a primary group, and a user has only one primary group 
        * User creates a file, the user's primary group becomes the group owner of the file 
        * User can also access all files their primary group has access to 
        * Primary group membership defined in /etc/passwd 
        * Group itself is stored in /etc/group 
        * Users can be a member of one or more SECONDARY GROUPS as well 
        * Secondary groups are important to get access to files 
        * Secondary groups are important (for file access)
        * Especially in regards to File servers (allow people working for different departments to share files with one another)
        * Secondary group membership can be used to enable user admin privileges thru sudo also (making user a member of group wheel)
    * Creating Groups 
        * vigr (modify group config file directly)
        * groupadd (command line utility)
    * Creating groups with vigr
        * vigr (open an editor interface directly on the /etc/group config file)
        * /etc/groups (there is also /etc/gshadow file)
        * Hardly used any more but store group passwords
        * Some cool features 
        * In the third field of this file you can list admins
        * Comma separated list of users who can change passwd for group members
        * NOTE that specifying group members here is optional 
            * But if it is done, group member names must be the same as the group members in /etc/group
    * Fields used in /etc/group 
        * Group Name (Contains the name of the group)
        * Group Password (Hardly used anymore field contain a group password)
            * Group password can be used by users who want to join the group on a tmp basis
            * Access to files the group has access is allowed (with password/if group password is used)
            * Stored in /etc/gshadow file (only accessible by root)
        * Group ID (field contains a uniq numeric group ID number)
        * Members (Find the names of users who are a member of the group as a SECONDARY GROUP)
            * DOES NOT show users who are a member of this group as their primary group 
    * Using groupadd to create groups 
        * groupadd (followed by name of the group you want to add)
        * -g (allows you to specify a group ID when creating the group)
    * Managing group properties 
        * groupmod (manage group properties)
        * Change the name or group ID of a group (can not add group members)
        * NOTE: may be a bad idea to change these properties (can impact group owned files that already exist)
        * usermod (usermod -aG (add users to new SECONDARY group))
        * Common that group properties are managed directly in /etc/group (vigr command)
        * lid (to see which users are a member of a group 
        * lid -g sales (check which users are a member of the sales group)
    * NOTE group membership are defined in two different locations so can be difficult to file which members belong to which groups 
        * groupmems (a way to check this)
        * groupmems -g sales -l (see which users are a member of sales group)
        * Secondary group and primary group assignments

### Permission Management 

* Following topics are covered in this chapter 
    * Managing file ownership 
    * Managing basic permissions
    * Managing advanced permissions 
    * Setting default permissions with umask 
    * Working with user extended attributes 
* Following RHCSA exam objectives are covered in this chapter 
    * Manage default permissions 
    * List, set, and change standard ugo/rwx permissions 
    * Create and config set-GID dirs for collaboration
    * Diagnose and correct file permission problems 
* Permission management 
    * Permissions are assigned to three entities (permissions are used to get access to files)
        * File owner
        * Group owner
        * Other entity 
* Managing file ownership
    * File and dir ownership are vital for working with permissions
    * Displaying ownership
        * Two owners for every file and dir (user owner and group owner)
        * ls -l (shows the user, group, and other listing (ugo))
        * Owners are set when a file or dir is created 
        * On creation the user who created the file becomes the user owner
        * Primary group of that user becomes the group owner
        * Shell checks ownership (to determine whether you as a user have permission to a file or dir)
        * Checks ownership in following order 
            1. Shell checks whether you are the user owner of the file you want to access (user of the file)
            * If you are the user you get permission (based on user permission set) and the shell looks no further
            1. If you are not the owner, shell checks if you are a member of the group owner 
            * Group of the file 
            * If you are a member you get access to the file based on group permission set (shell looks no further
            1. If you are neither the user owner nor the group owner 
            * And have not obtained permissions thru ACLs 
            * You get the permissions of the other entity
        * find -user (can get a list of all files on the system that have a given user or group as the owner)
        * find / -user linda 
        * find / -group users 
    * Change user ownership 
        * chown (command too apply apropriate permissions, 1st thing to consider is ownership)
        * chown who what
        * chown linda files (changes the ownership of the file files to user linda)
        * chown -R (set ownership recursively)
        * -R (set ownership of the current dir and everything below it)
        * chown -R linda /files (change ownership of the dir /files and everything beneath it to user linda)
    * Changing group ownership 
        * chown and chgrp
        * chown uses a . or : in front of the group name 
        * chown .account /home/account (change the group owner of the dir /home/account to the account group)
        * chown can be used to change user and/or group ownership in a number of ways 
            * chown lisa myfile (set user lisa as the owner of myfile)
            * chown lisa.sales myfile (set user lisa as user owner and group sales as group owner of myfile)
            * chown lisa:sales myfile (set user lisa as user owner and group sales as group owner of myfile)
            * chown .sales myfile (set group sales as group owner of myfile without changing the user owner)
            * chown :sales myfile (set group sales as group owner of myfile without changing the user owner)
        * chgrp account /home/account (set group ownership of the dir /home account to the group account)
    * Understanding default ownership 
        * When a user creates a file, default ownership is applied 
        * User who creates the file automatically becomes user owner 
        * Primary group of that user automatically becomes group owner 
        * user can use newgrp command to change the effective primary groups so that new files will get the new primary group as group owner
        * group (command to show the current primary group)
            * primary group is the first name listed after the : character
        * groups lisa
        * newgrp will open a new shell in which the new temporary primary group is set 
        * Will continue to be used as the effective primary group until the exit command is used 
        * To be able to use the newgrp command a user has to be a member of that group 
        * gpasswd can be used for a group password (but this is uncommon)
        If a user uses newgrp but is not a member of the group prompted for group passwd 
* Managing Basic Permissions 
    * Understanding read, write, and execute permissions 
        * Three basic permissions allow users read, write, and execute 
        * Effects differ when applied to files or dirs 
        * lines 2338-2362 part 1 goes over some indepth read write and execute info
        * Read
            * applied to files (view file contents)
            * applied to dirs (list content of dir)
        * Write 
            * applied to files (change content of file)
            * applied to dir (create and delete files and subdirs)
        * Execute 
            * applied to files (run a program)
            * applied to dirs (change to the dir)
            * Important for dirs (normally default to dirs)
            * execute never set automatically to files (user owner and root need to apply)
    * Applying read, write, and execute permissions 
        * chmod (command to apply permissions)
        * Chmod can set permissions for user, group, or other
        * Relative and absolute mode
        * Absolute mode three digits are used to set permissions (Read (4), Write (2), and Execute (1))
        * chmod 755 /somefile (rwx for user, rx for group, rx for other)
        * Absolute mode will replace current permissions
        * Relative mode works with three indicators to specify what you want to do
            * First specify for whom you want to change permissions
            * u (user), g (group), o (other), a (all)
            * Then you can add or remove permission from the current mode
            * Or set them in a absolute way 
            * Using r, w, and x to specify what permissions you want to set 
            * Omit the to whom part to add or remove a permission for all entities
        * chmod +x somefile (execute permission for all entities)
        * chmod g+w,o+r somefile (add write permissions to group and remove read from others)
        * Recursive mode needs special attention
        * If you want to apply execute permission in a recursive way you should apply it as X, not x 
        * chmod -R a+x files (instead use chmod -R a+X files)
* Managing Advanced Permissions 
    * Three advanced permissions
    * Set User ID (SUID)
        * ls -l (see SUID permission as an s at the execute (x) for user permissions)
    * Set Group ID (SGID)
        * shows as an s at the position where you normally find the group execute permission
        * Lowercase s indicates both SGID and execute are set 
        * Uppercase S means only SGID is set 
    * Sticky Bit
        * Shows as T at the position where you normally see execute permission for others 
        * Lowercase t indicates that sticky bit + execute permissions for the other entity are set 
        * Uppercase T indicates that only sticky bit is set 
    * RHCSA objectives specifically mentions being able to use SGID to create a shared group dir 
* Applying Advanced Permissions 
    * chmod (to apply SUID, SGID, and sticky bit)
    * SUID has a numeric value of 4
    * SGID has a numeric value of 2 
    * Sticky bit has a numeric value of 1 
    * Need to add a four digit arg to chmod 
    * First digit refers to the special permissions 
    * chmod 2755 /somedir (add SGID permission to a dir and set rwx for user, rx for group and other)
        * Impractical as you have to look up current permission (risk overwriting permissions)
    * Recommend working in relative mode if you need to apply any of the special permissions 
        * chmod u+s (for SUID)
        * chmod g+s (for SGID)
        * chmod +t (for sticky bit)
* Working with SUID, SGID, and Sticky Bit 
    * SUID 
        * 4 (numeric value) 
        * u+s (relative value)
        * User executes file with permissions of file owner
        * No means for dirs 
    * SGID 
        * 2 (numeric value)
        * g+s (relative value)
        * User executes file with permissions of group owner (on files)
        * Files created in dir get the same group owner (on dirs)
    * Sticky Bit
        * 1 (numeric value)
        * +t (reltaive value)
        * No meaning on files
        * Prevents users from deleting files from other users (on dirs)
* Setting default permissions with umask 
    * To set default permissions you use either file ACLs or umask 
    * Umask settings determine default permissions for new files 
    * This shell setting is applied to all users when logging in to the system 
    * Numeric value used to subtract from the max permissions that can be set automatically to a file 
    * Max setting for files is 666
    * Max setting for dirs is 777
    * First digit is user, second is group, third is other
    * Default umask setting of 022 gives 644 to all new files, and 755 to all new dirs 
    * Umask values and their results 
        * 0 
            * Applies rw to files 
            * Everythin to dirs
        * 1 
            * rw to files 
            * rw to dirs 
        * 2
            * r to files 
            * rw to dirs 
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
            * Nothing to files 
            * x to dirs 
        * 7 
            * Nothing to files 
            * Nothing to dirs 
    * Two ways to change umask settings
        * For all users 
        * For individual users 
    * /etc/profile 
    * Create a script in /etc/profile.d dir and specify the umask you want to use in that shell script
        * If the umask is changed in this file it applies to all users after logging in to your server 
    * Change umask settings in a file with the name .profile 
        * Home dir of an individual user
        * Applied to individual user only 
* Working with user extended attributes 
    * An alt method of securing files on a linux server is by working with attributes 
    * Most useful attributes that you can apply 
        * A 
            * Ensures that the file access time of the file is not modified
            * Normally every time a file is opened the file access time must be written to the files metadata
            * Can impact performance in a negative way 
            * Can be disabled for files that are accessed on a regular basis
        * a 
            * Allows a file to be added to but not to be removed 
        * c 
            * If a file system where volume level compression is supported 
            * Will make sure the file is compressed the first time compression engine becomes active 
        * D 
            * Changes to files are written to disk immediately and not to cache first 
            * Useful attribute on important database files to make sure that they do not get lost between file cache and hard disk 
        * d 
            * Makes sure the file is not backed up where the legacy dump utility is used 
        * I 
            * Enables indexing for the dir where it is enabled 
        * i
            * Makes file immutable (therefore no changes can be made to the file at all)
        * s 
            * Overwrites the blocks where the file was stored with 0s after the file has been deleted
        * u 
            * Saves undeleted information
            * Allows a utility to be developed that works with that information to salvage deleted files 
    * Most attributes are rather experimental 
    * Only of any use if an application is used that can work with the given attribute 
    * chattr (command to apply attributes)
    * chattr +s somefile (to apply the attributes to somefile)
    * chattr -s somefile (remove the attribute)
    * Test out to find how attributes are one of the rare cases where you can block access to the root user
    * lsattr (overview of all attributes that are currently applied)
* Summary 
    * Work with permissions 
    * Basic permissions as well as advanced permissions
    * umask 
    * User extended attributes (to apply an additional level of file system security)
* Define Key Terms 
    * Ownership 
    * Permissions
    * Inheritance 
    * Attribute 

### Configuring Networking 

* The Following Topics are covered in this Chapter 
    * Networking fundamentals 
    * Managing network address and ints 
    * Validating network configs 
    * Managing network config with nmtui and nmcli
    * Setting up hostname and name resolution
* The following RHCSA exam objectives are covered in this chapter
    * Config IPv4 and IPv6 Addresses
    * Config hostname resolution
* Networking Fundamentals 
    * To set up networking on a server, your server needs a unique address on the network 
    * IP (internet protocol) address are used 
    * IPv4 (32 bit addresses 4 octets separated by dots)
    * IPv6 (128 bit addresses and are written in 8 groups of hexadecimal 16 bits each separated by colons)
    * IP addresses 
        * Node (also might encounter the word host)
        * A host is typically a server providing services on the network 
        * For ease of communication every IP address belongs to a specific network 
        * Routers are used to communicate with computers across networks 
        * Router connects networks to one another 
        * Private network addresses (addresses that are for use in internel networks only)
        * Some IP network addresses have been reserved for this purpose 
            * 10.0.0.0/8 (Single class A network)
            * 172.16.0.0/12 (16 Class B networks)
            * 192.168.0.0/16 (256 Class C Networks)
        * Private address nodes cannot access the internet directly 
        * NAT (Network address translation)
            * NAT router in and out not interacting with individual hosts 
            * NAT router tracks tables of all connections that currently exist for host on the network 
            * NAT router helps make it possible for comps with a private IP address to connect to the internet
    * IPv6 Addresses
        * Can replace one range of zeros with ::
        * Leading zeros can be omitted
        * 02fb:0000:0000:0000:90ff:fe23:8998:1234
        * 2fb::90ff:fe23:8998:1234
    * IPv4 network masks 
        * Subnet mask defines which part of the network address indicates the network and what part indicates the node
        * Classless Inter-Domain Routing (CIDR) notion
        * Classical notation
        * They always need to be specified with the network address 
        * 192.168.10.100/24 (CIDR Notation - 24 bit network address is used)
        * 192.168.10.100/255.255.255.0 (Classical notation - same as above)
        * Often network masks use multiple bytes 
        * 192.168.10.100/24
            * First 3 bytes (192.168.10) are the network part
            * Last byte (.100) is the host part of that network 
        * 192.168.10.100/24 (Network address is 192.168.10.0)
        * Broadcast address (address that can be used to address all nodes in the network)
            * All node bits are set to 1 
            * 192.168.10.100/24 (Broadcast address is 192.168.10.255)
    * Binary Notation
        * IPv4 address space is limited 
        * As a result modern IPv4 networks use variable length network masks
        * 219.209.113.33/27
        * Only a part of the byte is used for addressing nodes 
        * Another part is used for addressing the network
        * /27 (last 3 bits of the last byte are used to address the network)
            * Last 5 bits are used for addressing node (hosts)
        * 212.209.113.33 = 11010100.11010001.00001010.00100001
        * Subnet mask /27 = 11111111.11111111.11111111.11100000
        * with a /27 30 nodes can be addressed per network 
        * 32 IPs, 2 of them network address and broadcast address (30 useable hosts)
    * MAC addresses 
        * IP addresses allow nodes to communicate to other nodes on the internet
        * Each network card also has a 12 byte MAC address 
        * MAC addresses are for use on the local network 
        * Not used for communication between nodes that are on different networks 
        * Help map IP to physical network card
        * 00:0c:29:7d:9b:17 (example mac address 
        * First 6 bytes are the vendor ID/Second 6 bytes are the unique node ID 
    * Protocol and ports 
        * IP addresses to ID individual nodes (On these nodes you will typically be running services)
        * Like web server or FTP server 
        * Every service has a specific port address (To ID these services)
        * port 80 for http, port 22 for ssh 
        * In network communication the sender and reciever are using port addresses 
        * Destination and source port address 
        * Specific protocol is used between IP address and the port address
        * TCP/UDP (or ICMP)
* Managing network addresses and interfaces 
    * Linux server admin need to manage network addresses and network interfaces 
    * Network addresses can be assigned in two ways 
        * Fixed and Dynamically assigned IP addresses
    * For a long time network cards in linux have had default names such as eth0, eth1, and eth2 
        * Naming assigned based on the order of detection of the network card 
        * RHEL 9 default names for network cards are based on firmware, device topology, and device type
    * Network card names always consist of the following parts
        * Ethernet interfaces begin with an en 
            * WLAN interfaces begin with wl 
            * WWAN interfaces begin with ww
        * The next part of the name represents the type of adapter 
            * an o for onboard 
            * s is for hotplug slot 
            * p is for a PCI location
            * Admins can also use x to create a device name that is based on the MAC address of the network card 
        * Followed by a number, which is used to represent an index of, ID, or port 
        * If the fixed name cannot be determined, traditional names such as eth0 are used 
        * Based on this information device names such as eno16777734 can be used
        * em1 (embedded network card 1)
        * OR p4p1 (which is PCI slot 4, port 1)
* Validating network config 
    * Check the following network items 
        * IP address and subnet mask 
        * routing
        * Availability of ports and services 
    * Validating network address config 
        * ip 
        * ip addr (to config and monitor network addresses)
        * ip route (to config and monitor routing information)
        * ip link (to config and monitor network link state)
        * ifconfig used in earlier linux versions
        * ip addr show (show current network settings)
        * 127.0.0.1 (loopback int used for communication between process/internal communication)
        * ip link show (if you are just interested in the link state of the network interfaces)
        * ip link show (repeats the link state info of the ip addr show command)
        * -s (option that will show current link statitics)
    * Validating routing 
        * Default gateway (every networks got one)
        * ip route show (show which router is used as the default router)
        * Default router at all times must be on the same network as the local IP address that your network card is using 
    * Validating the availability of ports and services 
        * netstat or newer ss command (verify availability of ports on your server)
        * ss -lt (see all listening TCP ports on the local system)
        * 127.0.0.1 or ::1 (loopback address for IPv4 and IPv6 means only listening locally)
        * Other ports are listening on all (*) or :::* 
* Managing network config with nmtui and nmcli 
    * RHEL 9 is managed by the network manager service 
    * systemctl status NetworkManager (to verify its current state)
    * When network manager comes up it reads the network card config script 
        * /etc/NetworkManager/systemconnections
        * Has a name that starts with the name of the network interface the config applies to 
        * Like ens160.nmconnection
    * Should know the difference between a device and a connection
        * A device is a network interface card
        * A connection is the config that is used on a device 
        * In RHEL 9 you can create multiple connections for a device 
    * Switching between connections on devices is common on end user systems but not so common on servers 
    * To manage network connections that you want to assign to devices, you use nmtui or the nmcli command 
    * nmcli tool is cool and very powerful but is not the easiest tool available 
        * To change network configs fast and efficiently you should use the menu drive nmtui utility??
    * Required permissions to change network config 
        * Root user can make modifications to current networking 
        * Ordinary user logged into local console is able to make changes as well 
        * As long as the user is using system keyboard to enter either a graphical console or a text based console these permissions are granted 
        * Users are suppose to be able to connect their local system to a network 
        * Regular users who use ssh to connect are not allowed to change the network config 
        * nmcli general permissions (to check your current permissions)
    * Configuring the network with nmcli 
        * ip addr add (to temp set an IP address on a network interface)
        * Everything you do with the ip command is nonpersistent
        * nmtui and nmcli (if you want to make persistent changes to the config)
        * nmcli (show all connections/shows inactive and active connections)
        * nmcli con show 
        * After finding the name of the connection you can use nmcli con show (followed by the name of the connection) to see all properties of the connection
        * man 5 nm-settings (to find out additional information/exactly settings are doing)
        * nmcli (show an overview of currently configd devices and the status of these devices)
        * nmcli dev status (show a list of devices)
        * nmcli dev show <devicename> (show settings for a specific device)
        * TIP nmcli might seem difficult (make sure that bash-completion package is installed)
            * nmcli (TAB x2 should see all available options that nmcli expects at this moment)
        * nmcli con add 
        * nmcli con mod (change current connection properties)
        * Execellent man page (man nmcli-examples)
            * If you can find this man page you can do almost anything with nmcli
    * Configuring the network with nmtui 
        * Text user interface that allows teh creation of network connections easily 
        * nmtui interface consists of three menu options
            * Edit a connection: create new or edit existing connection
            * Activate a connection: (re)activate a connection
            * Set system hostname: set the hostname of your computer 
        * Edit a connection offers almost all features that you might need while working with n/w connections
        * After editing the connection you need to deactivate it and activate it again
    * Working with network config files 
        * /etc/NetworkManager/system-connections
            * Every connection that you create is stored as a config file in this dir 
        * Name of the config files start with the name of the connection followed by .nmconnection
        * Previous versions of RHEL network connection were stored in the /etc/sysconfig/network-scripts dir
            * If NetworkManager finds legacy connection scripts in this dir, they will still be used
            * But NetworkManager connection scripts are no longer stored by default at this location
* Setting up hostname and name resolution
    * To communicate with other host, hostnames are used (important to know as an admin)
    * Important to make sure hosts can contact one another based on hostname (setting up hostname resolution)
    * Hostnames 
        * Important to know how to set up hostname (used to access servers and the services they offer)
        * Two parts that make up a fully qualified domain name (FQDN)
        * server1.example.com (for example good practice to specify the FQDN not just the hostname)
        * FQDN provides a unique identity on the internet 
        * There are different ways to change the hostname 
            * Use nmtui and select the option to change hostname 
            * hostnamectl set-hostname
            * edit the content of the config file /etc/hostname 
        * Config hostname with hostnamectl 
            * hostnamectl set-hostname myhost.example.com 
            * hostnamectl status (show the current hostname)
            * hostnamectl status (not only information about the hostname, linux kernel, virt type and more)
        * To set hostname resolution typically use DNS (config a DNS server is not a RHCSA objective)
        * But need to know how to config your server to use an existing DNS server for hostname resolution
        * Apart from DNS, you can config hostname resolution in /etc/hosts file 
        * cat /etc/hosts
        * All hostname IP address definitions as set in /etc/hosts will be applied b4 the hostname in DNS is used 
        * This is configed as default in the hosts line in /etc/nsswitch.conf 
            * Which by default looks like: hosts: files dns myhostname 
        * Setting up a etc/hosts file is easy 
            * Just make sure it contains at least two columns 
            * First column has the IP address ofthe specific host
            * Second column specifies the hostname 
            * Hostname can be provided as a short name (like server1) or a FQDN 
            * Can also specify both in /etc/hosts
            * In this case the second column must contain the FQDN and 3rd column can contain the alias 
    * DNS name resolution 
        * Just using a /etc/hosts is not enought for name resolution (if you want to communicate with other hosts on the internet 
        * Should use DNS too
        * Specify which DNS server should be used (set the DNS server using nmcli or nmtui)
        * NetworkManager config stores the DNS information in the config file for the network connection
            * /etc/sysconfig/network-scripts 
            * From there pushes the config to /etc/resolv.conf file 
            * Which is used for DNS name server resolving 
            * Do not edit /etc/resolv.conf directly (will be overwritten next time you restart NetworkManager)
            * Recommended to always set up at least two DNS name servers (first does not answer, second is contacted)
        * Few different options to specify which DNS server you want to use
            * nmtui to set DNS name server
            * Use a DHCP server that is configd to hand out address of the DNS name server 
            * nmcli con mod <connection-id> [+]ipv4.dns <ip-of-dns>
        * Notice that if your comp is configed to get the network config from a DHCP server, the DNS server is also set via DHCP server 
            * nmcli con mod <con-name> ipv4.ignore-auto-dns yes (if you do not want this to happen)
            * getent hosts <servername> (to verify hostname resolution)
            * This command searches in both /etc/hosts and DNS to resolve the hostname that has been specified
* Define key terms 
    * IP (internet protocol)
    * IPv4
    * IPv6
    * Subnet mask
    * port
    * protocol
    * interface
    * Dynamic Host configuration protocol (DHCP)
    * Connection
    * Domain Name System (DNS)
    * Fully qualified domain name (FQDN)

## Part 2 Operating Running Systems 

### Managing Software 

* The following topics are covered in this chapter
    * Managing software packages with dnf
    * Using dnf
    * Managing package modules
    * Managing software packages with rpm
* The Following RHCSA exam objectives are covered in this chapter
    * Install and update software packages from red hat network 
    * Remote repo 
    * Or local file system 
* Managing Software 
* Managing software packages with dnf 
    * dnf (the default utility used to manage software packages on RHEL)
    * dnf is designed to work with repos (repos are online depots of available software packages)
    * Learn how to create and manage repos (How to manage software packages based on the content of the repos)
    * Understanding the role of repositories 
        * S/W on RHEL is provided in the Red Hat Package Manager (RPM) format
        * Repos play a key role in working with software (working with repos make it easy to keep your server current)
        * Whenever you use the dnf command to install software (the most recent version is automatically used)
        * Also another major benefit is package dependencies with dnf
        * Without repos packages would have to be installed manually (repo resolves dependencies automatically)
        * If you are using RHEL with the repos provided for registered installations
            * There is no reason why procedure should not work 
            * The attempts to install software will usually succeed
        * While installing RHEL 9, you are asked to register with RH customer portal
            * Provides different repos (after registering, installed s/w packages verified by RH automatically)
            * Choose to not register (cannot get in touch with RH repos)
            * Need to be able to config repo client to specify yourself which repo you want to use
        * Repos are specific to OSs
        * EPEL (Extra package for enterprise linux) repo 
            * Not recommended
            * Provide additional software from Fedora project to RHEL server (for example)
    * Registering Red Hat Enterprise Linux for support 
        * RH support > Register > Entitlement 
        * Entitlement is assocaited to your account on RH customer portal (obtained thru purchase of a sub from RH)
        * Or by joing RH developer program (16 max install of RHEL systems)
        * No support, but updates and access to RH repos (developers.redhat.com)
        * RHSM (RH subscription management) tool to manage your entitlement
        * Managing an entitlement involves 4 basic tasks
            * Register, Subscribe, Enable, Review and Track (lines 76 - 84 part 2 cert guide)
    * Managing Subscriptions 
        * Manage subs either from GNOME GUI or command line 
        * subscription-manager (tool used for managing from the CLI)
        * subscription-manager register (to register, will prompt for name of your RH user account + passwd)
        * subscription-manager list --available (list available subscriptions, see what your account is entitled to)
        * subscription-manager attach --auto (automatically attach a subscription)
        * subscription-manager list --consumed (get an overview to see which subs are being used)
        * subscription-manager unregister (unregister, deprovision a system)
        * After you register and attach a subscription, entitlement certs are written to /etc/pki dir
        * /etc/pki/product (stored certs for which RH products are installated on this system)
        * /etc/pki/consumer (stored cert ID the RH account to which the system is registered)
        * /etc/pki/entitlement (contains information about the sub that are attach to this system)
    * Specifying which repo to use
        * After install it is configd with a list of repos that should be used 
        * Sometimes have to tell your server which repo should be used for example:
            * You want to distribute nondefault software packages through repos
            * You are installing RHEL without registering it 
        * Telling your server which repo to use is no difficult but is important to know 
        * Tell your server which repo to use (create a file with a name that ends in .repo in the dir /etc/ump.repo.d)
        * Following paraemters are commonly used 
            * [label] (the .repo file can contain different repos, each section starting with a label that IDs the specific repo)
            * name= (Use this to specify the repo you want to use)
            * baseurl= (this option contains the URL that points to the specific repo location)
            * gpgcheck= (This option specifies if a GNU privacy guard (GPG) key validity check should be used to verify that packages have not been tampered with)
        * RHEL 9 dnf config-manager tool (Older versions required memorization to create repo client files)
        * dnf config-manager --add-repo=http://reposerver.example.com/BaseOS (easily generate repo client file)
        * dnf config-manager --add-repo=file:///repo/BaseOS 
        * Need to edit the repo file in /etc/yump.conf.d after adding it (including gpgcheck=0)
            * Without this option the dnf tool wants to do GPG checks on incoming packages, which requires additional complex config that is not needed for the exam)
    * Key options in .repo files 
        * [label]
            * Contains the label used as an identifier in the repo file
        * name= 
            * mandatory option that specifies the name of the repo 
        * mirrorlist= (Typically used for bit online repo only)
            * Optional parameter that refers to a URL where information about mirror servers for this server can be obtained
        * baseurl= 
            * Mandatory option that refers to the base URL where RPM packages are found 
        * gpgcheck= 
            * set to 1 if a GNU privacy guard (GPG) integrity check needs to be performed on the packages
            * If set to 1 a GPG key is required 
        * gpgkey= 
            * Specifies the location of the GPG key that is used to check package integrity
    * Specifying which repo to use cont
        * When creating a repo file 
            * The baseurl parameter is the most important
            * Because it tells your server where to find the files that are to be installed 
        * Baseurl takes as its arg the URL where files need to be installed from 
        * When using a url two components are includes 
            * first the URL identifies the protocol to be used and is in teh format protcol://
            * Such as http://, ftp://, or file://
            * Following the URL is the exact location on that URL 
            * Can be the name of a web server or FTP server
            * Including subdirs where files are found 
            * If the URL is file based, the location on the file system starts with a / as well 
        * Therefore, for a file system based URL 
            * There will be three slashes in the baseurl 
            * Such as baseurl:///repo (which refers to the dir /repo on the local file system)
    * Understanding repository security 
        * Repos allow you to transparently install s/w from the internet (convenient but also security risk)
        * Installing RPM packages are done with root permissions (so RPM package scripts execute as root also)
        * Trust with the software package you are installing from
        * This is why repos in general use key for package signing (RHEL good idea to use trusted repos only)
        * Signed with a GPG key (Check whether packages have changed since the owner originally provided them)
        * GPG key used to sign the s/w packages is typically made available thru the repo as well 
        * Users of the repo can download the key and store it locally 
        * So that the package signature check can be performed automatically each time a package is downloaded from the repo 
        * If repo security is compromised and an intruder manages to hack the repo server, putting fake packages on it 
            * The GPG key signature will not match 
            * The dnf command will complain while installing new packages 
        * GPG keys are highly recommended when using internet repos (internal repos risk is not as high)
        * If you are using a repo where GPG package signing has been used 
            * First contact with the repo the dnf command proposes to download the key that was used for package signing 
            * This is a transparent procedure that requires no further action
        * GPG keys that were used for package signing are installed to /etc/pki/rpm-gpg by default 
    * Creating your own repos 
        * Not a requirement for RHCSA 
        * line 191 part 2 



 
            
            

     
           


