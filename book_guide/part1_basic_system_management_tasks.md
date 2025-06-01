# Part 1 Performing Basic System management tasks

## Chapter 1 Installing Red Hat Enterprise Linux 

* Going through the intro 
* Make sure not to forget about the bonus content 
* Installing Red Hat enterprise Linux
    * Setting up an environment to perform all exercises in the book 
* Do I know this already quiz 
    * Answers in appendix A 
    * Topic sections
    * Preparing to install red hat enterprise Linux 
    * Performing an install 
    * Questions: 
    * Might be good to go back an review these 
* Foundation Topics 
* Prearing to install red hat enterprise linux 
    * Learn what RHEL is 
    * How to get access to the software 
    * Set up requirements 
    * Next section is the actual install 
    * What is RHEL 9 Server?
        * RH developer subscription
        * When you pay for Red Hat Enterpirse linux Red hat offers you a supported enterprise linux OS 
        * Which has some key benefits taht are a normal requirement in corpo environments 
        * Monitored updates and patches that have gone through a thorough testing procedure 
        * Different levels of support and help, depending on which type of subscription you have purchased 
        * A certified OS that is guaranteed to run and to be supported on specific HW models 
        * A certified platform for running enterprise applications such as SAP midddleware, Oracle Database, and more 
        * Access to RH Customer Portal access.redhat.com, where you can find detailed documentation that is avilable to customers only 
    * Not all of this potential customers are interested in these features 
    * RH offers two free alternatives also 
        * CentOS stream
        * Fedora 
    * Apart from these there are also two community initiatives to provide free alts to RHEL 
    * Contain the same software but without Red Hat branding 
        * Rocky 
        * Alma 
* Getting the software 
    * Using Red hat enterprise Linux 
        * Developer program to get access for free
        * The most important thing you get in the official RHEL 9 server release is access to Red Hat Customer Portal 
        * Thru the portal you have access to a wide variety of information regarding RHEL 
        * In addition to updates provided through RHN (Red Hat Network)
        * The knowledge base is invaluable 
        * Also can find answers to common problems that have been posted there by Red Hat consultants 
    * Using CentOS stream
        * CentOS is the Community Enterprise OS 
        * Started as a recompiled version of RHEL 
        * With all items that were not available for free removed from RHEL software 
        * Before 2020, CentOS provided a good and completely free alt to RHEL 
        * In the past years, RH acquired CentOS and changed it policy 
        * Now they provide CentOS stream
        * CentOS stream is a linux distro where new features that will be release in the next version of RHEL are introduced 
        * In the RHEL development cycle, new feature are introduced in Fedora 
        * After testing in Fedora some features are introduced in CentOS stream
        * Which is used as the last testing platform before the features are included in RHEL 
        * New features are continuously integrated in CentOS stream, and for that reason, it doesn't know any sub versions such as RHEL 9.1 
        * Making CentOS stream a bad candidate for production environements 
    * Other Distros 
        * Fedora 
        * Latest and greatest software 
        * Recommended not to use Fedora to prepare for the exam 
        * Testing grounds 
        * Alma and Rocky 
        * Community distros that provide the same software as RHEL but without any lincense restrictions or support 
        * No way supervised by red hat 
        * If you want to use 100 percent compatible alt for RHEL without being bound by any license conditions 
* Understanding access to repositories 
    * An important difference between RHEL and other distros is the access to repositories 
    * A repo is the installation source used for installing software 
    * If you are using free software such as AlmaLinux, correct repos are automatically set up and no further action is required 
    * If you are using RHEL with a subscription, you will need to use the Subscription manager software to get access to repos 
    * If you install RHEL 9 installation disc but do not register it, you will not have access to a repo
    * Which is why you will need to know how to set up a repo access manually 
    * Key skill covered in Chap 9
* Setup requirements 
    * RHEL 9 can be installed on physical hardware and virtual hardware 
    * Does not matter much as long as the following minial conditions are met 
        * 1 GiB of Ram 
        * A 10-GiB hard disk 
        * A network card 
    * These requirements are minimal 
    * Requirements to perform all exercises in the book 
        * 64 bit platform support either Intel or ARM 
        * 2 GiB of RAM 
        * 20 GiB hard disk 
        * Dvd drive either virtual or physical 
        * network card 
* Cert Guide Environment Description
    * Installing on real hardware (less flexible)
    * Recommends using a virtual machine for snapshots 
    * Not KVM tho as it is not well supported 
* TIP 
    * In the chapter there will be step by step exercises that tell you exactly how to configure specific services 
    * At the end of the chapter you will find a end of chapter lab
    * These are very close to the real questions on RHCSA 
    * So it is suggested to start from a clear environment for the end of chapter labs 
* Performing an installation
    * Even if RHEL 9 can be installed from other media such as an installation server or USB key, the most common installation starts from the installation DVD
    * Or if you are working in a virtual machine from the installation DVD ISO file 
    * So take your installation DVD (or its ISO) and boot the computer on which you want to install the software 
        1. After booting from DVD you will see RHEL9 Boot menu from here you can choose four different options 
            * Install RHEL 9.0 - For normal installations 
            * Test this media and install RHEL 9.0 - Select if you want to test the installation media first 
            * Note testing will take a significant amount of time and should not be necessary in most cases 
            * Troubleshooting - Select this option for some troubleshooting options. 
            * USEFUL if you cannot boot normally from your computers hard drive after RHEL has been installed on it 
            * When the installation program starts, you can pass boot options to the kernel to enable or disable specific features 
            * To get access to the prompt where you can add these options, press TAB from the installation menu 
            * This shows you the kernel boot line that will be used and offers an option to change boot parameters 
        1. To Start a normal installation, select Install RHEL 9.0 boot option (sub version may change)
        1. Once the base system from which you will perform the installation has loaded, you see the Welcome to Red Hat Enterprise Linux 9.0 screen
            * From this screen you can select language and keyboard settings 
            * English 
            * Select the appropriate settings and click continue to proceed 
        1. After keyboard and lanugage selection you will see the installation summary screen
            * From this screen you can specify all settings you want to use 
            * There are several different options
            * Keyboard: Used to change the keyboard disposition
            * Language support: Used to add support for additional languages 
            * Time and date: Used to specify the current time and date as well as time zone 
            * Root password: used to disable the root user, and if this user is enabled set a password 
            * User creation: Used to create a non root user account and optionally mark this user as an admin
            * Connect to Red Hat: Used to register your system with Red Hat before starting the installation
            * Notice that all exercises in this book assume that your system is not installed with red hat 
            * Installation source: used to specify where to install from
            * Typically install from the installation DVD which is referred to as local media 
            * Software selection: Offers different installation patterns to easily install a default set of packages 
            * Installation destination: Used to ID to which disk to copy files during installation
            * KDUMP: Allows you to use a KDUMP kernel 
            * This is a core dump if anything goes wrong 
            * Network and host name: Allows you to set IP address and related settings here
            * Security profile: Offers a limited set of security policies enabling you to easily harden a server 
            * From this installation summary screen, you can see whether items still need to be configured 
            * Marked with an exclamation mark and a description in red text 
            * As long as any issues exist, you cannot click the begin installation button
        1. Click keyboard option to view the settings to config the keyboard layout 
            * Secondary keyboard layout, useful if your server is used by admin using different keyboard layout 
            * Not only are different language settings supported but also different hardware layouts 
            * For example if a admin is using Apple Mac computer you can select keyboard layout for Mac in the appropriate region
            * Can also configure layout switching options 
            * Key sequence that is used to switch between different kinds of layouts 
            * Select Options to specify the key combo you want to use for this purpose 
            * After specifying the config you want to use click done, to return to the installation summary screen
        1. The Language Support option on the installation summary screen is the same as the language support option used in step 3
            * If you already configed the language you do not need to change anything here 
        1. Click time and date to see a map of the world on which you can easily click the time zone that you are in
            * Alternatively, you can select the region and city you are in from the corresponding drop down list boxes 
            * You can also set the current date and time
            * And after setting the network, you can specify the NTP (Network time protocol) to be used to sync time with time servers on the internet 
            * This option is not accessible if the network is not accessible 
            * You will have to set up the network connection first 
            * When using network time, you can add the network time servers to be used by clicking the configuration icon in the upper right of the screen
            * After specifying the settings you want to use, click done 
        1. Root password 
            * By default the root user account is disabled 
            * If you want to be able to work as root you need to set a password here 
            * Enter password twice, and click done 
        1. User creation option
            * setting a full name and username 
            * Make this user admin 
        1. Installation source 
            * If you have booted from a regular installation disk, there is nothing to specify 
            * If you have booted from a minimal boot environment, you can specify the network URL where additional packages are available, as well as additional repositories that need to be used 
            * Don't have to do this for the RHCSA exam but if you are ever setting up an installation server it is useful to know 
        1. Software selection
            * You can select the base environment and choose additional software available for the selected environment 
            * Minimal install option is very common 
            * Allows you to install RHEL on a minimal size hard disk, providing just the essential software and nothing else 
            * Server with GUI option for this book 
            * Would never be done on a production server 
            * But for the RHCSA exam there are some task that need to be performed on the easy to use graphic tools available 
            * All additional packages can be added later 
            * Some tools discussed in this book only run on a GUI 
        1. Where you want to install to 
            * Installation Destination 
            * By default automatic partitioning is selected and you only need to approve the disk device you want to use for automatic partitioning 
            * Many advanced options are available as well 
            * You can install using the automatic option under storage configuration to ensure that no matter how your server is started everything is configured to have it boot correctly and your file systems are configured with the default XFS file system 
        1. Networking and Host name 
            * Have to configure something 
            * Set the hostname to server1.example.com
            * Default settings for now (DHCP) more on networking in chapter 8
        1. Security policy option does not need any change 
        1. After specifying all settings from the installation summary screen options, you click begin installation to start the installation
            * This will begin the installation procedure 
        1. When the installation has completed you will need to Reboot System to restart the computer and finalize the installation
        1. After rebooting you have to go through a couple of additional setup steps to set up your user environment 
            * Take a tour
            * Prompt that the system is not registered 
            * NOT register the system at the moment as it will complicate all the exercises about repo management in chapter 9
* Summary 
    * RHEL is and how it relates to some other linux distributions 
    * Install RHEL 9
    * You are now ready to set up basic environment that you can use to work on all the excercises in the book 
* Exam prep tasks 
* Review all key topics 
    * How to perform a RHEL 9 installation
* define key terms 
    * Distribution
    * Linux 
    * Red hat
    * CentOS
    * Fedora 
    * Alma Linux 
    * Rocky Linux 
* review questions
    * page 64 and 65
* End of chapter lab 

## Chapter 2 Using Essential Tools 

* The following topics are covered in this chapter 
    * Basic shell skills 
    * Editing files with vim
    * Understanding the shell environment 
    * find help
* The following exam objectives are covered in this chapter
    * Use input output redirection
    * access a shell prompt and issue commands with correct syntax 
    * Create and edit text files 
    * Locate, read, and use system documentation including man, info, and files in /usr/share/doc 
* Chapter 2 Using Essential Tools 
    * This chapter is dedicated to coverage of the basic linux skills that everyone should have before RHCSA 
* Do I know this already quiz 
    * Did pretty well on this 
