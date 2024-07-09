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

## Working with text files 

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

## Connecting to RHEL 9

