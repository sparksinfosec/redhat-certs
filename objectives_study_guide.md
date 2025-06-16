# Objectives Study Guide Final 

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


## Understanding and use essential tools 

* Access a shell prompt and issue commands with correct syntax 
    * Using virtual terminal 
        * Ctrl-ALT-Fn
        * chvt number
    * Using command line 
        * command --help 
    * find command 
        * find / -name "hosts"
        * find / -type f -size +100M
            * fine / -type f -size +1M -size -100M (bigger than 1M and smaller than 100M)
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
        * grep -i (case insensitive)
        * grep -A5 -B5 (after and before lines)
        * grep -R (recursively search dirs difference between -r)
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
    * /etc/hosts
        * IP_address hostname
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
    * ls -il (inode number might need ls -ila (show all and list plus inode))
    * ln [target] [linkname]
    * ln /etc/hosts myhosts 
    * ln -s myhost symhost
    * ln path_to_target path_to_link_file
    * Only hardlink to files not folders (only files on same filesystem)
* List, set, and change standard ugo/rwx permissions 
    * ls -l 
    * chown user:[group] file (to set user-ownership)
    * chgrp group file (to set group ownership)
    * chown lisa:sales newfiles/ (change user and group)
    * chown :sales newfile/ (change group ownership with chown)
    * chmod (change file permissions)
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
    * who [OPTION] ... [ FILE | ARG1 ARG2 ] (reading man page options)
        * [ ] optional ... multiple options
        * | OR indicator 
    * --help (man has more information)
    * man man
    * man -k (-K to go through them)
    * sudo mandb (rebuild man pages)
    * /usr/share/doc

## Create simple shell scripts 

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
            * [ COND1 ] || [ COND2 ] - OR operator
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
            * for i in `cat file`;do echo $i;done (can be any command)
        * for i in *.txt;do echo $i;done (*) THIS will look at any .txt file in current dir
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
        * $? (exit code of the previous command)
    * read -p "Enter in something" choice (read input into a variable called choice)
        * read variable (without the prompt)
* Processing output of shell command within scripts 
    * Specify exit codes within a script 
        * exit 1 (within the script and can exit the script with a specific code like under else statement)
    * break statement (breaks and exits the loop whether while or for)
    * contiune statement 
        * execution back to the beginning of the loop

## Operate running systems 

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
            * in the linux kernel line add systemd.unit=rescue.target (boot into the rescue target)
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
        * ps aux (all users)
        * ps fax (all forest)
        * ps lax (all long listing to see nice)
        * ps -U user (see processes for a specific user - ps -fU user)
        * ps u 1 (process ID - ps 1)
        * ps PID
        * pgrep -a bash (might be helpful but look at both with regular grep)
        * echo $$ (see the current shell procress ID)
    * top 
        * Shows most CPU intensive ones 
        * q to exit
        * arrows and pager buttons 
    * Signals 
        * kill -L (important to see all signals)
        * kill -9 PID (send a 9 (SIGKILL) to the PID)
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
        * logictl user-status <UID> (show a tree of processes currently open by this user)
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
        * tuned-adm profile_info (get info about a profile no option shows current)
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
        * journalctl -o (output string so specify verbose journalctl -o verbose)
        * logger -p err hello (write to logger then use journalctl -p err to see it)
    * /etc/logrotate.conf
        * systemctl list-unit-files -t timer 
        * systemctl status logrotate.timer
        * systemctl cat logrotate.service 
        * /etc/logrotate.conf 
        * man logrotate *(has great config examples)*
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
        * lsof 
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
        * rsync -a * server:/home/student/
        * Most common options 
            * -r (recursive sync the entire dir tree)
            * -l (sync symbolic links)
            * -p (preserve symbolic links)
            * -n (dry run before sync)
            * -a (archive mode)
            * -A (archive mode and also sync ACLs)
            * -X (sync SELinux context as well)


## Configure local storage 

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
        * GPT is more often used
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

## Create and configure file systems 

* create, mount, unmount, and use vfat, ext4, and xfs filesystems
    * mkfs.ext4
    * mkfs.xfs
    * mkfs.vfat 
    * man mkfs.xfs
    * xfs_admin (admin xfs fs)
    * tune2fs (admin ext fs ext4)
    * mkfs.xfs -L (create the label as well as the FS)
    * maybe look at lvm vdo?
* mount and unmount network file systems using NFS
    * Server config (may not be needed)
        * dnf install nfs-utils 
        * mkdir -p /nfsdata /home/ldap/ldapuser{1..9}
        * echo "/nfsdata *(rw,no_root_squash)" >> /etc/exports (*)
        * echo "/home/ldap *(rw,no_root_squash)" >> /etc/exports (*)
        systemctl enable --now nfs-server
        * for i in nfs mountd rpc-bind;do firewall-cmd --add-service $i --permanent;done
        * firewall-cmd --reload
    * Make sure nfs-utils are installed
    * showmount -e nfserver (show exports available)
    * mount nfsserver:nfsdata /mnt (mounting the specific share nfs data)
    * fstab (just in case)
        * node01:/share /mnt nfs defaults 0 0 (nfsserver:share_dir /mount_point_local nfs defaults 0 0)
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
        * sudo setfacl --modify user:aaron:rw exampleFile
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
 

## Delpoy, configure, and maintain systems 

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
        * sudo systemctl disable sshd.service (disable will not come up on boot)
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
        * rpm -qf filename (shows from which package filename was installed like /usr/bin/ls)
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
                        * enable and disable CHECK (dnf repolist --enable Repo_ID - dnf repolist --disable Repo_ID)
                        * dnf config-manager --enable REPO_ID (--disable REPO (actually enable and disable repos))
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


## Managing basic networking 

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

## Manage users and groups 

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

## Manage security 

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
        * /etc/ssh/sshd_config (d for daemon server config)
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
    * semanage fcontext -a (set a new context label)
    * semanage fcontext -m (modify an existing context label)
    * restorecon (enforce the policy setting on the filesystem)
    * touch /.autorelabel (relabel the files to the context specified in the policy)
    * man semanage-fcontext (documentation)
    * semanage fcontext -l -C (show settings that have changed in the current policy)
    * man pages for selinux-policy-doc
    * semanage fcontext -a -t http_sys_content_t "/web(/.*)?" (*)
    * restorecon -Rv /web (restorecon -R -v /web (man pages))
* manage SELinux port labels
    * semanage port -a -t ssh_port_t -p tcp 2022
        * semanage port -a -t http_port_t -p tcp 81
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

## Manage containers 

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
            * podman run -it (interactive mode)
        * podman stop (stops a currently running container)
        * podman ps (shows information about containers)
            * podman ps -a
        * podman build (builds an image from a containerfile)
        * podman images (lists images)
        * podman inspect (shows container or image details)
        * podman pull (pulls an image from the registry)
        * podman exec (executes a command in a running container)
        * podman rm (removes a container)
    * skopeo (additional information needed)
        * skopeo inspect image (inspect remote images)
        * skopeo inspect --config image
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