* Foundation Topics 
* Basic Shell skills 
    * The shell is the default working environment for a linux admin
    * Bash is the most common shell 
    * Unstanding commands 
        * Working with the shell is all about working with command syntax 
        * Typically command syntax has three basic parts 
        * The command 
        * its options 
        * and its arguments 
        * the command itself: for example ls
        * ls is the command itself and show a list of the files in the current dir 
        * To modify the behavior of the command, you can use options
        * Options are a part of the program code, and they modify what the command is doing 
        * -l (option with the ls command, a long listing of filenames and properties is displayed)
        * The word argument is a bit confusing 
        * Generally speaking it refers to anything that the command addresses, so anything you put after the command is an arg 
        * Including the options 
        * Apart from the options that can be used as arugments, commands can have other arguments as well, which serve as target to the command 
        * Looking at this in context of the command: ls -l /etc 
        * This command has two different arguments -l and /etc 
        * The first arg is an option
        * It modifys the behavior of the command 
        * The second arg is a target, specifying where the command should do its work 
        * You will find these three elements in nearly all commands you work with in a linux environment 
    * Executing commands 
        * The purpose of the linux shell is to provide an environment in which commands can be executed 
        * The shell takes care of interpreting the command that a user has enter correctly 
        * To do this the shell makes a distinction between the three kinds of commands 
            * Aliases 
            * Internal commands 
            * External commands 
        * An alias is a command that a user can define as needed 
        * Some aliases are provided by default 
        * type alias on the command line to get an overview 
        * To define an alias use: alias newcommand='oldcommand'
        * for example: ll='ls -l --color=auto'
        * This is created on the system by default 
        * Aliases are executed before anything else
        * So if you have a command called ll and a alias ll (the alias will always take precedence over the command)
        * Unless you use a absolute path like /usr/bin/ls 
        * An Internal command is a command that is a part of the shell itself, and does not have to be loaded from disk separately
        * An external command is a command that exists as an executable file on the disk of the computer 
        * Because it has to be read from disk the first time it is used it is a bit slower 
        * When a user executes a command, the shell first looks to determine whether it is an internal command 
        * If not it looks for an executable file with a name that matches the command on disk 
        * To see if a command is a Bash internal command or an executable file on disk use type 
        * type pwd 
        * To find out that the pwd command that will be executed is really an alias 
        * To change how external commands are found by the shell use the $PATH variable 
        * This variable defines a list of directories that is searched thru for a matching filename when a user enters a command 
        * To find out which exact command the shell will be using, use the which command 
        * which ls 
        * To find out where the shell will get the ls command from 
        * An even strong command is type, which will also work on internal commands and aliases 
        * You will notice that (for security reasons) the pwd is not in PATH 
        * That is why you need to start a command that is in the current dir but not in PATH with ./
        * The dot stands for the current dir and you are telling bash to look in the current dir 
        * PATH variable can be set for specific users but in general most users will be using the same PATH variable 
        * The only exception to this is the root user 
        * Root needs access to specific admin commands 
    * Exercise 2-1 Using internal and external commands from shell 
        1. Authenticate to the server1 that you created in Chapter 1 as the user created in Chapter 1 
        1. Open a terminal, all exercises in this book are intended to be executed in a terminal 
        1. Type: time ls (this executes the ls command where the bash internal time shows information about the time it took to complete this command)
        1. Type: which time 
            * This shows the file /usr/bin/time that was found in this $PATH variable 
        1. type time (which shows you that time is a shell keyword?)
        1. echo $PATH (shows the content of the $PATH variable)
            * You can see that /usr/bin is included in the list, but because there also is an internal command time, the time command from the path will not be executed unless you tell the shell specifically to do so.
            * The command in step 3 has executed the internal command for you because of the command precedence 
        1. /usr/bin/time ls (to run the /usr/bin/time command when executing ls) 
            * You will notice the out differs 
            * What matters for now is that you realize that these are two different commands 
    * I/O redirection
        * By default when a command is executed it shows its results on the screen of the computer you are working on
        * The computer monitor is used as the standard destination for output, which is also referred to as STDOUT
        * The shell also has default standard destinations to send error messages to (STDERR) and to accept input (STDIN)
        * STDIN
            * Computer keyboard by default 
            * Use in redirection (< (same as 0<))
            * File descriptor number = 0
        * STDOUT 
            * Computer monitor by default 
            * Redirection > (same as 1>)
            * File descriptor number = 1 
        * STDERR
            * Compter monitor by default 
            * 2> (use in redirection)
            * File descriptor number = 2
        * So if you run a command, that command would expect input from the keyboard, and it would normally send its output to the monitor of your computer without making a distinction between normal output and errors 
        * Some commands however are started in the background and not from a current terminal session
        * So these commands do not have a monitor or console session to send their output to 
        * And they do not listen to keyboard input to accept their standard input 
        * This is where redirection comes in handy 
        * Redirection is also useful if you want to work with input from an alternative location, such as a file 
        * Programs started from the command line have no idea what they are reading from or writing to 
        * They just read from what the linux kernel calls file descriptors 
        * 0 if they want to read from standard input, 
        * Write to file descriptor number 1 to display non error output (standard output)
        * And file descriptor 2 if they have error messages to be output
        * By default these file descriptors are connected to the keyboard and the screen
        * If you use redirection symbols such as <, >, and |, the shell connects the file decriptors to files or other commands 
        * > (same as 1>)
            * redirects STDOUT
            * If redirection is to a file, the current contents of that file are overwritten
        * >> (same as 1>>) 
            * Redirects STDOUT in append mode 
            * If output is written to a file, the  output is appended to that file 
        * 2> Redirects STDERR
        * 2>&1 
            * Redirects STDERR to the same destination as STDOUT 
            * NOTE that this has to be used in combo with normal output redirection
            * As in ls whuhiu > errout 2>&1 
        * < (same as 0<)
            * Redirects STDIN
        * In I/O redirection, files can be used to replace the default STDIN, STDOUT, and STDERR
        * You can also redirect to device files 
        * A device file on Linux is a file that is used to access specific hardware 
        * Your hard drive for instance can be referred to as /dev/sda in most cases 
        * The console of your server is known as /dev/console or /dev/tty1
        * And if you want discard a commands output, you can redirect to /dev/null 
        * Note that to access most device files, you need to have root privileges 
    * Using Pipes 
        * A pipe can be used to catch the output of one command and use that as input for a second command 
        * ls for instance the output is shown onscreen because the screenis teh default STDOUT 
        * If you use ls | less the commands ls and less are started in parallel 
        * The standard output of the ls command is connected to the standard input of less 
        * Everything that ls writes to the standard output will become available for reading from standard input in less 
        * By combining commands using pipes, you can created super commands that make almost anything possible (used alot by admins)
    * Exercise 2-2 Using I/O redirection and Pipes 
        1. cd without any args 
        1. pwd to verify current dir = users home directory 
        1. ls command and output on screen
        1. ls > /dev/null 
            * Redirects STDOUT to the null device, and you will not see it 
        1. ls ilwehgi > /dev/null 
            * This command shows no such file or dir message onscreen
            * You see this because it is not STDOUT, but rather an error message that is written to STDERR
        1. ls ilwehgi 2> /dev/null 
            * Now you will no longer see the error message 
        1. ls ilwehgi /etc 2> /dev/null 
            * This shows the content of the /etc folder while hiding the error message 
        1. ls ilwehgi /etc 2> /dev/null > output 
            * Still write the error message to /dev/null while sending STDOUT to a file with the name output that will be created in your home (curren dir) dir 
        1. cat output 
            * Shows the content of the output file 
        1. echo hello > output 
            * Overwrites teh contents of the output file 
            * Verify this by using cat output again
        1. ls >> output 
            * This appends the results of the ls command to the output file 
            * cat output to verify 
        1. ls -R /
            * Shows a long list of files and folders 
            * Ctrl C to stop (or wait for it to complete)
        1. ls -R / | less 
            * Shows the same results but in the less pager 
        1. q to close less (will also end the ls program)
        1. ls > /dev/tty1 
            * This throws an error because you are executing the command as an ordinary user 
            * Ordinary users cannot address device files directly (unless you are logged into tty1)
            * Only the user root has permission to write to device files directly 
    * History 
        * Bash history 
        * Bash is configed by default to keep the last 1000 commands a user used 
        * When a shell session is closed, the history of that session is updated to the history file 
        * The name of this file is .bash_history and it is created in the home dir of the user who started a specific shell session
        * Notice that the history file is written to only when the shell session is closed
        * Until that moment all commands in the history are kept in memory 
        * The history feature makes it easy to repeat complex commands
        * There are several ways to work with history 
        * history to show a list of all commands in the the bash history 
        * Ctrl r (to open the prompt from which you can do backward searches in commands that you have previously used
            * Type a string and Bash will look backward in the command history for any command containing that string as the command name or one of its arguments 
            * Press Ctrl r again to repeat the last backward search 
        * !number (to execute a command with a specific number from history)
        * history -d number
            * To delete a specific command from history 
            * This wil renumber all other lines in history 
        * !sometext (execute the last command that starts with sometext)
            * Notice that this is potentially dangerous as the command that was found is executed immediately 
        * history -c (clear the history)
        * If you want to remove both the current history and the content of the .bash_history file, then use history -w (immediately after running the history -c command)
        * history -d number (remove a specific command from history)
    * Exercise 2-3 Working with History 
        1. Make sure you have an open shell session
        1. history (get an overview of commands that have previously been used)
        1. Type some commands 
            * ls 
            * pwd
            * cat /etc/hosts
            * ls -l 
        1. Open a second terminal session
        1. History (you should not see the commands from the first session, the history file has not been updated yet)
        1. Ctrl r (first terminal session)
            * From the prompt that opens type ls 
            * Ctrl r again
            * You are looking backward and that the previous ls command is highlighted enter to execute it 
        1. history | grep cat 
            * grep command searches the history output for any commands that contain the text cat
            * Note the command number
        1. !nn (where nn is the number from the previous step)
        1. Close terminal with exit command
        1. history -c (in the other terminal sessions)
        1. Open a new terminal session and check the history 
            * history -c clears the in memory history, but does not remove the .bash_history file in the home dir 
    * Bash Completion
        * Helps you to find the command that you need, and it also works on variables and filesnames 
        * Type the beginning of a command and then TAB 
        * Bash should complete the command for you automatically 
        * If there are several options, you need to press TAB once more to get an overview of all the available options
    * Exercise 2-4 Using Bash Completion
        1. gd (TAB) nothing will happen
        1. Press TAB again (bash shows a short list of all commands that start with the letters gd)
        1. To make it clear type i (gdi) then TAB should autocomplete to gdisk, press enter to launch it (and enter again to close it)
        1. cd /etc
        1. cat pas (TAB), Since there is only one file that starts with pas bash should autocomplete to passwd (enter to execute)
* Editing Files with vim 
    * Managing Linux often means working with files 
    * Most things that are configed on Linux are configed thru files 
    * Often need to change the contents of a config file with a text editor 
    * Alot of editors but vi is the one that matters 
    * Only one that is always available 
    * Everything in this section about vim works with vi 
    * Different modes 
    * command and insert mode 
    * TIP about vimtutor (dnf install vim-enhanced)
    * Table 2-4 vim Essential Commands 
        * Esc 
            * Switches from input mode to command mode
        * i, a 
            * Switches from command mode to input mode at (i) or after (a) the current cursor position
        * o
            * Open a new line below the curren cursor and goes to input mode
        * :wq
            * Writes the current file and quites 
        * :q!
            * Quits the file without applying changes
            * ! forces the command to do its work 
            * Add the ! only if you really know what you are doing 
        * :w filename 
            * writes the current file with a new filename 
        * dd 
            * deletes the current line and places the contents of the deleted line into memory 
        * yy 
            * copies (yanks) the current line
        * p 
            * pastes the contents that have been cut or copied into memory 
        * v 
            * Enter visual mode
            * Select a block of text using the arrow keys (d to cut or y to copy the selection)
        * u
            * undo the last command. Repeat as often as necessary 
        * Ctrl-r 
            * redo the last undo (cannot be repeated more than once)
        * gg 
            * goes to the first line of the doc 
        * G 
            * goes to the last line of the doc 
        * /text
            * searches for text from the current cursor position forward 
        * ?text 
            * searches for text from the current cursor position backward 
        * ^ 
            * goes to the first position in the current line
        * $
            * goes to the last position in the current line
        * !ls
            * adds the output of ls (or any other command) in the current file 
        * :%s/old/new/g
            * Replaces all occurrences of old with new 
    * Exercise 2-5 vim Practice 
        1. vim ~/testfile (to open up a test file in home dir)
        1. i (to enter insert mode)
            * type in some multi line text, cow, sheep, ox, chicken, snake, fish, oxygen
        1. Press esc to get back to command mode and type :w to write the file 
        1. :3 (go to line number 3)
        1. dd (delete the line)
        1. dd again (delete another line)
        1. u (undo the last deletion
        1. o (open a new line)
        1. Enter some more text, tree, farm
        1. Esc (back to command mode)
        1. :%s/ox/OX/g (change ox to OX globally)
        1. :wq (write and quit) :wq! (write and quit force)
* Understanding the shell environment 
    * When working from a shell, an environment is created to ensure that all that is happening is happening the right way 
    * Special variables that define the user environment (like $PATH)
    * This section will give a brief overview of the shell environment and how it is created 
    * Unstanding variables 
        * Variables are fixed names that can be assigned dynamic values 
        * $LANG
        * Advantage of working with variables for scripts and programs is that program only has to use the name of the variable without taking interest in the specific value that is assigned to the variable
        * Because different users have different needs, the variable that are set in a user environment will differ
        * env command (get an overview of the current variables defined in the env)
        * env will show environment variables that are used to set important system settings 
    * Example 2-1 Displaying the current environment
        * env (that is it) and example output
        * to define a variable, you type the name of the variable, followed by = and the value that is assigned to the specific variable 
        * echo $PATH (to read the variable)
    * Recognixing environment configuration files 
        * When a user logs in, an env is created for the user automatically 
        * This happens based on four config files, where some code cna be specified and where variables can be defined 
        * /etc/profile 
            * this is the generic file that is processed by all users upon login
        * /etc/bashrc
            * This file is processed when subshells are started 
        * ~/.bash_profile
            * In this file, user specific login shell variables can be defined 
        * ~/.bashrc
            * In this user specific file, subshell variables can be defined
        * distinction between login shell and subshell
        * Login shell = first shell that is opened after a user logs in
        * From the login shell, a user may run scripts, which will start a subshell of that login shell 
        * Bash allows for the creation of different environment in the login shell and in the subshell 
        * But to make sure the same settings are used in all shells, it is a good idea to include subshell settings in the login shell as well 
    * Using /etc/motd and /etc/issue
        * To display messages during the login process
        * Bash uses the /etc/motd and the /etc/issue files 
        * Messages in /etc/motd display after a user has successfully logged into a shell (not in a gui)
        * Using /etc/motd can be useful to inform users about an issue or a security policy 
        * Another way to send information is by using /etc/issues 
        * The contents of this file display before the user logs in from a text based console interface 
        * Using this file provides an excellent means of specifying login instructions to users who are not logged in yet 
    * Exercise 2-6 manage the shell environment 
        1. Open a shell 
        1. echo $LANG (shows contents of the variable that sets your system keyboard and lang settings)
        1. ls --help (help about the ls command)
        1. LANG=es_ES.UTF-8 (temp sets the language variable to Spanish try ls --help again)
        1. exit to close the terminal (because you did not change the files, when you open a new shell the OG value for LANG should be used)
        1. Open another shell 
        1. verify the language settings again (echo $LANG)
        1. vim .bashrc (open the .bashrc configuration file)
        1. add the line COLOR=red (set a variable named COLOR and assign it the value red, just a variable)
        1. Close the shell and open a new one
        1. Verify the variable COLOR has been set (echo $COLOR)
        * because the .bashrc file is included in the login procedure, the variable is set after login
* Finding Help 
    * Alot of commands on a linux system to many to every remember all of them 
    * Using help resources is very important 
    * man command 
    * Most important resource for getting help about command syntax and usage 
    * can show a compact list of command options by using command --help also 
    * Using --help 
        * Quickest way to get an overview is to use the --help option
        * Nearly all commands will display a usage summary when using this option
        * Use mainly if you already know and understand the command and need a quick overview of options available with the command 
    * Using Man
        * man command 
        * The most important parts of the man page (in general) are at the bottom of the man page 
        * Two important sections
        * examples 
        * See also section
        * G (to get to the bottom of the man pages)
        * /example (to search for example in a man page)
    * Finding the right man page 
        * apropos or man -k (search the mandb)
        * man -k KEYWORD
        * Looks in the summary of all man pages that are stored in the mandb database
        * Note this searches only the short summary of each command that is installed 
        * sometimes you might get alot of information returned (which you can filter down with grep)
        * Man pages are categorized in different section (most important for system admins are)
            * 1: Executable programs or shell commands 
            * 5: File formats and conventions 
            * 8: System admin commands 
        * There are also sections that provide in depth details about your linux system, such as the sections about system calls and library calls 
        * man -k will get results from all of these sections
        * To limit results it makes sense to use grep to filter for what you need 
        * so if you are looking for the configuration file that has something to do with passwords 
            * man -k password | grep 5
        * If you are looking for the command that an admin would use to create partitions, 
            * man -k partition | grep 8
        * -f 
        * The command man -f <somecommand> (displays a short description of the item as found in the mandb database)
        * Might help you when deciding whether this man page contains the information you are looking for 
    * Updating mandb
        * man -k consults the mandb
        * This database is automatically created through a schedule job
        * Might need to update the db manually 
        * mandb (run as root without any args)
        * Looks to see whether new man pages have been installed and update the mandb database accordingly 
        * TIP dont memorize all the commands you need to accomplish specific tasks - learn how to find the commands and find what is needed from the man page 
    * Exercise 2-7 Using man -k 
        1. Make sure you are logged in as the student account 
        1. Look at the man page for man to see additional information about man -k (it is not returning expected results)
            * man man
            * /-k (to search for the arg)
            * Can read the man page for apropos to see more detail 
        1. man apropos 
            * see that the database searched by apropos is updated by the mandb program
        1. man mandb
            * explains how to run mandb to update the mandb database 
        1. sudo mandb (to update the mandb database)
    * Using info 
        * Most commands are documented in man pages, but some commands have their main documentation in the info system and only show a short usage summary in the man page
        * pinfo or info commands 
        * pinfo (easier special items such as menu items are clearly indicated)
        * Info pages are organized like web pages, which means that they are organized in a hierarchical way 
        * n to go to the next page 
        * p to go to the previous page 
        * u to move up in the hierarchy 
        * Menus 
        * Each item that is marked with an * is a menu item 
        * Use arrows keys to select a specific menu item 
        * This brings you one level down
        * u to get back up again
    * Exercise 2-8 Using info 
        * man ls (G to go to the end) 
            * look at the see also section
            * says full documentation is maintained as a texinfo manual that can be shown with the info command 
        * pinfo '(coreutils) ls invocation'
            * Shows the information about ls usage in the pinfo page 
            * Read thru it and press q when done 
            * can also use info, pinfo has better formatting (but not installed by default on ubuntu)
    * Using /usr/share/doc Documentation files 
        * /usr/share/doc dir
        * These files are avialable in particular for services and larger systems that are a bit more complicated 
        * Not find much about ls but some services do provide useful information in /usr/share/doc
        * Some services store very useful information in this dir
        * Like rsyslog, bind, kerberos, and OpenSSL 
        * For some services even sample files are included 
* Summary 
* Complete tables and lists from memory 
* define key terms 
    * shell
    * bash
    * internal commands
    * external commands
    * $PATH
    * STDIN
    * STDOUT
    * STDERR
    * redirection
    * file descriptor
    * device file
    * pipe 
    * environment
    * variable 
    * login shell 
    * subshell 
* Review questions
* End of chapter lab
    * You should be able to complete the lab without any additional help
    * Review these labs 

## Chapter 3 Essential File Management Tools 

* Following topics are covered in the chapter 
    * working with the file system hierarchy
    * Managing files 
    * Using links 
    * Working with archives and compressed files 
* The following RHCSA exam objectives are covered in this chapter 
    * Create, copy, delete, and move files and directories
    * Archive, compress, unpack, and uncompress files using tar, star, gzip, and bzip2
    * Create hard and soft links 
* Essential file management tools 
    * Linux is a file oriented OS 
    * This means that many of the things admins have to do on Linux can be traced down to managing files on the Linux OS 
    * When using HW devices, files are involved 
    * Essential file management skills 
    * Working with files and dirs 
    * How linux file system is organized 
    * Links and compressed or uncompressed archives
* Do I know this already quiz 
* Foundation Topics 
* Working with the file system hierarchy
    * Be familiar with the default dirs that exist on almost all linux systems 
    * Describe these dirs and explain how mounts are used to compose the file system hierarchy
    * Defining the file system hierarchy 
        * FHS (Filesystem Hierarchy standard)
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
            * contains process and user specific information that has been created since the last boot
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
    * Unstanding Mounts 
        * In order to understand the organization of the linux file system you need to understand the important concept of mounting 
        * A mount is a connection between a device and a dir
        * Linux file system is presented as one hierarchy, with the root directory (/) as its starting point
        * This hierarchy may be distributed over different devices and even computer systems that are mounted into the root directory 
        * In the process of mounting, a device is connected to a specific dir
        * Such that after a successful mount this directory gives access to the device contents 
        * Mounting devices make it possible to organize linux file system in a flexible way 
        * Not good to store all files in just one file system, which gives several good reasons to work with multiple mounts 
            * High activity in one area may fill up the entire file system, which will negatively impact services running on the server 
            * If all files are on the same device, it is difficult to secure access and distinguish between different areas of the file system with different security needs 
            * By mounting a separate file system, you can add mount options to meet specific security needs 
            * If a one device file system is completely filled, it may be difficult to make additional storage space available 
        * To avoid these pitsfalls, it is common to organize linux systems in different devices (and even shares on other computer systems)
        * Such as disk partitions and logical volumes, 
        * And mount these devices into the file system hierarchy 
        * By configuring a device as a dedicated mount, you also are able to use specific mount options that can restrict access to the device 
        * Some dirs are commonly mounted on dedicated devices 
        * /boot
            * This dir is often mounted on a separate device because it requires essential information your computer needs to boot 
            * Because the root dir (/) is often on a LVM (logical volume manager) logical volume, from which Linux cannot boot by default 
            * The kernel and associated files need to be stored separately on a dedicated /boot device 
        * /boot/EFI
            * If a system uses Extensible firmware interface (EFI) for booting, a dedicated mount is required
            * Giving access to all files required in the earliest stage of the boot procedure 
        * /var 
            * This dir is often on a dedicated device because it grows in a dynamic and uncontrolled way 
            * For example because of the log files that are written to /var/log
            * By putting it on a dedicated device, you can ensure that it will not fill up all storage on your server 
        * /home 
            * This directory often is on dedicated device for security reasons
            * By putting it on a dedicated device, you can mount it with specific options, such as noexec and nodev, to enhance security of the server 
            * When you are reinstalling the OS it is an advantage to have home dirs in a seperate file system
            * The home dirs can then survive the system reinstall 
        * /usr
            * This dir contains OS files only, 
            * To which normal users normally do not need any write access 
            * Putting this directory on a dedicated device allows admins to configure it as a read only mount 
        * Apart from these dirs, you may find servers that have other dirs that are mounted on dedicated partitions or volumes also 
        * It is up to the discretion of the admin to decide which dirs get their own dedicated devices 
        * mount 
            * command gives an overview of all mounted devices 
            * To get this information, the /proc/mounts files is read, where the kernel keeps information about all current mounts 
            * It shows kernel interfaces also, which may lead to a long list of mounted devices being displayed 
            * Example output page 99
        * df -Th 
            * command was designed to show available disk space on mounted devices
            * It includes most of the system mounts 
            * bc it will look on all mounted filed systems, it is a convenient command to use to get an overview of current system mounts 
            * -h option summarizes the output of the command in human readable format 
            * -T option shows which file system type is used on the different mounts 
        * findmnt
            * shows mounts and the relationship that exists between the different mounts 
            * The mount command might have alot of information (findmnt might be alittle more managable)
            * Note bc of width limitations of the book page, output that belongs in the OPTIONS column appear on the left side of the page 
        * Exercise 3-1 Getting an overview of current mounts 
            * Login and type mount 
                * Output can be overwhelming 
                * Read carefully you will see a few directories from the Linux dir structure and their corresponding mounts
            * df -hT
                * Lot fewer devices are shown
                * Example output page 101
        * Looking closer at the df command output 
        * The output of df is shown in 7 columns 
            * Filesystem
                * The name of the device file that interacts with the disk device that is used
                * The real device in the output start with /dev (which refers to the dir that is used to store device files)
                * You can also see a couple of tmpfs devices 
                * These are kernel devices that are used to create a temporary file system in RAM 
            * Type 
                * The type of file system that was used 
            * Size 
                * The size of the mounted device
            * Used 
                * The amount of disk space the device has in use 
            * Avail
                * The amount of unused disk space 
            * Use%
                * The percentage of the device that currently is in use 
            * Mounted on
                * The dir the device currently is mounted on 
        * df command the size is reported in kibibytes
        * -m will display these in mebibytes
        * -h will display human readable format in KiB, MiB, GiB, TiB, or PiB
* Managing Files 
    * As an admin you need to be able to do the following 
        * Working with wildcards
        * managing and working with dirs 
        * Working with absolute and relative pathnames 
        * Listing files and directories 
        * Copying files and dirs 
        * moving files and dirs 
        * Deleting files and dirs 
    * Working with wildcards 
        * A wildcard is a shell feature that helps you refer to multiple files in an easy way 
        * * (astrick) refers to an unlimited number of any characters
            * ls * shows all files in the current dir (except hidden files)
        * ? 
            * Used to refer to one specific character that can be any character 
            * ls c?t would match cat and cut 
        * [auo]
            * refers to one character that may be selected from the range that is specified between square brackets
            * ls c[auo]t would match cat, cut, and cot 
    * Managing and working with dirs 
        * To organize files, linux works with dirs (also referred to as folders)
        * Already went over default dirs as defined by FHS
        * When users start creating files and storing them on a sever it makes sense to provide a dir structure as well
        * As an admin you have to be able to walk through the dir structure 
    * Exercise 3-2 working with dirs 
        1. Open a shell
            * cd
            * pwd (print working dir)
            * Should be in the home directory /home/usrname
        1. touch file1
            * Creates an empty file with the name file1 on your server 
            * BC you are in the home dir you can create any file you want to 
        1. cd /
            * changes to the root dir 
            * touch file2 (should get permission denied)
            * Ordinary users can create files only in dirs where they have permission to do so 
        1. cd /tmp
            * brings you to the tmp directory 
            * All users should have write permission
            * touch file2 
            * Creates the file2 file in the /tmp directory (unless there is already a file2 that is owned by somebody else)
        1. cd 
            * back to the home dir 
        1. mkdir files 
            * creates a dir with the name files in the current dir 
            * Uses the name of the dir that need to be created as a relative pathname; relative to where you are 
        1. mkdir /home/$USER/files 
            * Using the variable $USER (subs in your current username)
            * This is an absolute filename to the files dir that you are creating
            * But the file already exist 
        1. rmdir files
            * removes the files dir that you just created 
            * rmdir will remove the directory, but only if the dir is empty and does not contain any files 
    * Working with absolute and relative pathnames 
        * cd and mkdir in the last exercise 
        * touched on relative and absolute filenames/pathnames
        * Absolute filename 
            * or absolute pathname
            * a complete path reference to the file or dir you want to work with 
            * Pathname starts with the root directory, followed by all subdirs up to the actual filename 
            * No matter what your current dir is, absolute filenames will always work 
        * Relative filename 
            * relative to the current directory 
            * pwd shows the current dir 
            * Good distinction ../oneup/onedown (is not absolute actually relative to the current dir)
            * It contains only the elements that are required to get from the current directory up to the item you need 
        * TIP if you are newer to linux always use absolute pathnames to avoid mistakes 
        * Bash completion works on filenames
    * Listing files and directories 
        * ls (show the contents of the current directory)
        * Common args 
            * ls -l (long listing)
                * includes information about file properties, such as creation date and permissions 
            * ls -a (show all files, including hidden files)
            * ls -lrt
                * -t option shows commands sorted based on modification date 
                * You will see the most recently modified files last in the list because of the -r option
                * Useful command 
            * ls -d 
                * Shows the names of directories
                * Not the contents of all dirs that match the wildcards that have been used with the ls command 
            * ls -R 
                * Shows the contents of the current dir
                * in addition to all of its subdirs 
                * RECURSIVELY decends all subdirs 
        * Hidden files start with a dot
    * Copying files and directories 
        * cp (command)
        * cp a single file 
            * cp /<path to file> /<path to destination>
            * cp /etc/hosts /tmp (copies /etc/hosts to /tmp)
        * If you copy a file to a dir but the target dir does not exist, a file will be created with the name of the alleged target dir
            * better to get an error and you can do so with a / after the dir name 
            * cp /etc/hosts /tmp/ (instead of cp /etc/hosts /tmp)
        * -R option 
            * recursively copy an entire subdir, with its contents and everything beneath it 
            * Will also see -R with many other linux commands (might be -r also)
            * cp -R /etc /tmp (copy the dir /ect and everything in it to the dir /tmp)
        * With cp you need to consider permissions and other properties of the file 
            * Without extra options, you risk these properties not being copied 
        * If you want to keep the current permissions, use the -a option
            * cp in archive mode 
            * This option ensures that permissions and all other file properties will be kept while copying 
            cp -a ~ /tmp (copy an exact state of the home dir to /tmp)
        * Hidden files with cp 
        * By default hidden files are not copied over 
        * Three solutions when working with hidden files and cp 
            * cp /somedir/.* /tmp
                * This copies all files that ahve a name starting with . (dot) over to /tmp
                * It gives an error message for DIRS whose name starts with a dot in /somedir, because -R option is not used 
            * cp -a /somedir/ . 
                * This copies the entire directory /somedir, including its contents, to the current directory (.)
                * A subdir somedir will be created in the current dir 
            * cp -a /somedir/. .
                * This copies all files, regular or hidden to the current dir 
                * Notice the space between the two dots at the end of this command 
    * Moving files and directories 
        * mv (command)
        * Removes the files from its current location and puts it in the new location
        * can also be used to rename a file 
        * Examples 
            * mv myfile /tmp
                * Moves the myfile file from the current dir to /tmp
            * mkdir somefiles; mv somefiles /tmp
                * First creates the dir somefiles 
                * Then moves the dir to /tmp
                * This will also work if the dir contains files 
            * mv myfile mynewfile
                * Renames the file myfile to a new file with the name mynewfile 
    * Deleting files and directories 
        * file deletion
        * rm (command)
        * When used on a single file the single file is removed 
        * Can also be used on a dir that contains files (-r option for recursive)
        * On RHEL 9 if you use rm command as root it prompts for confirmation
        * This is because rm is defined as an alias rm -i in /root/.bashrc
        * You can use the -f option (force) or remove the alias from /root/.bashrc (if you want to)
        * And be careful if you remove this 
    * Exercise 3-3 Working with files 
        1. Open a shell as a ordinary user 
        1. pwd (to see current dir)
            * Should be in /home/$USER
        1. mkdir newfiles oldfiles 
            * ls (should see the two new dirs just created, as well as anything else that was already in the user home dir)
        1. touch newfiles/.hidden; touch newfiles/unhidden
            * This creates two files in the dir newfiles 
        1. cd oldfiles
        1. ls -al 
            * This shows two items .. and . (for current dir and parent dir)
        1. ls -al ../newfiles 
            * relative pathname to refer to the contents of the /home/$USER/newfiles dir
        1. cp -a ../newfiles/ .
            * Notice the space between the / and the . at the end of the command
        1. ls -a 
            * You see that you have created subdir newfiles into the dir oldfiles 
        1. Within /home/$USER/oldfiles, type rm -rf newfiles
        1. cp -a ../newfiles/* . 
            * ls -al to see what has been copied now 
            * You should see the hidden file has not been copied 
        1. Make sure you copy hidden files as well as regular files 
            * cp -a ../newfiles/. .
        1. ls -al (verify the command worked this time 
            * Should see the hidden files as well as the regular files have been copied successfully 
* Using Links 
    * Links on Linux are like aliases that are assigned to a file 
    * Symbolic and hard links 
    * need to have alittle background in inodes
    * Understanding hard links 
        * Linux stores administrative data about files in inodes 
        * The inode is used to store all administrative data about files 
        * Every file on linux has an inode, and in the inode, important information about the files is stored 
            * The data block where the file contents are stored 
            * The creation, access, and modification date 
            * Permissions 
            * File owners 
        * Just one important piece of information is not stored in the inode: the name of the file 
        * Names are stored in dirs
        * And each filename knows which inode it has to address to access further file information
        * An inode does not know which name it has; it just knows how many names are associated with the inode 
        * These names are referred to as hardlinks 
        * So every file always has one hard link to start with, which is the name of the file 
        * When you create a file, you give it a name, basically this name is a hard link 
        * Multiple hard links can be created to a file 
        * This is useful if a file with the same contents needs to be available at multiple locations, and you need an easy solution to keep the contents the same 
        * *If a change is applied to any one of the hard links, it will show in all other hard links as well, as all hard links point to the same data blocks*
        * Some restrictions apply to hard link tho 
            * Hard links must exist all on the same device (partition, logical volume, etc)
            * You cannot create hard links to dirs 
            * When the last name (hard link) to a file is removed, access to the files data is also removed 
        * Nice thing about hard links is that there is no difference between the first hard link and the second hard link 
        * The are both just hard links
        * So if the first hard link that ever existed for a file is removed, that does not impact the other had links that still exist 
        * Linux OS uses links on many locations to make files more accessible 
    * Understanding Symbolic Links 
        * A symbolic link or soft link does not link directly to the inode but to the name of the file 
        * This makes symbolic links much more flexible, but it also has some disadvantages 
        * Advantages 
            * They can link to files on other devices, as well as on directories 
        * Major disadvantage 
            * When the OG file is removed, the symbolic link becomes invalid and does not work any longer 
        * Page 110 to see a schmetic overview of how inodes, hard links, and symbolic links related to one another 
    * Creating Links 
        * ln (command) to create links 
        * It uses the same order of parameters as cp and mv 
        * First mention the source name, followed by the destination name 
        * Symbolic links will use -s option (as well as specify the source and target file or dir)
        * Important restriction applied: to be able to create hard links, you must be the owner of the item that you want to link to
    * ln usage examples 
        * ln /etc/hosts . 
            * creates a link to the file /etc/hosts in the current dir 
        * ln -s /etc/hosts . 
            * creates a symbolic link to the file /etc/hosts in the current dir 
        * ln -s /home /tmp 
            * Creates a symbolic link to the directory /home in the directory /tmp
    * The ls command will reveal whether a file is a link
        * output of ls -l, the first character is an l if the file is a symbolic link 
        * If a file is a symbolic link, the output of ls -l shows the name of the item it links to after the filename 
        * If a file is a hard link, ls -l shows the hard link counter 
        * NOTE: use \ in front of a command to execute it without the alias 
    * Removing links 
        * Removing links can be dangerous 
        1. Make a test dir: mkdir ~/test
        1. cp /etc/[a-e]* ~/test (cp all files that have a name starting with a, b, c, d, or e from /etc to the test dir 
        1. ls -l ~/test/ (veiw and verify the contents of that dir)
        1. Go back to the users home dir with cd 
        1. ln -s test link
        1. rm link (removes the symbolic link (do not user -r or -f to remove symbolic links even if they are subdirs)
        1. ls -l (Should see the symbolic links have been removed)
        1. ln -s test link (to create the link again)
        1. rm -rf link/ 
        1. ls (you will see the dir link still exists)
        * ls test/ (should see the test dir is now empty)
    * Exercise 3-4 Working with Symbolic Links and hard links 
        1. Open a shell as the regular (student) user 
        1. From the home dir type: ln /etc/passwd . (Should not allow you since you are not the owner of /etc/passwd)
        1. ln -s /etc/hosts (if the target is not specified the link is created in the current dir 
        1. touch newfile (and create a hard link to this file) ln newfile linkedfile
        1. ls -l (Should see the hard link counter for newfile and linkedfile is currently set to 2)
        1. ln -s newfile symlinkfile (to create a symbolic link to newfile)
        1. rm newfile 
        1. cat symlinkfile (This should give no such file or dir as the original file could not be found)
        1. cat linkedfile (this gives no problems)
        1. ls -l (look at the way the symlinkfile is displayed, also look at linkedfile, the link counter should now be 1)
        1. ln linkedfile newfile 
        1. ls -l (should see the original situation has been restored)
* Working with archives and compressed files 
    * Another important file related task is managing archives and compressed files 
    * tar (command) often used to create an archive of files on Linux 
    * tar was originally designed to stream files to a tape without any compression of the file, and it still does not compress anything by default 
    * If you want to compress files as well you have to either use a specific compression tool or specify an option that compresses the archive while it is being created 
    * Managing archives with tar 
        * Tape ARchiever (tar)
        * Used to archive files 
        * Originally designed to stream files to a backup tape, in its current use tar is used mostly to write files to an archive file 
        * You have to be able to perform 4 important tasks with tar on the RHCSA 
            * Create an archive 
            * list the contents of an archive 
            * extract an archive 
            * compress and uncompress archives 
    * Creating archives with tar
        * tar -cf archivename.tar /files-you-want-to-archive (to create an archive)
        * -v option (to see what is happening)
        * To archive files, you need at least read permissions on the file and execute permissions on the dir the file resides in 
        * tar -cvf /root/homes.tar /home (as the root user)
            * Writes the contents of /home dir and everything below it to the file home.tar in the directory /root
            * The order of the options are important 
        * Originally tar did not use the dash (-) in front of its options 
            * Modern tar uses the dash, as well as all other linux programs
            * Still allow the old usage without a dash for backward compatibility 
        * Possible to add a file to an existing archive or to update an archive 
            * -r (add a file to an archive)
            * tar -rvf /root/homes.tar /etc/hosts (adds /etc/hosts file to the archive)
            * update a currently existing archive file you can use -u option
            * -u 
            * tar -uvf /root/homes.tar /home (to write newer versions of all files in /home to the archive
    * Monitoring and extracting tar files 
        * Before extracting good to know what to expect
        * -t option (can be used to find out)
        * tar -tvf /root/homes.tar (to see the contents of the tar archive)
        * TIP: good form to create archive files with an extension such as .tar or .tgz 
        * Not everybody will do this so can you file command to analyze its contents
        * tar -xvf /archivename.tar (to extract the contents of an archive)
        * This extracts the archive in the current directory 
        * Note this means if you are in /root
            * tar -xvf /root/homes.tar
            * And the file contains a dir /home, 
            * after extracting you will have a new dir /root/home that contains the entire contents of the file 
        * Two solutions to put the extracted contents right where you want to have them 
            * Before extracting the archive file, use cd to get into the dir where you want to extract the files 
            * Using the option -C /targetdir (specify the target dir where you want to extract the file to
                * tar -xvf homes.tar -C /tmp
        * NOTE: RHCSA objectives mention working with star
            * star utility was designed to offer support for archiving nondefault file attributes, such as ACL or SELinux file contents
            * current release tar offers this functionality 
            * So no real need to use star any more 
            * Also notice it is not included in default installation patterns any more 
        * Can also extract one file out of an archive 
            * tar -xvf /archivename.tar file-you-want-to-extract
            * tar -xvf /root/etc.tar etc/hosts
    * Using Compression 
        * Compression programs allow you to make files take less disk space by taking out redundancy
        * If there is no redundancy you won't gain much by using compression
        * In all of the tar examples nothing has been compressed 
        * Originally, after you created the archive it has to be compressed with a separate compression utility such as gzip or bzip2
        * After creating home.tar you can compress it with gzip creating home.tar.gzip
        * The compressed version of home.tar (taking up less space)
        * bzip2 is a alt to gzip 
        * Not much difference now, but originally bzip2 used a more efficient encrpytion algo resulting in smaller file sizes 
        * Another alt for compressing files is xz utility (more recent)
        * To decompress files that have compressed with gzip or bzip2, you can use gunzip and bunzip2 
        * Instead of using the utilities directly 
            * you can use:
            * -z (gzip)
            * -J (xz)
            * -j (bzip2)
            * While creating the archive with tar
            * This immediately compresses the archive while it is created 
        * Don't have to use this option when extracting
        * Tar will recognize the compressed content and automatically decompress it for you
    * Table 3-6 Overview of tar options
        * c
            * creates an archive 
        * v (shows verbose output while tar is working)
        * t (shows the contents of an archive)
        * z (compresses/decompresses the archive while creating it, using GZIP)
        * j (Compresses/decompresses the archive using BZIP2)
        * J (Compresses/decompresses the archive using XZ)
        * x (extract an archive)
        * u (updates an archive; only newer files will be written to the archive)
        * C (changes the working dir before performing the command)
        * r (appends files to an archive)
    * Exercise 3-5 using tar
        1. Open a root shell (should be in roots home dir)
        1. tar cvf etc.tar /etc (archive the contents of the /etc dir)
        1. file etc.tar (should tell you it is a tar archive)
        1. gzip etc.tar (compress the tar file, packages it into the file etc.tar.gz)
        1. tar tvf etc.tar.gz 
            * tar should not have any issue with the compressed archive
            * Also notice that the archive contents consists of all relative filenames
        1. tar xvf etc.tar.gz etc/hosts 
        1. ls -R 
            * A subdir etc should be created in the current dir 
            * In the subdir the file hosts has been restored there 
        1. gunzip etc.tar.gz (decompresses the compressed file but does not change anything with regards to the tar command)
        1. tar xvf etc.tar -C /tmp etc/passwd 
            * Extracts the password file including its relative pathname to the /tmp dir
            * ls -l /tmp/etc/passwd to verify 
        1. tar cjvf homes.tar /home 
            * This creates a compressed archive of the home directory in roots home dir 
        1. rm -f *zg *tar (remove all files resulting from exercises in this chapter from the roots home dir)* 
* Summary 
    * Review all key topics 
* Complete tables and lists from memory 
* Define key terms 
    * FHS (file system hierarchy standard)
    * Mount 
    * root dir
    * device
    * directory/folder
    * absolute filename
    * path
    * relative filename
    * inode
    * hard link
    * symbolic link
    * tar
    * star
    * compression
    * gzip
    * bzip2 
    * xz
* Review questions
* end of chapter lab

## Chapter 4 Working with text files 

* The following topic are covered in this chapter 
    * Using common text file related tools 
    * A primer to using regex 
    * using grep to analyze text
    * Working with other useful text processing utilities 
* The following RHCSA exam objectives are covered in this chapter 
    * Use grep and regex expressions to analyze text 
    * create and edit text files 
* Working with text files 
    * Everything you do on linux is stored as a text file 
    * By applying the correct tools, you will easily find and modify the config of everything
* Do you already know quiz 
* Foundation Topics 
* Using common text file related tools 
    * Before looking at finding text files containing specific text, look at how to display text in an efficient way 
    * Table 4-2 Essential Tools for managing text file contents 
        * less 
            * Opens the text file in a page, which allows for easy reading
        * cat 
            * dumps the contents of the text file on the screen
        * head 
            * shows the top of the text file 
        * tail 
            * shows the bottom of the text file 
        * cut 
            * used to filter specific columns or characters from a text file 
        * sort 
            * sorts the contents of a text file 
        * wc 
            * counts the number of lines, words, and characters in a text file 
    * These commands might prove helpful when used with pipes 
    * less /etc/passwd (to open the password file in less)
    * But can also use ps aux | less (which sends the output of ps aux to the less pager for easier reading)
    * Doing more with less 
        * using less 
        * convenient way to read files 
        * Page up and page down keys on the keyboard 
        * q to quit 
        * /sometext (search)
        * ?sometext (backward search)
        * n to repeat last search 
        * Similar behavior in vim and man 
        * NOTE: Less was suppose to take over for more (but more has been enhanced as well)
            * does not really matter that much which one you use 
            * However more utility ends if the end of the file is reached 
            *  more -p (to prevent this)
            * More is also on all systems by default where less might be less common
    * Exercise 4-1 Applying basic less skills 
        1. less /etc/passwd (open /etc/passwd file in the less pager)
        1. /root (to lok for the text root)
            * You should see that all occurrences of the text root are highlighted 
        1. Press G to go to the last line 
        1. Press q to quit less 
        1. ps aux | less (output of ps aux command into the pager less)
        1. q to quit less 
    * Showing file contents with cat 
        * Less is useful for long text files 
        * If not too long might be better off with cat 
        * Cat just dumps the contents of the text file on the terminal it was started from 
        * Great for short text files 
        * Longer text files might only show what fits on the terminal (hard to scroll up to see the start of the file)
        * cat /etc/passwd (to show the content of the file to the screen)
        * TIP: tac (reverse order of cat (cat is beginning to end) (tac is end to beginning))
    * Displaying the first or last lines of a file with head and tail 
        * head (command on a text file to show default 10 first lines of a file)
        * tail (command on a text file to show default last 10 lines of a file)
        * -n (adjust the number of lines you want to see)
        * tail -n 5 /etc/passwd (last 5 lines of the /etc/passwd file)
        * TIP: older versions of tail and head you had to specify n (newer version you do not tail -5 /etc/passwd == tail -n 5 /etc/passwd)
        * Another useful option with tail is -f 
        * -f (option starts by showing you the last ten lines of the file, but it refreshes the display as new lines are added to the file)
        * Useful for log files 
        * tail -f /var/log/messages (which has to be run as root)
        * Can be combined together to be helpful 
        * head -n 11 /etc/passwd | tail -n 1 
        * This will print the first 11 lines with head and the just grab the last line with tail (if you want to display the 11th line of the file)
    * Exercise 4-2 Using basic head and tail operations 
        1. From a root shell tail -f /var/log/messages (should see the last lines of the file, the file does not close automatically)
        1. Ctrl-c to quick the previous command
        1. head -n 5 /etc/passwd (show first five lines in /etc/passwd)
        1. tail -n 2 /etc/passwd (show last two lines of /etc/passwd)
        1. head -n 5 /etc/passwd | tail -n 1 (show only line number 5 of the /etc/password file)
    * Filtering specific columns with cut 
        * Filtering out specific fields 
        * See a list of all users in /etc/passwd 
        * cut (command)
        * -d option (delimiter)
        * -f option (field)
        * cut -d : -f 1 /etc/passwd (will filter the first field with the delimiter : in the /etc/passwd file)
        * Example results on page 128
    * Sorting file contents and output with sort 
        * sort (sorts text)
        * sort /etc/passwd (sorted in byte order)
        * cut -f 1 -d : /etc/passwd | sort (sorts just the first column of the /etc/passwd file)
        * By default sort command sorts in byte order (order in which the characters appear in the ASCII text table)
        * So not specifically alphabetical order 
        * For example capital letters are shown before lowercase 
        * Zoo before apple 
        * Other types of data (like numeric or another format)
        * sort -n (numeric order)
        * sort -rn (sort in reverse numeric order)
        * Sort can also sort by specific column 
        * sort -k3 -t : /etc/passwd (field separator : and the 3rd column of etc passwd)
        * Not this just sorts that column does not give it to you like cut 
        * ps aux | sort -k 4 -n (sort the 4th column assume the default is spaces of the output of ps aux command (numeric too))
    * Counting lines, words and characters with wc 
        * wc (command word count)
        * Before handling large files (or files in general) might help to get an idea of the amount of text is in the file
        * wc output gives three different resultes 
        * Number of lines 
        * number of words 
        * and number of characters 
        * ps aux | wc 
* A primer to using regular expressions 
    * Working with text files is important 
    * Not just how to create and modify existing text files, but also how to find text files that contains specific text 
    * Not always clear which specific text you are looking for 
    * flexible patters known as regular expressions
    * regex 
    * Looking at last six lines of /etc/passwd file to start
    * Now you are looking at a specific user 
    * general regular expression parser grep
    * grep user /etc/passwd 
    * But this might return multiple results depending on the user and text file 
    * Regular expression is a search pattern that allows you to look for specific text in an advanced and flexible way 
    * Using line anchors 
        * The type of regular expression that specifies where in a line of output the result is expected is known as a line anchor 
        * ^ (grep ^user /etc/passwd (looking only at the start of the line))
        * $ (states that the line ends with some text: grep ash$ /etc/passwd)
        * This will show all lines in /etc/passwd that end with the text ash (as in any user/account that have a shell and are abel to login)
    * Using escaping in regular expression
        * Not mandatory, but a good idea to use escaping to prevent regular expression from being interpreted by the shell 
        * When a command line is entered, bash parses the command line looking for any special characters like *, $, and ? (*)
        * To make sure bash does not interpret these characters you should escape them (for the purposes of regex)
        * Many cases not really necessary, in some cases, the regex will fail without escaping 
        * To prevent this from happening, a good idea to put the regex between quotes 
        * grep ^anna /etc/passwd == grep '^anna' /etc/passwd
    * Using wildcards and multipliers 
        * . (wildcard)
        * To look for one specific character 
        * r.t (would match rat, rot, and rut)
        * range of characters 
        * [ ]
        * r[aou]t (would match rat, rot, and rut, but not rit or ret)
        * * (multiplier matches zero or more of the previous character)
        * re\{2\}d (specifiy the number you are looking for here we would match reed but not red)
        * ? (matches zero or one of the previous character)
    * Using extended regular expressions 
        * different sets of regular expressions 
        * Base regular expressions (discussed so far) are supported by tools like grep 
        * Set of extended regular expressions that are not supported by default 
        * when using grep you will need to add the -E option to indicate it is an extended regular expression
        * + (indicate a character should occur one or more times 
        * ? (to indicate a character should occur zero or one times)
        * But use -E to indicate extended regular expressions 
    * Table 4-3 Most significant regular expressions
        * ^text (matches line that starts with specific text)
        * text$ (matches lines that ends with specific text)
        * . (wildcard (matches any single character))
        * [abc] (range matches a, b, or c)
        * ? (extended regular expression that matches zero or one of the preceding character)
        * + (extended regular expression that matches one or more of the preceding character)
        * * (matches zero to infinite number of the previous character)
        * \{2\} (matches extact two of the previous character)
        * \{1,3\} (matches a minimum of one and a maximum of three of the previous characters 
        * colou?r
            * Matches zero or one of the previous chracter
            * This makes previous character optional
            * match color or colour 
        * (...) (used to group multiple characters so that the regular expression can be applied to the group 
    * Looking at an example regex from man page semanage-fcontext
        * Relates to managing SELinux 
        * "/web(/.*)?" (*)
        * ? (means the part between the braces may occur zero or one times 
        * Within the braces starts the slash (so this means just the dir name gives a match, but also the dir name followed by just a slash, or a slash that is followed by a filename)
        * Two common extended regular expressions are + and ? 
        * + (will look for a pattern where the preceding character occurs one or more times)
        * ? (looks for a pattern where the preceding character does not occur or occurs one time 
        * Example procedure 
            1. create a text file with bat, boot, boat, and bt on seperate lines 
            1. grep 'b.*t' textfile (*) (see any lines that start with a b and end with a t)
            1. grep 'b.+t' textfile (this does not work because its an extended regular expression and grep does not recognize it)
            1. grep -E 'b.+t' text file (now you should see the expression work correctly)
* Using Grep to analyze text 
    * ultimate utility to work with regular expressions is grep 
    * general regular expression parser 
    * Table 4-4 Most useful grep options 
        * -i (matches upper and lowercase letters (not case sensitive))
        * -v (shows only lines that do not contain the regular expression)
        * -r (searches files in the current directory and all subdirs)
        * -e (searches for lines matching more than one regular expression, use -e before each regular expression you want to use)
        * -E (Extended regular expression (interprets the search pattern as an extended regex))
        * -A <number> (show <number> of lines after the matching regular expression)
        * -B <number> (shows <number> of lines before the matching regular expression)
    * Exercise 4-3 Using Common Grep Options 
        1. grep ' #' /etc/services (should show multiple lines with the comment sign #)
        1. grep -v '^#' /etc/services (filter out the lines that have the comment at the beginning of the line)
        1. grep -v '^#' /etc/services -B 5 (Shows lines that do not start with # and the fives lines that are directly before each of those lines)
            * useful because the preceding lines typically show comments on how the specific parameter works
            * However will also display multiple blank lines most cases 
        1. grep -v -e '^#' -e '^$' /etc/services (This excludes all blank lines and lines that start with #)
* Working with other useful text processing utilities 
    * awk and sed 
    * Developed before screens where common place, and they do a great job of treating text files in a scripted way 
    * Do not need to be specialist in these utilities any longer 
    * But it does make sense to know how to perform some common taks using these utilities 
    * awk -F : '{ print $4 }' /etc/passwd (print out the 4 field of the password file with -F as the delimiter :)
    * awk -F : '/user/ { print $4 }' /etc/passwd 
        * This will search the password file for the text user and will print out the 4th field of any matching lines 
    * sed -n 5p /etc/passwd 
        * Print the 5th line from the password file 
    * Sed is very powerful for filtering text from text files 
    * But added benefit that it also allow you to apply modifications to text files
    * sed -i s/old-text/new-text/g ~/myfile 
        * searches for the text old-text in ~/myfile 
        * And replaces all occurrences with the text new-text 
        * By default sed will write to STDOUT but -i writes results to the file 
        * Be careful as it might be hard to revert file modifications that are applied this way 
    * sed -i -e '2d' ~/myfile 
        * delete a line based on a specific line number
        * sed -i -e '2d;20,25d' ~/myfile (delete lines 2 and 20-25 in myfile)
    * TIP: do not focus on awk and sed to much (they are very rich)
* Summary 
    * Working with text files 
    * grep to search texts files 
    * regex 
    * alittle awk and sed 
* Exam prep tasks 
* Review all key topics 
    * Essential tools for managing text files contents 
    * Definition of a regular expression
    * most significant regular expressions
    * most useful grep options
* Complete tables and list from memory 
* Define key terms 
    * Pager
    * regular expression
    * line anchor
    * escaping 
    * wildcard
    * multiplier 
* Review questions
* Lab 4.1 

## Chapter 5 Connecting To red hat enterprise linux 9

* The following topics are covered in this chapter 
    * Working on local consoles 
    * Using ssh and related utilities 
* The following RHCSA exam objectives are covered in this chapter 
    * Access remote systems using SSH
    * Log in and switch users in multiuser targets 
    * Boot, reboot, and shutdown system normally 
    * Securely transfer files between systems 
    * Configure key based auth for SSH 
* Do I know this already quiz 
* Foundation topics 
* Working on a local console 
    * Console (the environment the user is looking at)
    * Terminal (environment that is opened to the console and provides access to a nographical shell, typically bash)
        * The command line env that can be used to type commands 
        * Can be offered thru a window while using a GUI
        * remote terminal via ssh 
        * the only thin you see in a textual console 
    * You can have multiple terminals open on a console, you can not have multiple consoles open in one terminal 
    * Logging in to a local console 
        * Generally there ware two way to make yourself known to a linux server 
        * Sit at the linux console and interactively log in from the login prompt that is presented 
        * Other cases a remote session is established 
        * To login from a text console, you need to know which user account you should be 
        * Logging in as root 
        * RHEL 9 you can indicate while installing if the root user should have a password or not
        * If the root user does not get a password you will only be able to log in with an administrator user 
        * This user can only obtain root thru sudo 
        * Reasons not to log in as root and use a locally defined user instead 
            * Logging in this way will make it more difficult to make critical errors 
            * On many occasions you will not need root permissions anyways 
            * If you only allow access to normal users and not root. Forces attacks to guess the username and password 
            * sudo -i will open a root shell. If you have sudo privileges
            * su - (if you know the root user password) sudo -i only works for authed user and requires user password not roots passwd
            * sudo to configure specific admin taks for specific users only 
    * Switching between terminals in a graphical environment 
        * Opening terminal in GUI 
        * terminals are opened as subshells, and do not require login again (get access to the user account you logged into the GUI with)
    * Exercise 5-1 Working with several terminal windows simultaneously 
        1. Log into GUI with non root user 
        1. Open a terminal '
        1. Select new window from the terminal menu
        1. From one terminal window use sudo -i
            * tail -f /var/log/secure (to start looking at the file and update it over time)
            * Monitor security events in real time 
        1. From the other terminal window use su - 
            * enter a wrong password for root 
        1. Should see the error message written to the tail session 
        1. Ctrl-c to close the tail session
    * Working with multiple terminals in a nongraphical environment 
        * In nongraphical env you have only one terminal interface that is available, making working in different user shell env a bit more difficult 
        * Virtual terminal 
            * Option to make working with several consoles on the same server possible 
        * Allows you to open 6 different terminal windows from the same console at the same time and use key sequences to navigate between them 
        * To open these terminal windows, you can use the key sequences Alt-F1 through Alt-F6 
        * Following virtual consoles are available 
            * F1 (gives access to the GNOME display manager (GDM) graphical login)
            * F2 (Provides access to the current graphical console)
            * F3 (Gives access back to the current graphical session)
            * F4-F6 (Gives access to nongraphical consoles)
        * TIP: chvt (command)
            * Enables you to switch to a different virtual env directly from the current env
            * chvt 4, chvt3, chvt 1 
        * Of these virtual consoles the first one is used as the default console 
        * Commonly known as virual console tty1 
        * /dev/tty1 
        * All have corresponding device files, /dev/tty1 - /dev/tty6
        * Graphical env requires Ctrl-Alt-Function
        * NOTE: Used to be dumb terminals connected to an OS (nothing more than a keyboard and screen) These days have passed 
    * Understanding pseudo terminal devices 
        * Every terminal used in a Linux env has a device file associated with it 
        * Terminals on nongraphical env are referred to typically as /dev/tty1 thru /dev/tty6
        * For terminal windows that are started from a graphical env pseudo terminals are started 
        * These pseudo terminals are referred to using numbers in the /dev/pts dir 
        * So first terminal from a graphical env appears as /dev/pts/1 
        * Second /dev/pts/2 (and so on)
        * NOTE: Eariler versions of Linux Pseudo terminals were seen as pty devices 
            * depracted and replaced with pts terminal types 
    * Exercise 5-2 Working with Pseudo Terminal
        1. Log in to graphical console, using a non root user 
        1. Open a terminal window 
        1. w (command, gives an overview of all users who are currently logged in)
            * Notice the column that mentions the tty the users are on, in which you see tty2 that refers to the terminal window
        1. Open another graphical terminal. become root (su -)
        1. w (command again)
            * Notice that the second su - session does not show as an additional user account 
            * This is because both have been started from the graphical interface which is tty2 
    * Should know how to work with console, terminals, virtual terminals, and pseudo terminal at this point 
    * Booting, Rebooting, and shutting down systems 
        * As an admin you may have to occasionally reboot linux servers 
        * Rebooting is not often a requirement 
        * But can make your work easier bc it will make sure that all processes and task that are running have to reread their configs and initializ properly 
        * TIP Reboot a linux server is an important task for the exam 
            * Everything configd for the exam should still be working after the server has rebooted 
            * So make sure to reboot at least once during the exam but also after making critical modifications to the server config 
            * If your server cannot reboot anymore after applying critical modifications to your servers config at least know where yo look to fix issues 
        * For an admin who really knows linux thoroughly, rebooting a server is seldom necessary 
        * Experienced admins can often trigger the right parameter to force a process to reread its configs 
        * There are some scenarios tho that will require a reboot 
            * To recovery from a serious problem such as server hangs or kernel panics 
            * to apply kernel updates 
            * to apply changes to kernel modules that are being used currently and therefore cannot be reloaded easily 
        * When a server is rebooted, all processes that are running need to shutdown properly 
        * If the server is justed stopped by pulling the plug, data could be lost 
        * Reason being processes that have written data do note typically write that data directly to disk, 
            * But instead store it in memory buffers (a cache) from where it is committed to disk when it is convenient for the OS 
        * To issue a proper reboot you have to alert systemd process
        * Systemd process is the first process that was started when the server was started 
        * Also responsible for managing all other processes, directly or indirectly 
        * So on system reboot or halt, systemd process needs to make sure that all these processes are stopped 
        * To tell the systemd process this has to happen you can use a few commands 
            * systemctl reboot (or reboot)
            * systemctl halt (or halt)
            * systemctl poweroff (poweroff)
        * When stopping a machine you can use the systemctl halt command or the systemctl poweroff command 
            * The difference between these two commands is that poweroff talks to power management on the machine to shut off power on the machine 
            * This often does not happen with using halt
        * NOTE: Emergency reset option
            * Might prove useful if the machine is not physically accessible
            * To force a machine to reset from a root shell (echo b > /proc/sysrq-trigger)
            * This command resets the machine without saving anything 
            * Should only be used if there is no other option
* Using SSH and related utilities 
    * Learned how to access a terminal if you have direct access to the server console 
    * Sometimes work with servers that are not physically accessible 
    * SSH (secure shell)
    * SSH is the common method to gain access to other machines over the network 
    * cryptography is used to ensure that you are connecting to the intended server 
    * traffic is encrypted while being transmitted 
    * Accessing remote systems using SSH 
        * To access a server using ssh you need the sshd server process as well as an SSH client 
        * On the remote server that you want to access the sshd service must be running and offering services, which it does at its default port 22 
        * And it should not be blocked by the firewall 
        * After install RHEL starts the sshd process automatically and by default it is not blocked by firewall 
        * If the ssh port is open you can access it using the ssh command from the command line 
        * ssh command by default tries to reach the sshd process on the server over port 22 
        * if you need to specify the port:
        * ssh -p <portnumber>
        * ssh command is available on all linux distros, and on apple mac computers as well 
        * ssh is not a native part of windows (outside of WSL)
        * ssh client like putty 
        * Putty can allow different types of remote sessions to be established with linux machines 
        * alternative SSH clients for windows are available as well: mobaxterm, Kitty, mremoteng, bitvise, and xshell
        * accessing another linux machine from a linux terminal is easy 
        * ssh followed by the name or IP address of the other linux machine 
        * After connecting you will be prompted for a password if a default config is used 
        * This is the password of a user account with the same name as your current user account, but who should exist on the remote machine 
        * Tries to connect as teh user account you are currently logged in with on the local machine 
        * Connecting with a different user: user@server 
        * ssh root@remoteserver
    * Exercise 5-3 Using SSH to log in to a remote server 
        * Assume that the remote server is available and reachable 
        * Can also use localhost to get the experience of working with ssh 
        1. Open a root shell on server2 
            * systemctl status sshd (should show you that the sshd process is currently up and running)
        1. ip a | grep 'inet ' (space between the closing quote in the grep)
            * Take note of the IP address of the server 
        1. Open a shell as a nonprivileged user on server1 
        1. on server one ssh into server two: ssh root@Server2_IPaddress 
        1. Should ask to authenticate the host yes to continue 
        1. Enter the root password for server2 
        1. w (command)
            * Should show the ssh session as another pseudo terminal session, but with the IP address in the from column
        1. exit (close the ssh connection)
    * NOTE: sometimes ssh connection might be slow 
        * using -v (can use multiples also) for verbose mode 
        * show all the individual componets that are contected 
        * Might help troubleshoot why its being slow 
    * After connecting to the server for the first time a public key fingerprint is stored in the file ~/.ssh/known_hosts
    * The next time you connect to the same server, this fingerprint is checked with the encryption key that was send over by the remote server to initialize contact 
    * If the fingerprint matches you will not see this message any more 
    * Some cases, the remote host key fingerprint does not match the key fingerprint that is stored locally 
        * this is potentially dangerious
        * But can also happen if you are connecting to an IP address that you have been connected to before but that is now in use by a different server
        * Or if the sshd service has been deleted or reinstalled 
    * You just have to remove the key fingerprint from the ~/.ssh/known_hosts file on the CLIENT computer 
    * for example removing with sed (sed -i -e '25d' ~/.ssh/known_hosts (removes line 25))
    * Using graphical applications in an SSH environement 
        * by default ssh sessions cannot start graphical applications 
        * Security related 
        * a remote host cannot display screens on your computer without specific permission to do so
        * There are two requirements for starting graphical applications through an SSH connection
            * An X server must be running on the client computer 
            * The X server is the software component that creates the graphical screens
            * The remote host must be allowed to display screens on the local computer 
        * ssh -Y (easiest way to allow the remote host to display graphical screens on your computer)
        * ssh -Y linda@server2 
    * Table 5-2 Common SSH options 
        * -v (verbose; shows details about what is happening while establishing the connection)
        * -Y (enables support for graphical applications)
        * -p <PORT> (Specify the port (default is 22))
    * As an admin, you can create a system wide config that allows you to use X forwarding which is starting graphical applications thru an SSH session
    * To do so open the configuration file /etc/ssh/ssh_config and make sure it includes the following lines 
        * FowardX11 yes 
        * X forwarding will be available by default next time you use the ssh command 
    * Securely transferring files between systems 
        * If a host is running the sshd service, that service can also be used to securely transfer files between systems 
        * scp (command if you want the file to be copied)
        * rsync (command synchronize the file)
        * sftp (command part of ssh solution that enables the use of FTP command line syntax to transfer files using sshd)
    * Using scp to securely copy files 
        * scp (similar to cp command but includes an option that enables it to work with remote hosts)
        * scp can also be used to copy files and subdirs to and from remote hosts 
        * scp /etc/hosts server2:/tmp (cp /etc/hosts file to the /tmp dir on server2)
        * scp root@server2:/etc/passwd ~ (connect to server2 as user root, copy the /etc/passwd file to your home dir)
        * -r (recursive to copy an entire subdir structure)
        * scp -r server2:/etc/ /tmp (copy recursively /etc/ on server two to /tmp locally)
        * scp can also use -P to specify non default port number 
    * Using sftp to securely transfer files 
        * sftp command provides an alternative to securely transfer files 
        * scp = cp 
        * sftp provides an FTP like interface 
        * When working with sftp, you open an FTP client session to the remote server 
        * Where the only requirement on the remote server is that it should be running the sshd process 
        * From the FTP client session, you use typical FTP client commands, like put or upload a file or get to download a file 
        * When working with sftp, the local dir is important, even if after opening the FTP session you only see the remote directory on the server 
        * When you are downloading a file using get command, the file will be stored in the current local dir 
        * When uploading a file using put the file will be searched for in the local dir
    * Using rsync to synchronize files 
        * srync command usees ssh to synchronize files between a remote dir and a local directory 
        * The advantage of synchronizing files is that only differences need to be considered 
        * For example if you are synchronizing a 100-MiB file in which only a few blocks have changed since the previous sync, only the changed block will be synchronized 
        * This approach is also known as delta sync 
    * Table 5-3 Common rsync option
        * -r (synchronizes the entire directory tree)
        * -l (copies symbolic links as symbolic links)
        * -p (preserves permissions)
        * -n (performs only a dry run, not actually synchronizing anything)
        * -a (uses archive mode, thus ensuring that entire subdir tress and all file properties will be synchronized)
        * -A (uses archive mode, and in addition synchronizes ACLs)
        * -X (synchronizes SELinux context as well)
    * Exercise 5-4 Using SFTP to manage files on a remote server
        1. sudo shell, add a line that matches the server2 IP address to the hostname server2 (what?)
        1. stfp student@server2 (this gives you access to an SFTP prompt that is open on server2)
        1. ls (you will see files in the current working dir on the remote server)
        1. pwd (shows you the current dir on the remote server)
        1. lpwd (shows you local current dir)
        1. lcd /tmp (changes the local current dir to /tmp)
        1. put /etc/hosts (will put/upload /etc/hosts file from server1 to the user student home dir on server2)
        1. exit (closes the SFTP session)
    * Configuring key based auth for ssh 
        * If ssh is used on the internet (public facing) might not be a good idea to allow password logins 
        * SSH is more secure when using private/public keys for auth
        * This authentication method is normally enabled by default because it is more secure than password based auth
        * Only if key based auth is not possible is password login used 
        * In order to enable key based login is to create a key pair (everything else is organized by default already)
        * User who wants to connect to a server generates a public/private key pair 
        * Private key kept private and will never be distributed 
        * Public key is stored in the home directory of the target user on the SSH server in the file .ssh/authorized_keys
        * When authenticating using key pairs, the user generates a hash derived from the private key 
        * This hash is ent to the server, and if on the server it proves to match the public key that is stored on the server, the user is authenticated 
    * Using passphrases or not? 
        * When creating a public/private key pair, you are prompted for a passphrase 
        * If you want max security, you should enter a passphrase 
        * You are prompted for that passphrase each time that you are using the private key to authenticate to a remote host 
        * THIS IS SECURE, BUT NOT VERY CONVENIENT 
        * To create a config that allows for maximal convenience, you can just press enter twice when generating the public/private key pair to confirm that you do not want to set a passphrase 
        * This is a typical config that is used for authentication between servers in a trusted environment where no outside access is possible anyways 
        * To create a key pair:
            * ssh-keygen 
        * ssh-copy-id 
            * command to copy the public key over to the target server 
    * Exercise 5-5 Connecting to a remote server with public/private keys 
        1. On server1, open a root shell 
        1. ssh-keygen (to generate the key pair)
        1. When asked for the filename in which to store (private) key, accept the default filename ~/.ssh/id_rsa
        1. When asked to enter a passphrase, press enter twice
        1. The private key now is written to the ~/.ssh/id_rsa file and the public key is written to ~/.ssh/id_rsa.pub file 
        1. ssh-copy-id server2 (copies the public key to server2, You are then asked for the password on the remote server one last time)
        1. After copying the public  key, verify that it can actually be used for authentication
            * ssh server2 (You should now authenticate without having to enter the password for the remote user account)
    * After you copy the public key to the remote host, it will be written to the ~/.ssh/authorized_keys file on that host 
    * Notice that if multiple users are using keys to log in with that specific account, the authorized_keys file may contain a lot of public keys 
    * Don't overwrite this file 
* Summary 
    * Learned the difference between consoles, terminals, and shells
    * set up terminal sessions locally as well as remotely 
    * SSH to connect to a remote server and how to securely copy files between servers 
    * Did not really talk about the ssh config file tho so some holes. 
* Exam preparation tasks 
* Review all key topics 
    * Definitions of the words console and terminal 
    * Situations that typically require a server reboot 
    * Common ssh options 
* Complete tables and lists from memory 
* define key terms 
    * Console 
    * Terminal 
    * subshell
    * reboot
    * systemd
    * key based login
    * publc key 
    * private key 
* Review questions 
* End of chapter labs 
    * lab 5.1 
    * lab 5.2 

## Chapter 6 User and group management 

* The following topics are covered in this chapter 
    * understanding different user types 
    * creating and managing user account 
    * creating and managing group accounts 
* The following RHCSA exam objectives are covered in this chapter 
    * Create, delete, and modify local user accounts 
    * change passwords and adjust password aging for local user accounts 
    * Create, delete, and modify local groups and group memberships 
    * configure superuser access 
* User and group management 
    * On a linux system, various processes are normally being used 
    * These process need access to specific resources on the linux system 
    * To determine how theese resources can be accessed, a distinction is made between processes that run in kernel mode and processes that run without full permission to the OS 
    * In the latter case user accounts are needed 
    * Not only to gran the required permissions to processes but also to make sure that people can do their work 
    * This chapter explains how to set up user and group accounts 
* Do I know this already Quiz 
    * UNderstanding different user types 
    * Creating and managing user accounts 
    * Creating and managing group accounts 
* Foundation topics 
* Understanding different user types 
    * create and manage user accounts 
    * Users on linux 
        * On linux there are two ways to look at system security 
        * There are privileged users and unprivileged users 
        * default privileged user is root 
        * This user account has full access to everything on a linux server and is allowed to work in system space without restrictions 
        * Root user account is meant to perform system admin tasks and should be used for that only 
        * For all other tasks an unpriviledged user account should be used 
        * On modern linux distros like RHEL 9, the root user account is often disabled 
        * Durning install you have a choice of what to do with the root user 
        * If you create a regular user and choose the option make this user admin, you don't have to set a root password and you will be able to use sudo to up privileges 
        * Sudo when administrator privileges are needed 
        * If you want to be able to login as root directly you can set a password for the root user 
        * id (command)
            * Get information about a user account 
            * see details about the current user 
            * can also use it on other user accounts to get details about those accounts 
            * id linda 
    * Working as root 
        * On linux systems by default there is the user root 
        * also known as the super user 
        * This account is used for managing linux and has no restrictions at all 
        * Root for instance can create other user accounts on the system 
        * Some task root privileges are required 
        * Some examples include 
            * installing software 
            * managing users
            * creating partitions on disk devices 
            * generally speaking all tasks that involve direct access to devices need root permissions 
        * Since root is so useful some people make a habit of logging in as root 
        * Not recommended especially not when logging into a graphical environment 
        * When you log in as root in a graphical environment all tasks that are executed run as root as well, involves an unnecessary security risk
    * Table 6-2 Methods to run tasks with elevated permissions 
        * su 
            * opens a subshell as a different user, with the advantage that commands are executed as root only in the subshell 
        * sudo 
            * allows authorized users to work with admin privileges 
        * PolicyKit 
            * enables you to set up graphical utilities to run with admin privileges 
    * Using su 
        * su (command to start a subshell in which you have another identity)
        * To perform admin tasks, for instances, you can log in with a normal user account and type su to open a root shell
        * The benefit is that root privileges are used only in the root shell 
        * You do need to enter the root password tho, which is best practice from a security prespective 
        * If you just type su, the username root is implied 
        * su can be used to run taks as another user as well 
        * su linda (open a subshell as the user linda)
        * when using su as an ordinary user, you are prompted for a password, and after entering that, you acquire the credentials of the target user 
        * The subshell that is started when using su is an env where you are able to work as the target user account
            * but env settings for that user account have not been set 
        * If you need complete access to the entire env of the user account you can use su - to start a login shell 
        * If you start a login shell all scripts that make up the user env are processed which makes you work in an env that is exactly the same as when logging in as that user 
        * NOTE: if you want to use su
            * su - is better than using su 
            * When the - is used, a login shell is started
            * without the -, some variables may not be set correctly 
            * So you are better off using su - immediately 
            * But don't forget that for running tasks with admin privileges you are better off using sudo 
    * Exercise 6-1 Switching User accounts 
        1. Log in to your system as a nonprivileged user and open a terminal 
        1. whoami (to see which user account you are currently using 
            * id (notice that you get more detail about your current credentials when using id)
        1. su - (enter the root password)
            * id (again to see you are currently are root)
        1. useradd bob (to create a user that you can use for testing purposes)
        1. From the root shell, user su - bob (confirm that you can log in without entering a password, bob does not have a password that is currently set)
        1. exit (exit from user bob shell. exit again from the root shell to return to the ordinary user shell)
    * sudo 
        * If a non root user needs to perform a specific system admin task, the user does not need root access 
        * Instead the system admin can config sudo to give user admin permissions to perform the specific tasks 
        * The user then carries out the task by starting the command with sudo (and entering the user's password when prompted)
        * so instead of using commands like useradd as teh root user, you can use sudo-enabled user account and type sudo useradd
        * This approach is definitely more secure because you will have admin permissions only while running specific command 
        * When creating a user during the installation process you can select grant admin permissions to that specific user 
        * If you select to do so, the user will be able to use all admin commands using sudo 
        * Also possible to set up sudo privileges after install
        * Making the user a member of the group wheel 
        * Two step procedure to add user to group wheel 
            1. Make the admin user account a member of the group wheel by using 
            * usermod -aG wheel user
            1. visudo (make sure the line %wheel ALL=(ALL) ALL is there)
        * This will give a user access to all admin commands
        * You can also use visudo to edit the /etc/sudoers config file and give user access to specific commands 
        * For example 
            * linda ALL=/usr/bin/useradd, /usr/bin/passwd 
            * Gives linda permission to run only commands useradd and passwd with admin privileges 
        * TIP: while using sudo you are prompted to enter a password 
            * Based on this a password token is generated, which allows you to run new sudo commands without entering the password again
            * Token is only valid for five minutes 
            * Use the following to extend the lifetime of the token in /etc/sudoers *using visudo*
            * extends to 240 minutes 
            * Defaults timestamp_timeout=240
            * If you want to set up users with specific sudo privileges, be careful with the passwd command 
            * If a user has sudo privileges on the passwd command, that would allow the user to change the password for root as well 
            * Can add an exeception
            * linda ALL=user/bin/useradd, /usr/bin/passwd, ! /usr/bin/passwd root 
            * This would allow user linda to change the password for all users, but not root
            * To assign sudo privileges to individual users or groups of users, you can change the contents of /etc/suderos using visudo 
            * A better practice is to create a drop-in file in the dir /etc/sudoers.d 
            * This drop in file would have the exact same contents as the modification you would make to /etc/sudoers
            * With the benefit that the custom config is separated from the standard config that was created while installing linux 
            * Files in /etc/sudoer.d are always included while using sudo 
        * TIP: Convenient to be able to use pipes in sudo commands 
            * By default this is not allowed
            * sudo sh -c (you can use any command containing a pipe as its arg)
            * example:
            * sudo sh -c "rpm -qa | grep ssh" (to get a list of all packages that have the string ssh in their name 
    * PolicyKit 
        * Most admin programs with GUI use policykit to authenticate as root user 
        * If a normal user that is not in the wheel group accesses such an application, that user will be propmoted for authentication
        * If a user who is a member of wheel opens a PolicyKit app, that user will have to enter their own password 
        * You do not need to know the details about Policy kit for RHCSA but it is good to know that you can use pkexec command 
        * pkexec command as an alt to sudo in case you ever completely lose sudo access to a system 
        * pkexec visudo (to repair the sudo config)
    * Exercise 6-2 Switching user accounts 
        1. Log into the system as student user and open a terminal 
        1. sudo -i (open a sudo root shell, enter the password for student user)
        1. useradd betty; useradd amy (to create two new users)
        1. echo password | passwd --stdin betty; echo password | passwd --stdin amy (to set the password for these two users)
            * exit to return to the user student shell
        1. su - betty (open a shell as user betty)
            * When prompted enter in the password you have just assigned for user betty 
        1. sudo ls /root (enter in the betty password and should notice an error message)
        1. exit (return to the shell in which you are student user)
            * whoami to verify the current user ID
        1. sudo sh -c 'echo "betty ALL=(ALL) ALL" > /etc/sudoers.d/betty' (to allow full sudo access for betty)
        1. su - betty (open a shell as betty again, and enter password of this user when prompted)
        1. sudo ls -l /root (to verify that sudo access is working)
            * The /root dir can only be viewed by the root user due to the permissions of that dir
        1. sudo sh -c 'echo "amy ALL=/usr/sbin/useradd, /usr/bin/passwd, !/usr/bin/passwd root" > /etc/sudoers.d/amy'
        1. su - amy (enter in amy's password when prompted)
        1. sudo passwd betty (to verify that you can change the password as user amy)
        1. sudo passwd root (to verify that you can NOT change the root password)
        1. exit x2 (to return to the student user shell)
            * whoami (to verify what user/shell you are in)
* Creating and managing user accounts 
    * System accounts and normal accounts 
        * A typical Linux env has two kinds of user accounts 
        * There are normal user accounts for people who need to work on a server and who need limited access to the resources on that server 
        * These user accounts typically have a password that is used for authenticating the user to the system 
        * There are also system accounts that are used by services the server is offering 
        * Both type of user accounts share common properties
        * Which are kept in the files /etc/passwd and /etc/shadow 
        * Example 6-2 show partial content of the /etc/passwd user config file 
    * NOTE: on many linux servers hardly any user accounts are used by people
        * Many linux servers are installed to run a specific service, and if people interact with that service they will auth with the service 
    * System accounts and normal accounts cont
        * Different fields are used in /etc/passwd to define a user account 
        * The fields are separated from each other by a colon 
        * The following is a summary of these fields followed by short description of their purpose 
    * Breaking down /etc/passwd fields 
        * Username
            * this is a unique name for the user 
            * Usernames are important to match a user to their password 
            * Password is stored seperately in /etc/shadow
            * There can be no spaces in the username
            * And in general it is a good idea to specify usernames in all lowercase letters 
        * Password 
            * In the old days, the second field of /etc/passwd was used to store the hashed password of the user 
            * Because /etc/passwd is readable by all users, this poses a security threat
            * Because of this on current Linux systems that hashed passwords are stored in /etc/shadow 
        * UID 
            * Each user has an unique ID (UID)
            * This is a numeric ID 
            * It is the UID that really determines what a user can do 
            * When permissions are set for a user, the UID (not the username) is stored in the file metadata 
            * UID 0 is reservered for root, the unrestricted user account
            * The lower UIDs (typically up to 999) are used for system accounts, 
            * Higher UIDs (from 1000 on by default) are reserved for people who need to connect a directory to the server 
            * The range of UIDs that are used to create regular user accounts is set in /etc/login.defs 
        * GID 
            * Each user is a member of at least one group 
            * This group is referred to as the primary group
            * This group plays a central role in permissions management 
            * Users can be a member of additional groups which are administered in the file /etc/group 
        * Comment field 
            * Comment field is used to add comments for user accounts 
            * IS OPTIONAL 
            * But it can be used to describe what a user account is created for 
            * Some ulilities, such as the obsolete finger utility can be used to get information from this field 
            * This field is also referred to as the GECOS field
            * General electric comprehensive operating system 
            * Had a specific purpose for IDing jobs in the early 1970s when GE was still an important manufacturer of servers 
        * Directory 
            * This is the initial dir where the user is placed after logging in
            * Also referred to as the home dir 
            * If the user account is used by a person, this is where the person would store personal files and programs 
            * For a system user account, this is the env where the service can store files it needs while operating 
        * Shell 
            * This is the program that is started after the user has successfully connected to a server 
            * For most users this will be /bin/bash (default linux shell)
            * For system user accounts, it will typically be a shell like /sbin/nologin
            * sbin/nologin command is a specific command that silently denies access to users 
            * To ensure that if by accident an intruder logs into the server the intruder cannot get any shell access 
            * Optionally, you can create an /etc/nologin.txt file
            * In which case only root will be able to log in but other users will see the contents of this file when their logins are denied 
        * A part of the user properties is stored in /etc/passwd
        * Another part of the config of user properties is stored in the /etc/shadow file 
        * The settings in this file are used to set properties of the password 
        * only the user root and processes running as root have access to /etc/shadow 
    * Example 6-3 Sample content from /etc/shadow 
        * page 172
    * Fields from the /etc/shadow file 
        * Login name 
            * Notice that /etc/shadow does not contain any UIDs (username only)
            * This opens up a possibility for multiple users using the same UID but different passwords (which is not recommended)
        * Encrypted Password 
            * This field contains all that is needed to store the password in a secure way 
            * If the field is empty, no password is set and the user cannot login
            * If the field starts with an exclamation mark, login for this account currently is disabled
        * Days since Jan. 1, 1970 that the password was last changed (epoch)
            * Many things on Linux refer to this date which on linux is considered the beginning of time 
        * Days before password may be changed 
            * This allow system admins to use a stricter password policy 
            * Where it is not possible to change back to the original password immediately after a password has been changed 
            * Typically this field is set to the value 0
        * Days after which password must be changed 
            * this field contains the maximal validity period of passwords 
            * In example 6-3 it is set to 99,999 (about 274 years), which is the default 
        * Days before password is to expire that user is warned 
            * this field is used to warn a user when a forced password change is upcoming 
            * Notice in the example it is set to 7 days, which is the default (even if password validity is set to 99,999 days)
        * Days after password expires that account is disabled 
            * Use this field to enforce a password change 
            * After password expiry, user can no longer log in
            * After the account has reached the max validity period, the account is locked out 
            * This field allows for a grace period in which the user can change their pasword but only during the login process 
            * This field is set in days and is unset by default 
        * Days since Jan. 1 1970, that acocunt is disabled 
            * An admin can set this specific field to disable an account on a specific date 
            * This is typically a better approach than removing an account
            * As all associated properties and files of the account are kept, but the account no longer can be used to auth on your server 
            * Note that this field does not have a default value 
        * A reserved field, which was once added "for future use"
            * This field was reserved a long time ago
            * It will probably never be used 
        * Most of the password properties can be managed with the passwd or chage commands 
    * Creating users 
        * There are many solutions for creating users on a linux server 
        * To start you can edit the contents of /etc/passwd and /etc/shadow config files directly 
        * using the vipw command (with the risk of making an error that could make logging in impossible to anyone)
        * useradd (another option which is the utility that you should use for creating users)
        * userdel (to remove users)
        * userdel -r (to remove a user and the complete user environment 
    * Modifying the configuration files 
        * Creating a user account by modifying the config files simply requires adding one line to /etc/passwd and another line to /etc/shadow
        * In which the user account and all of its properties are defined 
        * This method of creating users is not recommended tho
        * If you make an error you might mess up the consistency of the file and make logging in completely impossible to anyone 
        * Also might encounter locking problems if one admin is trying to modify the file contents directly while another admin wants to write a modification with some tool 
        * If you absolutely must modify the config file directly you should use vipw 
        * vipw will open an editor interface on your config files
        * More importantly it sets the appropriate locks on the config files to prevent corruption
        * It does not check syntax however 
        * so make sure that you know what you are doing, because making even one type might still severely mess up your server 
        * If you want to use this to modify /etc/shadow file use vipw -s 
        * vipw -s (/etc/shadow file)
        * vigr (edit the contents of /etc/group (where groups are defined))
    * NOTE: Nice to know that vipw and vigr exist 
        * But better not to use these utilities or anything else that opens the user and group config files directly
        * Using tools like useradd and groupmod is a better option
    * Using useradd
        * useradd is probably the most common tool on linux for adding users 
        * The ability to add a user account from the command line by using many of its parameters 
        * useradd -m -u 1201 -G sales,ops linda (create a user named linda)
        * Who is a member of the secondary groups sales and ops 
        * UID of 1201
        * Add a home directory to the user account as well 
    * Home directory 
        * All normal users will have a home dir
        * For people the home dir is the dir where personal files can be stored 
        * For system accounts the home dir often contains the working env for the service account 
        * As an admin you will not change home directory related settings for system accounts 
            * Because they are created automatically from the RPM post installation scripts when installing related software packages 
        * If you have people who need user accounts, you probably do want to manage home dirs content a bit 
        * When creating home dirs (which happens by default while you are creating users)
        * The content of the skeleton directory is copied to the user home dir 
        * /ect/skel (skeleton directory and its files are copied to the user home dir at the moment this dir is created)
        * These files will also get the appropriate permissions to ensure that the new user can use and access them
        * By default the skeleton dir contains mostly config files that determine how the user env is set up 
        * If in your env specific files need to be present in the home dir of all users
        * You can do this by adding the files to the skeleton dir (/etc/skel)
    * Default Shell 
        * Most regular users normally have a default shell 
        * This is the program that is started after successful authentication
        * For most users, this shell is set to /bin/bash 
        * System users should not have an interactive shell as the default shell
        * For most system users this shell is set to /sbin/nologin
        * To set or change the default shell using useradd or usermod there is the -s option
        * usermod/useradd -s (change the default shell)
        * useradd caroline -s /sbin/nologin (to make sure this user will not be able/allowed to log in)
    * Managing User properties 
        * For changing user properties the same rules apply as for creating user accounts 
        * command line tool or work directly in the config file using vipw 
        * usermod (command for modifying  user properties)
        * Can be used to set all properties of users as stored in /etc/passwd and /etc/shadow
        * plus additional tasks, such as managing group membership 
        * There is just one task it does not do well: SETTING PASSWORDS
        * usermod has an option -p
        * It tells you to use encrypted password for the new password however expects you to do the password encryption before adding the user account 
        * If wanting to change the password should use passwd 
    * Configuration files for user management defaults 
        * When working with tools such as useradd, some default values are assumed 
        * These default values are set in two config files: /etc/login.defs and /etc/default/useradd
    * Example 6-4 useradd defaults in /etc/default/useradd
        * page 175
    Config files for user management defaults cont
        * /etc/default/useradd (defines default values that are applied when using useradd)
        * In the file /etc/login.defs (different login related variables are set)
        * This file is used by different commands and it relates to setting up appropriate env for new users 
    * Some of the most significant properties that can be set from /etc/login.defs 
        * MOTD_FILE:
            * Defines the file that is used as the message of the day file 
            * In this file you can include messages to be displayed after the user has successfully logged into the server 
        * ENV_PATH 
            * Defines the $PATH variable
            * A list of dirs that should be searched for executable files after logging in
        * PASS_MAX_DAYS, PASS_MIN_DAYS, and PASS_WARN_AGE:
            * Define the default password expiration properties when creating new users 
        * UID_MIN:
            * Indicates the first UID to use when creating new users 
        * CREATE_HOME:
            * Indicates whether or not to create a home dir for new users 
    * Managing password properties 
        * Two commands to change the password properties for user (that live in /etc/shadow): chage and passwd 
        * passwd -n 30 -w 3 -x 90 linda (sets the password for linda user to a minimal usage period of 30
            * an exiry after 90 days 
            * where a warning is generated 3 days before expiry 
        * many of the tasks that can be accomplished with passwd can be done with chage also 
        * chage -E 2025-12-31 bob (have the account for user bob expire on Dec 31 2025)
        * chage -l (see current password management settings)
        * chage also has a interactive mode 
        * chage anna (the command will prompt for all the password properties you want to set interactively 
        * Example 6-5 showing password expiry information with chage -l 
            * page 176
    * Creating a user environment 
        * When a user logs in, an environment is created 
        * The env consists of some variables that determine how the user is working 
        * such as $PATH (which defines a list of dirs that should be searched when a user types a command)
        * To construct the user env a few files play a role 
            * /etc/profile (Used for default settings for all users when starting a login shell)
            * /etc/bashrc (Used to define defaults for all users when starting a subshell)
            * ~/.profile (specific settings for one user applied when starting a login shell)
            * ~/.bashrc (specific settings for one user applied when starting a subshell)
        * When you log in the files are read in this order 
        * Variables and other settings that are defined in these files are applied 
        * If a variable or setting occurs in more than one file, the last one wins 
    * Exercise 6-3 Creating user accounts 
        1. From a sudo shell vim /etc/login.defs (open the config file /etc/login.defs)
            * PASS_MAX_DAYS to the value 99 before you start creating users 
            * Look for the parameter CREATE_HOME and make sure it is set to yes 
        1. cd /etc/skel (mkdir fotos and mkdir files (to add two default directories to all user home dirs))
            * Also change the contents of the file .bashrc to include the line export EDITOR=/usr/bin/vim
            * This sets the default editor for tools that need to modify text files 
        1. useradd linda (to create an account for the user linda)
            * id linda (verify that linda is a member of a group with the name linda and nothing else)
            * Also verify that the dir Pictures and Documents have been created in user linda's home dir 
        1. passwd linda (to set a password for the user you have just created)
            * use the password password 
        1. passwd -n 30 -w 3 -x 90 linda (to change the password properties)
            * password expire after 90 days (-x 90)
            * three days before expiry the user will get a warning (-w 3)
            * Password has to be used for at least 30 days before it can be changed (-n 30)
        1. Create a few more users: lucy, lori, and bob
            * for i in lucy bob lori; do adduser $i;done
            * You may get an error message stating the user already exist, this message can be safely ignored 
        1. grep lori /etc/passwd /etc/shadow /etc/group 
            * This shows the user lori created in all three critical files and confirms they have been set up correctly 
* Creating and managing group accounts 
    * Every linux user has to be a member of at least one group 
    * Understanding Linux groups 
        * Linux users can be a member of two different kinds of groups 
        * First there is the primary group 
            * Every user must be a member of the primary group, and a user has only one primary group 
        * When a user creates a file, the user's primary group becomes the group owner of the file 
        * Users can also access all files their primary group has access to 
        * The user's primary group membership is defined in /etc/passwd
        * The group itself is stored in the /etc/group config file 
        * Besides the mandatory primary group, users can be a member of one or more secondary groups as well 
        * A user can be a member of a secondary group in addition to the primary group 
        * Secondary groups are important to get access to files
        * If the group a user is a member of has access to specific files, the user will get access to those files also
        * Working with secondary groups is important
            * In particular in env where linux is used as a file server to allow people working for different departments to share files with one another 
        * You have also seen how secondary group membership can be used to enable user admin privileges through sudo 
        * By making the user a member of the group wheel 
    * Creating groups 
        * There are different options for creating groups 
        * The group config files can be modified directly using vigr
        * Or the command line utility groupadd 
    * Creating groups with vigr 
        * vigr (command: you open an editor interface directly on the /etc/group config file)
    * Fields are used in /etc/group 
        * Group name: contains the name of the group 
        * Group password: field contains a group password (a feature that is hardly used anymore)
            * A group password can be used by users who want to join the group on a temporary basis 
            * So that access to files the group has access to is allowed
            * If a group password is used
            * It is stored in /etc/gshadow file (file is only accessible by root)
        * Group ID: This field contains a uniq numeric group ID number 
        * Members: Here you find the names of users who are a member of this group as a secondary group
            * Note that this field does not show users who are a member of this group as their primary group 
    * Creating groups with vigr cont 
        * In addition to /etc/group, there is the /etc/gshadow file 
        * This file is not commonly used to store group passwords (because hardly anyone still uses them)
        * But it does have a cool feature 
        * In the third field of this file you can list admins 
        * This is a comma separated list of users that can change password for group members (which are listed in the fourth field of this file)
        * Note that specifying group members here is optional, but if it is done, the group member names must be the same as the group members in /etc/group 
    * Using groupadd to create groups 
        * Another method to create new groups is by using the groupadd command 
        * groupadd (followed by the name of the group you want to add)
        * There are some advanced options
        * The only signigicant one is -g (which allows you to specify a group ID when creating the group)
    * Managing group properties 
        * groupmod (manage group properties)
        * Can use this command to change the name or group ID of the group 
        * It does not allow you to add group members 
        * Notice that is may be a bad idea to change either of these properties
        * As it can affect group owned files that already exist 
        * TO do this you use usermod 
        * usermod -aG (will add users to new groups that will be used as their secondary group)
        * Because a group does not have many properties 
            * Common that group properties are managed directly in /etc/group file by using the vigr command 
        * lid (to see which users are a member of a group)
        * lid -g sales (to check which users are a member of the group sales)
    * TIP: Because user's group membership are defined in two different locations it can be difficult to find out which groups a user is a member of 
        * groupmems (a way to check this)
        * groupmems -g sales -l (to see which users are a member of the groups sales
        * Shows users who are a member of this group as a secondary group assignment 
        * But also users who are a member of this group as the primary group assignment 
    * Exercise 6-4 Working with groups 
        1. open a sudo shell and type groupadd sales
            * groupadd account (to add groups with names sales and account)
        1. usermod (to add user linda and laura to the group sales 
            * add lori and bob to the sales group account 
            * usermod -aG sales usern_name 
        1. id linda (to verify that user linda has correctly been added to the group sales 
            * The results should show linda is assigned to a group with the name linda 
            * This is lindas primary group
            * Indicated with the gid option
            * groups parameter shows all groups user linda currently is a member of 
            * which indlues the primary group as well as the secondary group sales that the user has been assigned too 
* Summary 
    * Learned how to create and manage users and groups 
    * Which config files are used to store users and groups
    * and which properties are used in these files 
    * Also learned which utilities are available to manage user and group accounts 
* Exam prep tasks 
* Review all key topics 
    * Users on Linux 
    * Methods to run tasks with elevated permissions 
    * Description of user account fields in /etc/passwd 
    * description of password property fields in /etc/shadow 
    * significant properties that can be set from /etc/login.def 
    * files that play a role in constructing the user env 
* Define key terms 
    * User
    * Privileged user
    * Unpriviledged user
    * root
    * password 
    * GECOS
    * Group
    * Primary group 
    * secondary group 
* Review questions 
* End of chapter labs 
* Lab 6.1 
* Lab 6.2 

## Chapter 7 Permission management 

* The following topics are covered in this chapter 
    * Managing file ownership 
    * managing basic permissions 
    * managing advanced permissions 
    * Setting default permissions with umask 
    * working with user extended attributes 
* The following RHCSA exam objectives are covered in this chapter 
    * Manage default permissions 
    * List, set, and change standard ugo/rwx permissions 
    * Create and configure set-GID directories for collaboration
    * Diagnose and correct file permission problems 
* Permission Management 
    * To get access to files on linux you use permissions 
    * These permissions are assigned to three entities 
        * The file owner, 
        * The group owner
        * The other entity (everybody else)
* Do I know this already quiz 
* Foundation topics section
    * Managing file ownership
    * managing basic permissions 
    * managing advanced permissions 
    * setting default permissions with umask 
    * Working with user extended attributes 
* Foundation topics 
* Managing file ownership
    * Before we discuss permissions you need to understand the role of file and directory ownership
    * File and dir ownership are vital for working with permissions 
    * Displaying ownership 
        * Every file and dir has two owners 
        * A user owner and a group owner
        * Also the other entity (which also is considered to be an entity to determine the permissions a user has)
        * ls -l (shows the user, group, and other listing (ugo))
        * Owners are set when a file or dir is created 
        * On creation the user who creates teh files becomes the user owner
        * And the primary group of that user becomes the group owner
        * To determine whether you as a user have permission to a file or dir 
        * The shell checks ownership 
        * This happens in the following order
            1. The shell checks whether you are the user owner of the file you want to access 
            * Which is also referred to as the user of the file 
            * If you are the user you get the permissions that are set for the user and the shell looks no further 
            1. If you are not the user owner, the shell checks whether you are a member of the group owner
            * Which is also referred to as the group of the file 
            * If you are a member of the group you get access to the file with the permissions of the group 
            * The shell looks no further 
            1. If you are neither the user owner nor the group owner 
            * And have not obtained permissions through access controls lists (ACLs)
            * You get the permissions of the other entity 
        * ls -l (to see current ownership assignments)
        * This command shows the user owner and the group owner 
    * Example 7-1 Displaying current file ownership
        * page 190
    * Displaying ownership cont
        * ls (can display ownership for files in a given dir)
        * find -user (can get a list of all files on the system that have a given user or group as owner)
        * find / -user linda (shows all files that have user linda as their owner)
        * find / -group users (searches all files that are owned by group user (the user group))
    * Changing user ownership
        * To apply appropriate permissions, first thing to consider is ownership
        * chown (command)
        * chown who what
        * chown linda files (changes the ownership of the file files to user linda)
        * chown -R (set ownership recursively)
        * -R (allows you to set ownership of the current dir and everything below)
        * chown -R linda /files (changes ownership for the dir /files and everything beneath it to user linda)
    * Changing group ownership 
        * There are actually two ways to change group ownership
        * chown
        * chgrp 
        * chown use a . or : in front of the group name 
        * chown .account /home/account (changes the group owner of dir /home/account to the group account)
        * Chown can be used to change user and/or group ownership in a number of ways 
            * chown lisa myfile (set user lisa as the owner of myfile)
            * chown lisa.sales myfile (set user lisa as user owner and group sales as group owner of myfile)
            * chown lisa:sales myfile (sets user lisa as user owner and group sales as group owner of my file)
            * chown .sales myfile (sets group sales as group owner of myfile without changing the user owner)
            * chown :sales myfile (sets group sales as group owner of myfile without changing the user owner)
        * Can also use the chgrp command to change group ownership
        * chgrp account /home/account (set group ownership for the dir /home/account to the group account)
    * Understanding default ownership 
        * When a user creates a file, default ownership is applied 
        * The user who creates the file automatically becomes user owner
        * And the primary group of that user automatically becomes group owner 
        * Normally this is the group that is set in /etc/passwd file as the user's primary group 
        * If a user if a member of more groups however 
        * The user can use newgrp command to change the effective primary groups so that new files will get the new primary group as group owner 
        * group (command to show the current primary group)
        * Of the groups listed the primary group os the first name after the : character 
        * groups lisa 
        * newgrp will open a new shell in which the new temporary primary group is set 
        * This group will continue to be used as the effective primary group until you use the exit command 
        * Example 7-2 Using newgrp to change the effective primary group (page 192)
        * After you change the effective primary group all new files that the user creates will get this group as their group owner 
        * To return to the original primary group setting, use exit 
        * To be able to use the newgrp command, a user has to be a member of that group 
        * A group password can be set for the group using gpasswd command (but this is uncommonly used)
        * If a user uses the newgrp command but is not a member of the target group the shell prompts for the group password 
        * After the user enters the correct group password the new effective primary group is set 
* Managing basic permissions 
    * Understanding Read, write, and execute permissions 
        * The three basic permissions allow users to read, write and execute files 
        * The effects differ when applied to files or dirs 
        * read (for files gives the right to open the file for viewing)
            * Can read the contents, but also means your comp can open the file to do something with it 
            * A program file that needs access to a library needs, for example read access to that library 
            * Most basic permissions you need to work with files 
        * read (dirs allows you to list the contents of that dir)
            * Does not extend to reading files in the dir 
            * This permission does not allow you to read files in the dir as well 
            * Linux permission system does not know inheritance
            * Only way to read a file is by using the read permission for the file
            * to open a file for reading, however, it is required to have read as well as execute permissions to the dir because you would not see the file otherwise
        * Write (file/dir allows you to modify the contents of the file)
            * allows you to modify the contents of existing files
            * Does not allow you to create or delete new files 
            * You need write permission on the dir where you want to create the file to do this
            * To modify permissions on a file, you have to be the owner (or root)
            * On dirs this permission also allows you to create and remove new subdirs 
        * Execute (what you need to run a program)
            * Also need execute permission on a dir if you want to do anything in that dir 
            * The execute permission will never be set by default (which makes linux almost immune to viruses)
            * Only the user owner and the root user can apply execute permissions 
        * Having the execute permission on files means you are allowed to run a program
        * If applied to a dir it means that you are allowed to use cd command to enter that dir
        * Execute is an important permission for dirs 
        * Normally applied as the default permission to dirs 
        * Without it there is no way to change to that dir 
    * Table 7-2 Use of read, write, and execute permissions 
        * Read
            * applied to files (view file content)
            * applied to dirs (list contents of dir)
        * Write 
            * Applied to files (change contents of a file)
            * Applied to dirs (create and delete files and subdirs)
        * Execute 
            * Applied to files (run a program)
            * Applied to dirs (change to the dir)
    * Applying read, write, and execute permissions 
        * chmod (command to apply permissions)
        * When using chmod you can set permissions for user, group, and other
        * Can be used in two modes 
            * relative mode and absolute mode 
        * Absolute mode three digits are used to set permissions 
        * Three digits apply to user, group, and other respectively 
        * Read = 4 
        * Write = 2 
        * Execute = 1 
        * When setting permissions, calculate the value that you need 
        * chmod 755 /somefile (rwx for user, rx for group, rx for others on /somefile)
        * When you use chmod in this way, all current permissions are replaced by permissions you set 
        * If you want to modify permissions relative to the current permissions, you can use chmod in relative mode 
        * When using chmod in relative mode you work with three indicators to specify what you want to do 
            * First you specify for whom you want to change permissions 
            * To do this you can choose between user (u), group (g), others (o), and all (a)
            * Then you can use operator to add or remove permissions from the current mode, or set them in a absolute way 
            * At the end you use r, w, and x to specify what permissions you want to set 
        * When changing permission is relative mode, you may omit the to whom part to add or remove a permission for all entities 
        * For instance, the following adds the execute permission for all users 
            * chmod +x somefile
        * When working in relative mode, you may use more complex commands as well 
        * chmod g+w,o+r somefile (adds write permissions to the group and removes read for others)
        * When applied in recursive mode, the execute permission needs special attention
        * Example 
            1. Open a root shell and type mkdir ~/files 
            1. Use cp /etc/[a-e]* ~/files (ignore the errors and warning that you see)
            1. ls -l ~/files/* (observe the permissions that are set on the files)
            1. chmod -R a+x ~/files 
            1. ls -l ~/files/* again (should notice that all files have become executable as well)
        * Files becoming executable in an uncontrolled way are a major security issue 
        * If you want to apply the execute permission in a recursive way you should apply it as X, not x 
        * chmod -R a+x files (instead use chmod -R a+X files) 
        * This ensures that subdirs will obtain the execute permission but the execute permission is not applied to any files 
    * Exercise 7-1 Managing Basic Permissions 
        1. From a root shell (mkdir -p /data/sales /data/account)
        1. Before setting the permissions, change the owners of these dirs using (chown linda.sales /data/sales)
            * chown linda.account /data/account 
        1. Set the permissions to enable the user and group owners to write giles to these dirs and deny all access for all others 
            * chmod 770 /data/sales 
            * chmod 770 /data/account 
        1. su - laura (become user laura and change into the dir /data/ account)
            * touch emptyfile (create a file in the dir)
            * Does this work?
            * groups to figure out why?
        1. Still as laura (cd /data/sales)
            * touch emptyfile (create a file in this dir)
            * Does this work (groups to figure out why)
* Managing Advanced Permissions 
    * Set of advanced permissions 
    * These are not permissions that would be set by default 
    * But sometimes provide useful addition to realize more advanced scenarios 
    * Understanding advanced permissions 
        * Three advanced permissions 
        * set uid ID (SUID)
            * Some very specific occasions, you may want to apply this permission to executable files 
            * By default a user who runs an executable file runs this file with their own permissions 
            * For normal users that usually means that the use of the program is restricted 
            * In some cases however the user needs special permissions just for the execution of certain task 
        * On /usr/bin/passwd this permission is set by default 
        * Meaning when a user changes their password, the user temporarily has root permissions because /usr/bin/passwd utility is owned by the root user 
        * Allows the user to write to the /etc/shadow file 
        * ls -l (see the SUID permission as an s at the position where normally you would expect to see the x for the user permissions)
        * Lowercase s means that both SUID and execute are set
        * Uppercase S would mean that only the SUID is set 
        * Potentially dangerous 
        * You may gives away root permissions by accident if applied wrongly 
        * Use with great care 
        * Don't apply it to any files at all (it is set on some OS files and should stay)
        * set group ID (SGID)
            * Has two effects 
            * if applied on an executable file, it gives the user who executes the file the permissions of the group owner of that file 
            * Can accomplish more or less the same thing that SUID does 
            * Hardly used 
            * Applied to some system files as a default setting 
        * When applied to a dir SGID can be useful 
            * Can use it to set default group ownership on files and subdirs created in that dir 
            * By default when a user creates a file, user's effective primary group is set as the group owner of that file 
            * Not useful because primary group is usually a group with the same name as the user 
            * And which the user is the only member
            * So by default files that a user creates will be group shared with nobody else
        * If you create a shared group dir and make sure that the SGID permission is applied to that dir, and the group account is set as the group owner of that dir
        * All files created in that dir and all its subdir also get the group as the default group owner 
        * SGID is a very useful permission to set on shared group dirs 
        * SGID shows as an s at the position where you normally find the group execute permission 
        * Lowercase s indicates both SGID and execute are set 
        * Uppercase S means only SGID is set 
        * Sticky bit 
            * This permission is useful to protect files against accidential deletion in an env where multiple users have write permissions in the same dir 
            * If sticky bit is applied a user may delete a file only if they are the user owner of the file or of the dir that contains the file 
            * Applied as default permission to the /tmp dir 
            * Can be useful on shared group dirs as well 
        * Without the sticky bit, it a user can create files in a dir, the user can also delete files from that dir 
        * May be annoying in a shared group env
        * When you apply sticky bit, a user can delete files only if one of the following is true 
            * The user has root access 
            * The user is owner of the file 
            * The user is owner of the dir where the file exists 
        * Sticky bit shows as T at the position where you normally see the execute permission for others 
        * Lowercase t indicates that sticky bit as well as execute permission for the others entity are set 
        * Uppercase T indicates that only sticky bit is set 
        * NOTE: Make sure you know how to manage these advanced permissions 
            * The RHCSA objectives specifically mention that you need to be able to use SGID to create a shared group dir 
    * Applying advanced permissions 
        * chmod (to apply SUID, SGID, and sticky bit)
        * SUID has a numeric value 4
        * SGID has a numeric value 2
        * Sticky bit has a numeric value 1 
        * Need to add a four digit arg to chmod 
        * Which the first digit refers to the special permissions
        * chmod 2755 /somedir (add SGID permission to a dir and set rwx for user, rx for group and other) 
        * Impractical if you have to look up the current permissions that are set before working with chmod in absolute mode 
        * Risk overwriting permissions if you do not
        * Recommend working in relative mode if you need to apply any of the special permissions 
        * chmod u+s (for SUID)
        * chmod g+s (for SGID)
        * chmod +t (for sticky bit)
            * Followed by the name of teh file or the dir that you want to set the permissions on 
    * Table 7-4 Working with SUID, SGID, and Sticky Bit
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
    * Applying advanced permissions cont
    * Exercise 7-2 Working with special permissions 
        1. Open a root shell
        1. su - linda (open a terminal in which you are user linda)
        1. cd /data/sales (go to the sales dir)
            * touch linda1 and touch linda2 (create two files of which linda is the owner)
        1. exit (back to the root shell)
            * su - laura (switch the current user identity to user laura, who is also a member of the group sales)
        1. cd /data/sales (ls -l)
            * See the two files that were created by user linda that are group owned by the group linda
            * rm -f linda* (remove the two linda files)
        1. touch laura1 laura2 (create two files that are owned by user laura)
        1. su - (escalate your current permissions to root level)
        1. chmod g+s,o+t /data/sales (set group ID bit as well as sticky bit on shared group dirs)
        1. su - linda (cd /data/sales)
            * touch linda3 linda4
            * You should see that the two files you have created are owned by the group sales, which is group owner of the dir /data/sales 
        1. rm -rd laura*
            * Normally sticky bit prevents you from doing so, 
            * But bc user linda is the owner of the dir that contains the files you are allowed to do it anyways 
* Setting default permissions with umask 
    * To setdefault permissions, you use either file ACLs or umask 
    * Do not need to know about ACLs for RHCSA 9 exam
    * Default permissions for new files 
    * These permissions are determined by umask setting 
    * This shell setting is applied to all users when logging in to the system
    * In the umask setting, a numeric value is used that is subtracted from the maximum permissions that can be set automatically to a file
    * The max setting for files is 666, and for dirs is 777
    * Of the digits used in the umask, like chmod, 
    * first digit is the user permissions 
    * second digit refers to the group permissions
    * Last refers to default permissions set for others 
    * deault umask setting of 022 gives 644 to all new files and 755 for all new dirs 
    * Table 7-5 umask values and their results 
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
    * Setting default permissions with umask cont 
    * Easy way to see how umask settings work is as followed:
        * start with the default permissions for a file set to 666 and subtract the umask to get the effective permissions
        * For a dir start with its default permissions that are set to 777 and subtract the umask to get the effective permissions 
    * There are two ways to change the umask settings: for all users and for individual users 
    * If you want to set the umask for all users
    * Must make sure the umask setting is considered when starting the shell env files as directed by /etc/profile 
    * The right approach is to create a shell script with the name umask.sh in the /etc/profile.d dir and specify the umask you want to use in that shell script
    * If the umask is changed in this file it applies to all users after logging in to your server 
    * An alt to setting the umask through /etc/profile and realted files where it is applied to all users logging in to the system is to change the umask settings in a file with the name .profile 
        * which is created in the home dir of an individual user 
        * Settings applied in this file are applied for hte individual user only
        * Nice method if you need more granularity
        * Like this feature to change the default umask for root to 027
        * Whereas normal users work with the default umask of 022 
* Wokring with user extended attributes 
    * A relationship always exists between a user or group object and the permissions these user or group objects have on a file or dir 
    * An alt method of securing files on a Linux server is by working with attributes 
    * Attributes do their work regardless of the user who accesses the file 
    * Many attributes are documented 
    * Some attributes are available but not yet implemented 
    * Most useful attributes that you can apply 
        * A 
            * This attribute ensures that the file access time of the file is not modified 
            * Normally every time a file is opened the file access time must be written to the files metadata 
            * This affects performance in a negative way 
            * Therefore on files that are accessed on a regular basis
            * A attribute can be used to disable this feature 
        * a 
            * This attribute allows a file to be added to but not to be removed 
        * c 
            * If you are using a file system where volume level compression is supported 
            * This file attribute makes sure that the file is compressed the first time the compression engine becomes active 
        * D
            * This attribute makes sure that changes to files are written to disk immediately and not to cache first 
            * This is a useful attribute on important database files to make sure that they do not get lost between file cache and hard disk 
        * d 
            * This attribute makes sure the file is not backed up where the legacy dump utility is used 
        * I 
            * This attribute enables indexing for the dir where it is enabled 
        * i 
            * This attribute makes the file immutable 
            * Therefore no changes can be made to the file at all
            * Which is useful for files that need a bit of extra protection
        * s 
            * This attribute overwrites the blocks where the file was stored with 0s after the file has been deleted
            * This makes sure recovery of the file is not possible after it has been deleted 
        * u 
            * This attribute saves undeleted information
            * This allows a utility to be developed that works with that information to salvage deleted files 
    * NOTE Altho there are quite a few attribute that can be used 
        * Be aware that most attributes are rather experimental
        * Are only of any use if an application is used that can work with the given attribute 
        * Example: does not make sense to apply u attribute if no application has been developed that can use this attribute to recver deleted files 
    * Working with user extended attributes cont 
    * chattr (command to apply attributes)
    * chattr +s somefile (to apply the attributes to somefile)
    * chattr -s somefile (remove the attribute)
    * Should try this to find out how attributes are one of the rare cases where you can even block access to the root user
    * Example 
        1. Open a root shell 
        1. touch /root/myfile (create a new file)
        1. chattr +i /root/myfile (set immutable permission)
        1. rm -f /root/myfile (try to remove the file but can't)
        1. chattr -i /root/myfile (remove the attribute again)
    * lsattr (overview of all attributes that are currently applied)
* Summary 
    * work with permissions 
    * basic permissions as well as advanced permissions 
    * umask 
    * user extended attributes (to apply an additional level of file system security)
* Exam prep tasks 
* Review all key topics 
    * Read, Write, and Execute permissions 
    * Numeric Representation of permissions 
    * Working with SUID, GUID, and Sticky bit 
    * umask values and their results 
* Complete tables and lists from memory 
* Define key terms 
    * ownership
    * permissions
    * inheritance
    * attribute 
* Review questions 
* End of chapter lab 
* Lab 7.1

## Chapter 8 Configuring Networking 

* The following topics are covered in this chapter 
    * Networking fundamentals 
    * managing network address and interfaces 
    * validating network config 
    * managing network config with nmtui and nmcli
    * setting up hostname and name resolution
* The following RHCSA exam objectives are covered in this chapter 
    * Config IPv4 and IPv6 addresses 
    * Config hostname resolution
* Configuring networking 
* RHEL 9 networking is managed by NetworkManager service 
* Old network service do not exist anymore 
* That means that modern NetworkManager-releated tools like nmcli nmtui are the only way to manage network settings 
* Do I know this already quiz 
    * Foundation topics section
    * Networking fundamentals 
    * managing network addresses and interfaces 
    * Validating network configuration
    * Managing network configuration with nmtui and nmcli 
    * Setting up hostname and name resolution
* Foundation topics 
* Networking fundamentals 
    * To set up networking on a server, your server needs a unique address on the network 
    * IP (internet protocol) address are used 
    * Two versions of IP addresses are relevant 
    * IPv4 addresses (32 bit addresses and have 4 octets separated by dots)
    * IPv6 (128 bit addresses and are written in eight groups of hexacimal numbers that are 16 bits each separated by colons)
    * IP addresses 
        * Node (also might encounter the word host)
        * A host (or refered to as node in the text) is typically a server providing services on the network 
        * To make it easier for comps to communicate with one another every IP address belongs to a specific network
        * To communicate with computers on another network a router is used 
        * A router is a machine that connects networks to one another
        * To communicate on the Internet, every comp needs a worldwide uniq IP address 
        * Private network addresses 
        * Private network addresses are addresses that are for use in internal networks only 
        * Some specific IP network addresses have been reserved for this purpose 
            * 10.0.0.0/8 (a single Class A network)
            * 172.16.0.0/12 (16 Class B networks)
            * 192.168.0.0/16 (256 Class C networks)
        * When private addresses are used, the nodes that are using them cannot access the internet directly 
        * Nodes from the internet cannot easily access them 
        * NAT (Network Address Translation) commonly used on the router that connects the private network to the internet
        * In NAT, the nodes use a private IP address 
        * But when accessing the internet, this private IP is replaced with the IP address of the NAT router 
        * Nodes on the Internet think that they are communicating with the NAT router, and not with the individual hosts 
        * The NAT router in turn uses tables to keep track of all connections that currently exist for the hosts in the network 
        * Based on this table, NAT router helps make it possible for computers with a private IP address to connect to hosts on the Internet
        * NAT is very common
    * IPv6 Addresses 
        * To make IPv6 addresses more readable, you can replace one range of zeros with ::
        * IPv6 addresses that start with leading zeros can be omitted 
        * 02fb:0000:0000:0000:90ff:fe23:8998:1234
        * 2fb::90ff:fe23:8998:1234
    * IPv4 Network Masks 
        * To know which network a computer belongs a subnet mask is used with every IP address 
        * Subnet mask defines which part of the network address indicates the network and which part indicates the node 
        * Subnet masks may be written in the Classless Inter-Domain Routing (CIDR) notion
        * Indicates the number of bits in the subnet mask 
        * Or classical notation 
        * They always need to be specified with the network address 
        * 192.168.10.100/24(CIDR notation)
            * Indicates that a 24 bit network address is used
        * 192.168.10.100/255.255.255.0 (classical notation)
            * exact same thin
        * Often network masks use multiple bytes
        * 192.168.10.100/24
            * The first 3 bytes (192.168.10) are the network part
            * Last byte (100) is the host part of that network 
        * When talking about network addresses, you use a 4 byte number, as well, in which the node address is set to 0
        * For 192.168.10.100/24 (the network address is 192.168.10.0)
        * There is also always a broadcast address
        * This is the address that can be used to address all nodes in the network 
        * In the broadcast address all node bits are set to 1 
            * Which makes for the decimal number 255 if an entire byte is refered to
            * 192.168.10.100/24 (Broadcast address is 192.168.10.255)
    * Binary Notation
        * BC IPv4 address space is limited, modern IPv4 network variable length network masks are used 
        * These are network masks such as 212.209.113.33/27
        * In a variable length subnet mask only a part of the byte is used for addressing nodes
        * Another part is used for addressing the network 
        * IN the subnet mask /27, the first 3 bits of the last byte are used to address the network 
        * And the last 5 bits are used for addressing nodes 
        * Easier to understand when written out in binary notation
        * 212.209.113.33 = 11010100.11010001.00001010.00100001
        * Subnet mask /27 = 11111111.11111111.11111111.11100000
        * Table 8-2 Binary decimal conversion overiew (page 213)
        * 219.209.113.33/27
        * With a /27 30 nodes can be addressed per network
        * 32 IPs, 2 of them are the network address and broadcast address (which leaves 30 for the host addresses)
        * NOTE: DO NOT NEED TO MAKE THESE CALCULATIONS FOR THE EXAM BUT HELPFUL TO KNOW
    * MAC addresses 
        * IP addresses are the addresses that allow nodes to communicate to any other node on the internet 
        * Not the only addresses in use tho
        * Each network card also has a 12 byte MAC address
        * MAC addresses are for use on the local network 
        * The local physical network or local WLAN, just up to the first router that is encountered
        * Cannot be used for communication between nodes that are on different networks 
        * MAC addresses are important tho, because they help computers to find the specific network card that an IP address belongs to
        * 00:0c:29:7d:9b:17 (example mac address)
        * First 6 bytes are the vendor ID 
        * Second 6 bytes are the unique node ID 
        * Vendor IDs are registered
        * By using registered vendor IDs, it is possible to allocate unique MAC addresses 
    * Protocol and Ports 
        * IP addresses to identify individual nodes 
        * On these nodes you will typically be running services 
        * Like a web server or FTP server 
        * To ID these services port addresses are used 
        * Every service has a specific port address
        * Such as port 80 for HTTP
        * prot 22 for ssh
        * In network communication the sender and receiver are using port addresses 
        * Destination port address as well as a source port address involved in network communications 
        * Because not all services are addressed in a similar way 
        * A specific protocol is used between the IP address and the port address
        * Such as TCP or UDP (or ICMP)
        * Every protocol has specific properties
        * TCP is typically used when the network communication must be reliable and delivery must be guaranteed
        * UDP is used when it must be fast and guaranteed delivery is not necessary 
* Managing network addresses and interfaces 
    * As a linux server admin you need to manage network addresses and network interfaces 
    * The network addresses can be assigned in two ways 
        * Fixed IP addresses (useful for servers and other computers that always need to be available at the same IP address)
        * Dynamically assigned IP addresses (useful for end user devices, and for instances in a cloud env)
            * To dynamically assign IP addresses you usually use a dynamic host config protocol (DHCP) server 
    * For a long time network cards in linux have had default names such as eth0, eth1, and eth2 
    * Naming is assigned based on the order of detection of the network card 
    * eth0 the first, eth1 the second, and so on
    * Works well in an env where a node has one or two network cards only 
    * If a node has multiple network cards that need to be dynamically added and removed 
        * This approach does not work so well because it is very hard to identify which physical network card is using which name 
    * RHEL 9 default names for network cards are based on firmware, device topology, and device type
    * Leads to network card names that always consist of the following parts 
        * Ethernet interfaces begin with an en
            * WLAN interfaces begin with wl 
            * WWAN interfaces begin with ww 
        * The next part of the name represents the type of adapter 
            * an o is for onboard 
            * s is for hotplug slot 
            * p is for a PCI location
            * Admins can also use x to create a device name that is based on the MAC address of the network card 
        * Then follows a number, which is used to represent an index of, ID, or port 
        * If the fixed name cannot be determined, traditional names such as eth0 are used 
    * Based on this information device names such as eno16777734 can be used
        * Standas for an onboard ethernet device with its unique index number 
    * Apart from this default device naming, network cards can be named based on BIOS device name as well 
    * In this naming scheme names such as em1 (embdedded network card 1)
        * OR p4p1 (which is PCI slot 4, port 1) can be used
* Validating network configuration
    * Before learning how to set up network information, must know how to verify current network information
    * Check the following network items
        * IP address and subnet mask 
        * routing 
        * availability of ports and services 
    * Validating network address configuration
        * ip (verify the config of the network address)
        * ip utility is a modern utility that can consider advanced networking features that have been introduced in the past decade 
        * With ip you can monitor many aspects of networking 
            * ip addr (to config and monitor network addresses)
            * ip route (to config and monitor routing information)
            * ip link (to config and monitor network link state)
        * Can also manage many other aspects of networking but you do not need to know about them for the exam
    * WARNING: ifconfig used in earlier linux versions
        * DO NOT USE ON MODERN LINUX DISTROS 
        * Linux has become important in cloud computer space, and networking has evolved alot to match cloud computing requirements 
        * Many new features have been added to linux networking 
        * with ifconfig you can not manage or validate these concepts 
    * Validating network config cont
        * ip addr show (show current network settings)
            * can be abbreviated as ip a s or even ip a
        * ip command is relatively smart and does not always require you to type the complete option
        * Example 8-1 Monitoring current network config with ip addr show (page 217)
        * Loopback interface is used for communication between processes 
        * Some processes use the IP protocol for internal communication
        * For that reason you will always find a loopback int
        * And the IP address of the loopback interface is always set to 127.0.0.1 
        * Important part of the output of the command is for the onboard ethernet card 
        * Example command shows the following items about its current status 
            * Current state (The most important part of this line is the test UP, which shows that this network card is currently up and available)
            * MAC address config: Unique MAC address that is set for every network card 
            * Can see the MAC address itself as well as the corresponding broadcast address 
            * IPv4 Configuration: This line shows the IP address that is currently set, as well as teh subnet mask that is used 
            * Can also see the broadcast address that is used for this network config 
            * NOtice that on some ints you may find multiple IPv4 addresses 
            * IPv6 configuration: Shows the current IPv6 address and its config 
            * Even if you have not configed anything 
            * Every interface automatically gets an IPv6 address, which can be used for communication on the local network only 
        * ip link show (if you are just interested in the link state of the network interfaces)
        * ip link show (repeats the link state information of the ip addr show command)
        * -s (option that will show current link statitics
        * Which gives information about packets transmitted and recieved as well as an overview of errors that have occurred during packet transmission
        * Example 8-2 ip link show output (page 218)
        * ip link show (command shows the current link state as down)
        * You can temp bring it up again by using ip link set 
        * ip link set (followed by dev device-name and up)
        * ip link set dev ens33 up
    * Exercise 8-1 Validating Network Config 
        1. Open a root shell 
        1. ip -s link show (this shows all existing network connections
            * In addition to stats about the number of packets that have been sent and associated error messages 
        1. ip addr show (To see the current address assignments for network ints on your server)
    * Validating routing 
        * Routing is an important aspect of networking 
        * ON every network that needs to communicate to nodes on other networks, routing is a requirement 
        * Every network has, at least, a default router (default gateway) that is set 
        * ip route show (show which router is used as the default router)
        * You should always perform one quick check to verify that your router is set correctly 
        * The default router at all times must be on the same network as the local IP address that your network card is using 
        * Example 8-3 ip route show (page 219)
    * Validating the availability of ports and services 
        * Network problems can be related to the local IP address and router settings
        * But can also be related to network ports that are not available on your server or on a remote server 
        * netstat or newer ss command (verify availability of ports on your server)
        * ss -lt (see all listening TCP ports on the local system)
        * Example 8-4 Using ss -lt to display all listening ports on the local system (page 220)
        * Notice where the port is listening on 
        * Some ports are only listening on the IPv4 loopback address 127.0.0.1 or the IPv6 loopback address ::1
            * Which means that they are locally accessible only and cannot be reached from external machines 
        * Other ports are listening on \* (astrick)
            * Which stands for all IPv4 addresses or :::* which represents all ports on all IPv6 addresses 
    * Exercise 8-2 Verifying network settings 
        1. Open a root shell to your server (ip addr show)
            * Shows the current network configs 
            * Note the IPv4 addresses that is used and the network device names that are used
            * Need these for later in the exercise
        1. ip route show (verify routing config)
        1. If connected to the internet can use ping to verify the connection to the internet is working properly 
            * ping -c 4 8.8.8.8 (send four packets to IP address 8.8.8.8)
            * Should get echo reply to verify connectivity 
        1. ip addr add 10.0.0.10/24 dev <yourdevicename>
            * Trmporarily set a new IP address 
        1. ip addr show 
            * Should see the newly set IP address, in addition to the IP address that was already in use 
        1. ifconfig (notice that you do not see the newly set IP address)
            * No options with ifconfig command that allow you to see it 
            * One example of why you should not use the ifconfig command anymore 
        1. ss -tul (see a list of all UDP and TCP ports that are listening on your server)
* Managing network config with nmtui and nmcli
    * Mentioned eariler RHEL 9 is managed by the network manager service 
    * systemctl status NetworkManager (to verify its current state)
    * When network manager comes up it reads the network card config script 
        * which are in /etc/NetworkManager/systemconnections
        * Have a name that starts with the name of the network interface the config applies to 
        * Like ens160.nmconnection
    * When working with network config in RHEL 9 you should know the difference between a device and a connection
        * A device is a network interface card 
        * A connection is the configuration that is used on a device 
    * In RHEL 9 you can create multiple connections for a device 
    * This makes sense on a mobile computer, for example, 
        * To differentiate between settings that are used to connect to the home network and settings that are used to connect to the corpo network 
    * Switching between connections on devices is common on end user systems but not so common on servers 
    * To manage the network connections that you want to assign to devices, you use the nmtui or the nmcli command 
    * EXAM tip: nmcli tool is cool and very powerful but it is not the easiest tool available 
        * To change network configs fast and efficiently you should use the menu driven nmtui utility 
        * May not be as cool as nmcli but it allows you to do what you need to do in less than a minute
    * Required permissions to change network configuration
        * Root user can make modifications to current networking 
        * However if a ordinary user is logged into the local console this user is able to make changes to network config as well 
        * As long as the user is using the system keyboard to enter either a graphical console or a text based console these permissions are granted 
        * The reason is that users are suppose to be able to connect their local system to a network 
        * Notice that regular users who have used ssh to connect to a server are not allowed to change the network config 
        * nmcli general permissions (to check your current permissions)
    * Configuring the network with nmcli 
        * ip addr add (to temp set an IP address on a network int)
        * Everything you do with the ip command is nonpersistent 
        * If you want to make your config persistent, use nmtui or nmcli
        * nmcli (show all connections)
        * Shows inactive and active connections
        * You can easily see the difference because inactive connections are not currently assigned to a device 
        * nmcli con show (example 8-5 showing current connection status page 223)
        * After finding the name of the connection you can use nmcli con show followed by the name of the connection to see all properties of the connection
        * Shows many properties 
        * man 5 nm-settings (to find out what exactly these settings are doing)
        * nmcli (show an overview of currently configd devices and the status of these devices)
        * nmcli dev status (show a list of devices)
        * nmcli dev show <devicename> (show settings for a specific device)
        * TIP nmcli might seem difficult 
            * Offers excellent command line completion features 
            * Just make that bash-completion package has been installed 
            * nmcli (TAB x2 should see all available options that nmcli expects at this moment)
            * Choose an option such as connection and press Tab twice 
            * Using this approach helps you to compose long commands without the need to memorize anything 
    * Exercise 8-3 Managing network connections with nmcli
        * In this exercise you create a new connection and manage its status
        * This connection needs to be connected to a network device 
        * ens33 is used
        * Run this exercise from a console session not using SSH connection
        * If necessary change this to the name of the network device in use on your computer 
        1. Create a network connection by typing (nmcli con add con-name dhcp type ethernet ifname ens33 ipv4.method auto)
        1. Create a connection with the name static to define a static IP address and gateway 
            * nmcli con add con-name static ifname ens33 autoconnect no type ethernet ip4 10.0.0.10/24 gw4 10.0.0.1 ipv4.method manual 
            * The gateway might not exist in your config but that does not matter
        1. nmcli con show (show connections)
            * nmcli con up statis (activate the static connection)
            * Switch back to the DHCP connection using (nmcli con up dhcp)
    * Config the network with nmcli cont 
        * nmcli con add
        * You can also change current connection properties by using nmcli con mod 
    * Exercise 8-4 Changing Connection Parameters with nmcli 
        1. nmcli con mod static connection.autoconnect no (make sure that the static connection does not connect automatically)
        1. nmcli con mod static ipv4.dns 10.0.0.10 (add a DNS server to the static connection)
            * Notice that while adding a network connection, you use ip4 
            * Modifying parameters for an existing connection, you often use ipv4 instead 
        1. nmcli con mod static +ipv4.dns 8.8.8.8 (to add a second item for the same parameter, use a + sign)
        1. nmcli con mod (you can also change parameters such as the existing IP address)
            * nmcli con mod static ipv4.addresses 10.0.0.100/24
        1. nmcli con mod statis +ipv4.addresses 10.20.30.40/16 (add a second Ip address (+ sign again))
        1. nmcli con up static (activate the connection after changing the properties)
    * Config the network with nmcli cont
        * Should be all you need to know for the exam 
        * Very rich command 
        * Exact syntax of the command may be hard to remember 
        * Excellent man page 
        * man nmcli-examples (show the man page)
        * If you can find this man page you can do almost anything with nmcli 
        * Don't forget tab completion with nmcli also 
    * Configuring the network with nmtui 
        * if you do not like the complicated syntax of nmcli command you may like nmtui 
        * text user interface that allows the creation of network connections easily 
        * The nmtui interface consists of three menu options 
            * Edit a connection: Create new or edit existing connections
            * Activate a connection: (re)activate a connection
            * Set system hostname: Set the hostname of your computer 
        * Option to edit a connection offers almost all the features that you might ever need while working on network connections
        * Allows you to do anything you need to be doing on the exam 
        * Use it to add any type of connection
        * Not just ethernet connections, but also more advanced connection types
        * Like network bridges 
        * teamed network drivers are supported 
        * When selecting the option edit a connection
        * You get access to a rich interface that allows you to edit most properties of network connections
        * After editing the connection you need to deactivate it and activate it again
        * TIP: nm-connection-editor instead of nmtui (for GUI)
            * Be prepared that this interface offers a relatively restricted option set 
            * Does not contain advanced options 
            * Such as the options to create network team interfaces and manage network bridge interfaces 
            * Does offer all you need to manage address configs on a network connection
            * nm-connection-editor (start or by using the applet in the GNOME graphical interface)
    * Working on Network Configuration files 
        * /etc/NetworkManager/system-connections (every connection that you create is stored as a config file in this dir)
        * Name of the config files start with the name of the connection, followed by .nmconnection
        * Previous versions of RHEL network connection were stored in the /etc/sysconfig/network-scripts dir
        * If NetworkManager find legacy connection scripts in this dir, they will still be used 
        * But NetworkManager connection scripts are no longer stored by default at this location
        * Example 8-7 example of a network manager connection file 
* Setting up hostname and name resolution
    * To communicate with other host, hostnames are used
    * Important to know as an admin
    * Need to make sure that hosts can contact one another based on hostnames by setting up hostname resolution
    * Hostnames 
        * Hostnames are used to access servers and the services they are offering 
        * Important to know how to set up the system hostname 
        * Hostname typically consist of different parts 
        * Name of the host and the DNS domain (Domain name system) in which the host resides 
        * These two parts together make up the fully qualified domain name (FQDN)
        * server1.example.com (for example)
        * Good practice to specify an FQDN and not just the hostname
        * Because the FQDN provides a unique identity on the internet 
        * There are different ways to change the hostname 
            * Use nmtui and select the option change hostname 
            * hostnamectl set-hostname 
            * edit the contents of the config file /etc/hostname 
        * To config hostname with hostnamectl
            * hostnamectl set-hostname myhost.example.com
            * hostnamectl status (show the current hostname)
        * hostnamectl status (not only information about the hostname)
        * Also info about the Linux Kernel, virtualization type (and more)
        * Can set the hostname using nmtui interface
        * To set hostname resolution, you typically use DNS 
        * Config a DNS server is not an RHCSA objective 
        * But you need to know how to config your server to use an existing DNS server for hostname resolution
        * Apart from DNS, you can config hostname resolution in /etc/hosts file 
        * cat /etc/hosts 
        * All hostname IP address definitions as set in /etc/hosts will be applied b4 the hostname in DNS is used 
        * This is configed as a default in the hosts liune in /etc/nsswitch.conf
        * Which by default looks like: hosts: files dns myhostname 
        * Setting up an /etc/hosts file is easy 
        * Just make sure that it contains at least two columns 
        * First column has the IP address of the specific host
        * Second column specifies the hostname 
        * Hostname can be provided as a short name (like server1) 
        * Or a FQDN
        * FQDN hostname as well as the complete DNS name are included (server1.example.com)
            * If a host has more than one name
            * Like a short name and a fully qualified DNS name
            * You can specify both in /etc/hosts 
            * In that case, the second column must contain the FQDN
            * 3rd column can contain the alias 
    * DNS Name Resolution
        * If you want to communicate with other hosts on the internet
            * Just using an /etc/hosts is not enough for name resolution
        * Should use DNS too 
        * To specify which DNS server should be used
            * Set the DNS server using nmcli or nmtui 
        * NetworkManager config stores the DNS information in the config file for the network connection
        * /etc/sysconfig/network-scripts
        * From there pushes the config to the /etc/resolv.conf file
            * Which is used for DNS name server resolving 
        * Do not edit /etc/resolv.conf directly
            * As it will be overwritten the next time you restart NetworkManager 
        * It is recommended to always set up at least two DNS name servers to be contacted 
        * If the first name server does not answer, the second server is contacted 
        * Few different options to specify which DNS server you want to use 
            * nmtui to set DNS name server
            * Use a DHCP server that is configd to hand out the address of the DNS name server 
            * nmcli con mod <connection-id> [+]ipv4.dns <ip-of-dns>
        * Notice that if your computer is configed to get the network config from a DHCP server, the DNS server is also set via DHCP server 
        * If you do not want this to happen 
            * nmcli con mod <con-name> ipv4.ignore-auto-dns yes 
        * getent hosts <servername> (to verify hostname resolution)
            * This command searches in both /etc/hosts and DNS to resolve the hostname that has been specified 
        * EXAM note: Do not specify the DNS server directly in /etc/resolv.conf
            * They will be overwritten by NetworkManager when it is (re)started
* Summary 
    * Learned how to config networking in RHEL 9 
    * How IP protocol is used to connect computers
    * Which techniques are used to make services between hosts accessible 
    * Verify the network config using ip utility and some related utilities 
    * How to set IP addresses and other host configs in a permanent way by using either the nmcli or nmtui utility 
* Exam preparation tasks 
* Review all key topics 
    * IPv4 and IPv6 short descriptions 
    * Private network addresses 
    * Binary-decimal conversion overview
    * IP address types 
* Complete tables and lists from memory 
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
* Review questions 
* End of chapter lab

