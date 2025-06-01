9u# Part Two Operating Running Systems 

## Chapter 9 Managing Software 

* The following topics are covered in this chapter 
    * Managing software packages with dnf 
    * Using dnf 
    * Managing package modules 
    * Managing software packages with rpm
* The following RHCSA exam objectives are covered in this chapter 
    * Install and update software packages from red hat network, a remote repo, or from the local file system
* Managing Software 
    * Learn how to manage software packages from the command line by using dnf utility 
    * Learn which role repos play in software management with dnf 
    * Cover working with Package Modules
        * A solution that makes it possible to work with the specific version packages that you need in your env
    * Learn how to manage software with rpm command (useful to query new and installed software packages)
* Do I know this already quiz 
    * Foundation topic sections
        * Managing software packages with dnf
        * using dnf
        * Managing package modules 
        * Managing software packages with rpm
* Managing software packages with dnf
    * dnf (the default utility used to manage software packages on RHEL)
    * dnf is designed to work with repos 
        * repos are online depots of available software packages
    * Learn how to create and manage repos 
    * How to manage software packages based on the content of the repos 
    * Understanding the role of repositories 
        * Software on RHEL is provided in the Red Hat Package Manager (RPM) format 
        * This is a specific format used to archive the package and provide package metadata as well 
        * repos play a key role in working with software in RHEL 
        * Working with repos make it easy to keep your server current
        * The maintainer of the repo publishes updated packages in the repo 
        * The result is that whenever you use the dnf command to install software 
        * The most recent version of the software is automatically used 
        * Another major benefit of working with dnf is the way that package dependencies are dealt with 
        * On Linux (and most other modern OSs) software packages have dependencies 
        * This means that to be able to use one package, other packages may have to be present as well 
        * Without using repos, that would mean these packages would have to be installed manually 
        * The repo system takes care of resolving dependencies automatically 
        * If a package is going to be installed, it contains information about the required dependencies 
        * The dnf command then looks in the repo configed on this system to fetch the dependencies automatically 
        * If all goes well the installer just sees a short list of the dependencies that will be installed as a dependency to install the package 
        * If you are using RHEL with the repos that are provided for registered installations on RHEL 
            * There is no reason why this procedure should not work
            * The attempts to install software will usually succeed 
        * While installing RHEL 9, you are asked to register with RH customer portal, which provides different repos 
        * After registering, you can install software packages that are verified by RH automatically 
        * If you choose to install RHEL without registration
        * It cannot get in touch with the RH repos 
            * And you end up with no repos at all 
            * In which case you will have to be able to config a repo client to specify yourself which repo you want to use 
        * Note that repos are specific to OSs 
        * If you are using RHEL you should use RHEL repos only 
        * DO not try for instance to add CentOS repos to a RHEL 
        * If you want to provide additional software from the Fedora Project to a RHEL server (which for support reasons is not recommended)
            * You can consider adding the EPEL (Extra package for enterprise linux) repo
            * fedoraproject.org/wiki/EPEL for more information
            * Including information on how to config your system to use EPEL repo 
        * Warning: B4 adding the EPEL repo to RHEL, make sure that is does not break your current support status
            * EPEL packages are not managed by RH and ading them may break supported RH packages 
    * Registering Red Hat Enterprise Linux for support 
        * RHEL is a support Linux OS that requires you to register 
        * To register RHEL, you need a valid entitlement
        * This entitlement is associated to your account on the RH customer portal 
        * You can obtain an entitlement by purchasing a sub for RHEL 
        * OR by joining the RH developer program (which gives access to the no cost RH Enterprise Developer subscription
        * With a developer sub you are allowed to install a max of 16 RHEL systems 
            * You will not get any support on these systems
            * But will be able to access RH repos and receive updates 
        * Sign up at developers.redhat.com
        * After obtaining a valid subscription for red hat enterprise linux you can use the RH subscription management (RHSM) tool to manage your entitlement 
        * Managing an entitlement involves four basic tasks:
        * Register: While registering a sub you connect it to your current RH account.
            * As a result the subcription-manager tool can inventory the system
            * If a system is no longer used it can also be unregistered
        * Subscribe: Subscribing a system gives it access to updates for RH products that your subscription is entitled to 
            * Also by subscribing you will get access to the support level that is associated with your account 
        * Enable Repositories: 
            * After subscribing a system, you will get access to a default set of repos
            * Some repos by default are disabled but can be enabled after subscribing your system
        * Review and track: You can review and track current subscriptions that are in use 
    * Managing subscriptions 
        * You can manage subs either from GNOME graphical interface or from the command line 
        * The subscription-manager tool is used for managing subscriptions from the command line 
        * You can use it for the following ways 
        * Register a system: `subscription-manager register` to register
            * IT will prompt for the name of your RH user account as well as your password 
            * After entering these your RHEL server will be registered 
        * List available subscriptions: each account has access to specific subscriptions 
            * `subscription-manager list --available` (to see what your account is entitled to)
        * Automatically attach a subscription: registering a server is not enough to get access to the repo 
            * `subscription-manager attach --auto` (to automatically attach your sub to the repo that are available)
        * Get an overview: to see which subscriptions you are currently useing
            * subscription-manager list --consumed 
        * Unregister: If you are going to deprovision a system
            * `subscription-manager unregister`
            * If you have access to a limited number of registered system only, unregistering is important to ensure that you don't run out of available licenses 
        * After you register and attach a subscription, entitlement certificates are written to /etc/pki dir
        * In /etc/pki/product, stored certs indicates which RH products are installed on this system
        * In /etc/pki/consumer, stored certs ID the RH account to which the system is registered
            * /etc/pki/entitlement dir contains information about the subscription that are attached to this system
    * Specifying which repo to use 
        * On most occasions, after the install of your server has finished, it is configd with a list of repos that should be used 
        * You sometimes have to tell your server which repo should be used for example if 
            * You want to distribute nondefault software packages through repos 
            * You are installing RHEL without registering it 
        * Telling your server which repo to use is not difficult, but is important to know (for the EXAM as well)
        * IMPORTANT: to learn how to work with repos and software packages, do not use the repos that are provided be default 
            * So if you have installed RHEL do not register using subscription-manager
            * And if you have installed CentOS remove all files from /etc/yum.repos.d
            * If you overlooked this requirement while installing earlier you can use subscription-manager unregister to remove all registration
            * subscription-manager unregister (remove all registration)
        * To tell your server which repo to use you need to create a file with a name that ends in .repo in the dir /etc/yum.repos.d
        * Following parameters are commonly used
            * [label] (the .repo file can contain different repos, each section starting with a label that identifies the specific repo)
            * name= (Use this to specify the repo you want to use)
            * baseurl= (this option contains the URL that points to the specific repo location)
            * gpgcheck= (Use this option to specify if a GNU privacy guard (GPG) key validity check should be used to verify that packages have not been tampered with)
        * Older versions of RHEL you needed to memorize how to create a repo client file 
        * RHEL 9 the dnf config-manager tool is available 
        * Even in a minimal installation to create repo client file for you 
        * dnf config-manager --add-repo=http://reposerver.example.com/BaseOS (to easily generate the repo client file)
            * Make sure to replace the URL in this example with the correct URI that points to the location of the repo that you want to use 
            * If for instance you have copied the contents of the RHEL 9 installation disk to the /repo dir, you would be using a file :// URI
            * dnf config-manager --add-repo=file:///repo/BaseOS (would add the BaseOS repo based on the example above)
        * If you are using the dnf config-manager tool to add repos
        * You need to edit the repo file in /etc/yum.conf.d after adding it
            * So that it includes the line gpgcheck=0
        * Without that option the dnf tool wants to do a GPG check on incoming packages, which requires additional complex config that is not needed on the exam
        * Example 9-1 Repo file example (page 243)
        * In the repo config file several options can be used 
    * Table 9-2 Key options in .repo files 
        * [label]
            * Contains the label used as an identifier in the repo file 
        * name= 
            * Mandatory option that specifies the name of the repo 
        * mirrorlist=
            * Optional parameter that refers to a URL where information about mirror servers for this server can be obtained
            * Typically used for big online repo only 
        * baseurl=
            * Mandatory option that refers to the base URL where RPM packages are found
        * gpgcheck=
            * set to 1 if a GNU privacy guard (GPG) integrity check needs to be performed on the packages 
            * If set to 1, a GPG key is required 
        * gpgkey=
            * Specifies the location of the GPG key that is used to check package integrity
    * Specifying which repo to use cont
        * When you are creating a repo file
            * The baseurl parameter is the most important because it tells your server where to find the files that are to be installed 
        * The baseurl takes as its argument the URL where files need to be installed from
        * This will often be an HTTP or FTP URL, but it can be file based URL as well 
        * When you use a URL two components are included
            * First the URL identifies the protocol to be used and is in the format protocol://
            * Such as http://, ftp://, or file://
            * Following the URL is the exact location on that URL 
            * That can be the name of a web server or an FTP server
            * Including the subdirs where the files are found
            * If the URL is file based, the location on the file system starts with a / as well 
        * Therefore, for a file system based URL 
            * There will be three slashes in the baseurl 
            * Such as baseurl:///repo (which refers to the dir /repo on the local file system)
    * Understanding repository security 
        * Using repos allows you to transparently install software packages from the internet
        * Convenient, but also involves a security risk 
        * When installing RPM packages, you do that with root permissions 
        * And if in the RPM package sript code is executed (which is common) it is executed as root as well 
        * So you need to make sure you trust the software package you are trying to install from 
        * This is why repos in general use keys for package signing 
        * Also why on RHEL it is a good idea to use trusted repos only
        * To secure packages in a repo these packages are often signed with a GPG key 
        * This makes it possible to check whether packages have been changed since the owner of the repo provided them 
        * THe GPG key used to sign the software packages is typically made available through the repo as well 
        * The users of the repo can download that key and store it locally 
        * So that the package signature check can be performed automatically each time a package is downloaded from the repo 
        * If repo security is compromised and an intruder manages to hack the repo server and put some fake packages on it 
            * The GPG key signature will not match 
            * and the dnf command will complain while installing new packages 
        * Highly recommended to use GPG keys when using internet repos 
        * If you are using a repo where GPG package signing has been used
            * ON first contact with that repo the dnf command will propose to download the key that was used for package signing 
            * This is a transparent procedure that requires no further action
        * The GPG keys that were used for package signing are installed to /etc/pki/rpm-gpg dir by default 
        * TIP FOr using internel repos, the security risk are not that high 
            * For that reason you do not have to know how to work with GPG signed packages on the exam
    * Example 9-2 On first contact with a repo, the GPG key is downloaded 
    * Creating your own Repository 
        * Not a requirement for RHCSA 
        * But useful if you want to test setting up and working with repos 
        * Also if you are using a RHEL system that is not connected to Red Hat Repo, it is the only way to install packages 
        * Procedure is not hard to summarize 
            * You need to make sure all RPM packages are available in the dir that you want to use as a repo 
            * After doing that you need to use the createrepo command to generate the metadata that enables you to use that dir as a repo 
            * If you are using the RHEL 9 installation disk, it is even easier, as you do not have to generate the repo metadata
    * Exercise 9-1 Creating your own repo 
        * To perform this exercise, you need to have access to the RHEL or CentOS installation disk or ISO file 
        1. INsert the installation disk in your virtual machine and make sure it is attached and available 
        1. Open a root shell and type mkdir /repo (so you have a mount point where you can mount the ISO file)
        1. Adding the following to the end of the /etc/fstab config file 
            * /dev/sr0/repo iso9660 defaults 0 0 
        1. mount -a 
            * mount | grep sr0 
            * You should now see that the optical device is mounted on the dir /repo 
            * At this point the dir /repo can be used as a repo 
        1. Now two subdirs are available through the /repo dir 
            * The BaseOS repo provides access to the base packages 
            * THe application stream (appstream) repo provides access to application streams (these repos are described in more detail later)
            * To make them accessible you need to add two files to the /ect/yum.repo.d dir 
            * Start with the file BaseOS.repo 
            * dnf config-manager --add-repo=file:///repo/BaseOS (to generate this file)
        1. Add the file /etc/yum.repos.d/AppStream.repo using the following command 
            * dnf config-manager --add-repo=file:///repo/AppStream
        1. ls /etc/yum.repos.d/ (This should show two new files: repo_BaseOS.repo and repo_AppStream.repo 
            * Add the following lines to the end of both files 
            * gpgcheck=0
        1. dnf repolist (to verify the availability of the newly created repo 
            * SHould show the name of both repos 
            * Including the number of packages offered through this repo 
            * Notice on RHEL you will also see a message that this system is not registered 
    * Example 9-3 Verifying repo availability with dnf repolist 
        * dnf repolist 
* Using dnf 
    * At this point you should have operational repos (so time to start using them)
    * dnf command to use repos 
    * This command enables you to perform several tasks on the repo 
    * Table 9-3 Common dnf tasks
        * search 
            * search packages for a string that occurs in the package name or summary 
        * search all 
            * search packages for a string that occurs in the package name, summary, or description
        * [what]provides */name 
            * Performs a deep search in teh package to look for specific files within the package 
        * info 
            * provides more information about the package 
        * install 
            * install the package 
        * remove 
            * remove the package 
        * list [all | installed]
            * List all or installed packages
        * group list 
            * list package groups 
        * group install 
            * install all packages from a group 
        * update 
            * update package specified 
        * clean all 
            * remove all stored metadata 
    * Using dnf to find software packages 
        * To install packages with dnf, you first need to know the name of the package 
        * dnf search can help you with that 
        * dnf search: first gets in touch with the online repo (which might take a minute)
            * after which it downloads the most recent repo metadata to the local machine 
        * dnf search looks in the package name and description for the string you have been looking for 
        * dnf search all (if this does not give the expected results)
            * Performs a deeper search in the package description as well 
        * Example 9-4 dnf search Sample output (page 248)
        * Because the dnf search command looks in the package name and summary only, it often does not show what you need 
        * In some cases you might need to find a package that contains a specific file 
        * dnf whatprovides (command to do this)
        * dnf provides (also could help)
        * There is no functional difference between these two commands
        * There is even a 3rd option that does exactly the same: dnf wp 
        * To make it clear that you are looking for packages containing a specific file:
            * You need to specify the filename as */filename
            * Or use the full pathname to the file you want to use 
            * dnf whatprovides */Containerfile (if you are looking for the package containing the file Containerfile)
    * Getting more information about packages 
        * B4 you install a packagem, it is a good idea to get some more information about the package 
        * dnf info (followed by the name of the package)
    * Example 9-5 Sample Output of dnf info nmap 
        * dnf info nmap (page 249)
    * Installing and removing software packages 
        * after looking over dnf info and are happy with the package next step is installing 
        * dnf install (name of package: dnf install nmap)
        * When used in this way, dnf asks for confirmation
        * If you are sure about the install you can pass a -y option
            * which passes a "yes" to the confirmation prompt that dnf normally issues 
        * Example 9-6 Installing Software with dnf (page 250)
        * dnf starts by analyzing what is going to be installed 
        * In example 9-6 you can see that dnf starts by analyzing what is going to be installed 
        * Once that is clear it gives an overview of the package that is going to be installed 
        * Including dependencies
        * Then the package itself is installed to the system 
        * To remove the s/w packages from a machine, use the dnf remove command 
        * This command also does a dependency analysis
        * which means that it will remove not only the selected package but also all packages that depend on it 
        * This may sometimes lead to a long list of software packages that are going to be removed 
        * To avoid unpleasant suprises, you should never use dnf remove with the -y option
    * NOTE some packages are protected 
        * Therefore, you cannot easily remove them 
        * If dnf remove encounters protected packages, it refuses to remove them 
    * Showing Lists of packages 
        * When working with dnf, you may also use dnf list command to show lists of packages 
        * dnf list (without args shows a list of all s/w packages that are available)
        * Including the repo they were installed from (assuming that the package has been installed)
        * If a repo name is shown, the package is available in that specific repo 
        * If @anaconda is listed, the package has already been installed on this system
        * Example 9-7 shows the partial output of the dnf list command 
        * Example 9-7 Partial Output of the dnf list command (page 252 
        * If you only want to see which packages are installed on your server, you can use the dnf list installed command 
        * dnf list command can also prove useful when used with the name of a specific package as its argument 
        * dnf list kernel (to show which version of the kernel is actually installed and which version is available as the most recent version in the repo 
        * Particularly useful if your system is using online repos and you want to check if a new version of the package is available 
        * Example 9-8 shows the results of this command taken from a registered RHEL 9 system 
    * Example 9-8 Use dnf list packagename for information about installed and available versions 
    * Updating Packages
        * Major benefit of working with dnf repo is that repos make it easy to update packages 
        * The repo maintainer is responsible for copying updates packages to the repo 
        * The index in the repo always contains the current version of a package in the repo 
        * On the local machine also, a database is available with the current versions of the packages that are used 
        * dnf update (current versions of packages that are installed are compared to the version of these packages in the repos)
        * As shown in example 9-9 dnf next shows an overview of updatable packages 
        * From this overview type y to install the update 
        * Notice that while updating packages the old version of the package is replaced with a new version of the package 
        * There is one exception (which is for the kernel package)
        * dnf update kernel (the kernel package is not updated but the newer kernel is installed in addition to the old kernel 
        * So that while booting you can select the kernel that you want to use 
        * Useful if the new kernel won't work because of hardware compatibility issues 
        * In that case, you can interrupt GRUB 2 boot process (see chapter 17) to start the older kernel 
    * Example 9-9 Using dnf update (page 254) 
    * Working with dnf package groups 
        * While managing specific sevices on a linux machine you often need several different packages 
        * For intance you want to make your machine a virtualization host, you need KVM packages, but also supporting packages such as qemu, libvirt, and the client package 
        * Or while configing your server as a web server, you need to install additional packages like PHP as well in many cases 
        * To make it easier to manage specific functionality instead of specific packages, you can work with package groups as well 
        * A package group is defined in the repo and dnf offers the group management commands to work with these groups 
        * For an overview of all current groups, use dnf group list 
        * Example 9-10 shows output
        * TIP: Name of the command is dnf group, but there are aliases that ensure that dnf group and even commands like dnf groupinstall are also working 
            * So you can use any of these commands 
        * example 9-10 showing available dnf groups (page 255)
        * Notice that some dnf groups are not listed by default 
        * To show those as well type `dnf group list hidden`
        * The list of groups is considerably longer 
        * The difference is that dnf group list shows environment groups, which contain basic functionality
        * Within an environment group, different subgroups can be used; these are displayed only when using dnf group list hidden
        * To get information about packages available in a group use dnf group info 
        * BC group names normally contain spaces, do not forget to put the entire group name between quotes 
        * dnf group info "Container Management" to see what is in the Container Management group 
        * As you can see in example 9-11 this command shows mandatory items and optional items in the group 
        * The items can be groups and individual packages 
    * Example 9-11 showing group contents with dnf group info (page 256)
    * Using dnf history 
        * While you are working with dnf all actions are registered 
        * You can use dnf history command to get an overview of all actions that have been issued 
        * For the history file it is possible to undo specific actions
        * Use dnf history undo followed by the number of the specific action you want to undo 
        * Example 9-12 you see the result of the dnf history command, where every action has its own ID 
        * Example 9-12 Showing past dnf action using dnf history page 257 
        * As you can see action number 2 altered one package and was used to install packages 
        * To undo this action completely type dnf history undo 2 
        * Exercise 9-2 you apply some of the most useful dnf commands for common package management tasks, as discussed previously 
    * Exercise 9-2 Using dnf for package management 
        1. Type dnf repolist to show a list of the current repos that your system is using 
        1. dnf search seinfo (this will give no matching results)
        1. dnf provides seinfo (This command shows that the setools-console-<version> package contains this file
        1. Install this package using dnf install -y setools-console 
            * depending on your current config you might notice that quite a few dependencies have to be installed to 
        1. dnf list setools-console (see that the package is listed as installed)
        1. dnf history (note the number of the last dnf command you use)
        1. dnf history undo <nn> (where <nn> is replaced with the number that you found in step 6
            * This undoes the last action, so it removes the package you just installed 
        1. Repeat the dnf list setools-console command (package is now listed as available but not as installed)
* Managing Package Modules 
    * Up to RHEL 7 all packages were offered in one repo 
    * This made package version management challenging, as RH has always maintained the philosophy that major versions of packages should not be changed during a distribution lifetime 
    * The issue is that changing a major version of any package often involves changing dependencies as well 
    * And if that happens it is very difficult to guarantee that all packages are installed with the right version
    * As a result of adhering to this philosophy, RH was not able to introduce Python3 during RHEL 7 lifetime 
    * The current Python2 version that was included in RHEL7 however became deprecated and customers had a hard time understanding this 
    * To offer a higher level of flexibility, with the intro of RHEL 8, RH introduced two different repos 
    * The BaseOS repo is for core operating system packages (and all packages in this repo will not change their major version during the distribution lifetime) 
    * The Application Stream (AppStream) repo contains other packages that may change their major version during the distribution lifetime 
    * Important applications like Python are provided as AppStream packages
    * To ensure that if a new major version becomes available during the distribution lifetime, this major version can be included 
    * Understanding dnf modules 
        * In the AppStream repo, content with varying life cycles is provided 
        * This content may be provided as traditional RPM packages but also as modules 
        * A module describes a set of RPM packages that belong together, and adds features to package management 
        * Typically modules are oganized around a specific version of an application
        * And in a module you will find module packages together with all of the dependencies for that specific version
        * Each module can have one or more application streams 
        * A stream contains one specific version and updates are provided for a specific stream 
        * By using streams, different versions of packages can be offered through the same repo 
        * When you are working with modules that have different streams, only one stream can be enabled at the same time 
        * This allows users to select the package version that is needed in their env 
        * Modules can also have one or more profiles 
        * A profile is a list of packages that are installed together for a particular use case 
        * You may find, for instance, a minimal profile, a default profile, a server profile, and many more 
        * While you are working with modules you may select which profile you want to use 
    * Table 9-4 dnf module terminology 
        * RPM 
            * The default package format 
            * Contains files, as well as metadata that describes how to install the files 
            * Optionally may contain pre and post installation scripts as well 
        * Module 
            * A delivery mechanism to install RPM packages 
            * In a module different versions and profiles can be provided 
        * Application Stream 
            * A specific version of the module 
        * Profile 
            * A collection of packages that are installed together for a particular use case 
    * Managing Modules 
        * The dnf command in RHEL 9 supports working with modules using dnf module command 
        * dnf module list (to find out which modules are available)
        * See sample output in Example 9-13 
        * NOTE: in RHEL 9.0 no modules are provided 
            * It is expected that in future updates modules will be provided 
            * To show the working of the dnf module command, all examples are taken from CentOS stream
        * Example 9-13 showing dnf module with dnf module list (page 260)
        * In the list of modules, you can see whether or not the module is installed and whether or not a specific stream is enabled 
        * To list specific streams for a module, use the dnf module list modulename comamnd 
        * For instance, use dnf module list maven to get details about streams that are available for the maven module
        * Example 9-14 Showing details about dnf modules with dnf module list (page 260)
        * After you find out which module streams are available, the next step is to get information about specific profiles 
        * You can use dnf module info to ontain this information
        * For instance dnf module info php to get more information about the php module 
        * This will provide information for profiles that are available in all the module streams 
        * To find profile information for a specific stream you can provide the stream version as an arg 
        * dnf module info php:8.1 
        * Example 9-15 showing information about dnf modules with dnf module list (page 261)
        * After you find module information, the next step is to enable a module stream and install modules 
        * Every module has a default module stream, providing access to a specific version
        * If that version is what you need, you don't have to enable anything 
        * If you want to work with a different version, you should start by enabling the corresponding module stream
        * For example, dnf module enable php:8.1 to enable that specific version
        * Enabling a module stream before starting to work with a specific module is not mandatory 
        * dnf module install to install packages from a module, packages from the default module stream will be installed 
        * You can also switch between application stream versions 
        * If for instance you are now on php:8.1 and want to change to php:8.2 
        * You have to type dnf module install php:8.2 
        * This will disable the old stream and enable the new stream
        * After doing this, to ensure that all dependent packages that are not in the module itself are updated as well, type dnf distro-sync to finalize the procedure 
* Managing Software Packages with rpm 
    * Once upon a time, repos did not exist and the rpm command was used to install package files after they had been downloaded
    * That worked but there was one major issue: the dependency hell 
    * Because RPM packages have always focused on specific functionality, to install specific software, a collection of RPM packages were normally required 
    * Therefore a missing dependency message was often issued while users were trying to install RPM packages
    * Which meant that to install the selected package, other packages needed to be installed first 
    * Sometimes a whole chain of dependencies needed to be installed to finally get the desired functionality 
    * That did not make working with RPM packages a joyful experience 
    * On modern RHEL systems, repos are used, and packages are installed using dnf
    * dnf considers all package dependencies and tries to look them up in the currently available repo 
    * rpm command no longer used for software installation
    * That does not mean the rpm command has become totally useless
    * You can still use it to query RPM packages 
    * TIP ON your system two package databases are maintained
        * the dnf database and the RPM database 
        * When installing packages through dnf, dnf database is updated first 
        * After which the updated information is synchronized to the RPM database 
        * If you install packages using rpm commaand, the update is written to the RPM database only and will not be updated to the dnf database
        * Important reason not to use rpm command to install software packages 
    * Understanding RPM filenames 
        * When you are working with RPM packages directly makes sense to understand how the RPM filename is composed 
        * Typical RPM filename looks like autofs-5.0.7-40.el7.x86_64.rpm
        * This name consists of several parts 
            * autofs: The name of the actual package 
            * 5.0.7: version of the package 
            * This normally corresponds to the name of the package as it was released by the package creator
            * -40: sub version of the package 
            * el7: RH version this package was created for 
            * x86_64: Platform (32 bits or 64 bits) this package was created for 
    * Querying the RPM database 
        * rpm command enables you to get much information about packages 
        * RPM queries can be a really useful way to find out how software can be configured and used 
        * rpm -qa (command like dnf list installed, shows a list of all software that is installed on the machine)
        * Use grep on this command to find out specific package names 
        * To perform queries on RPM packages, you need the name and not the version info 
        * After finding the package about which you want more information
        * You can start with some generic queries to find out what is in the package 
        * rpm -qi nmap (to get a description of the package)
        * This will perform a query of a package that is already installed on your system
        * It will query the package database to get more details about it 
        * rpm -ql nmap (which shows a list of all files that are in the package)
        * On some packages, the result can be a really long list of filename that is not particularly useful
        * rpm -qd nmap (shows all documentation available for the package)
        * rpm -qc nmap (shows all config files in the package)
        * Using RPM queries can really help in finding out more useful information about packages 
        * The only thing you need to know is the RPM package name that a specific file belongs to 
        * rpm -qf followed by the specific filename you are looking for 
        * rpm -qf /bin/ls (to find the name of the RPM package the ls command comes from)
    * Querying RPM package files 
        * RPM queries by default are used on the RPM database, and what you are querying are installed RPM packages 
        * It sometimes makes sense to query an RPM package file before actually installing it 
        * -p option to do this
        * without the -p option you will be querying the database not the package file 
        * Also when querying a package file you need to refer to the complete filename
        * Including the version number and all other info that you do nothave to use when querying RPM database
        * rpm -qp --scripts httpd-2.4.6-19.el7.centos.x86_64.rpm (queries the specific RPM file to see whether it contains scripts)
        * --scripts (query option that needs special attention)
        * Queries an RPM package or package file to see which scripts it contains (if any)
        * This option is especially important when combined with the -p option
            * to find out whether a package file that you are going to install includes any scripts
        * When you install RPM packages, you do so as root 
        * Before installing an RPM package from an unknown source
        * You need to make sure that it does not include any rogue scripts 
        * If you do not you risk installing malware on your computer without even knowing it 
    * Table 9-5 Common RPM query commands 
        * rpm -qf 
            * Use a filename as its arg to find the specific RPM package a file belongs to 
        * rpm -ql 
            * uses the RPM database to provide a list of files in the RPM package
        * rpm -qi 
            * Uses RPM database to provide package information (equivalent to yum info)
        * rpm -qd 
            * Uses the RPM dtabase to show all documentation that is available in the package
        * rpm -qc 
            * Uses the RPM database to show all config files that are available in the package 
        * rpm -q --scripts
            * Uses the RPM database to show scripts that are used in the package 
            * This is particularly useful if combined with -p option
        * rpm -qp <pkg>
            * the -p option is used with all the previous listed options to query individual RPM package files instead of RPM package database 
            * Using this option before installation helps you find out what is actually in the package before it is installed 
        * rpm -qR 
            * Shows dependencies for a specific package 
        * rpm -V 
            * Shows which parts of a specific package have been changed since intallation
        * rpm -Va 
            * Verifies all installed packages and shows which parts of the package have been changed since install 
            * This is an easy and convenient way to do package integrity check 
        * rpm -qa 
            * lists all packages that are installed on this server 
    * Using repoquery 
        * While rpm -qp provides useful tools to query packages before install
        * There is a slight problem with this command 
        * It works only on RPM package files, and it can not query files directly from the repo 
        * If you want to query packages from the repos before they are installed 
        * you need repoquery
        * This binary is not installed by default so make sure to install dnf-utils RPM package to use it 
        * repoquery command is pretty similar to rpm -q command and uses many similar options 
        * There is just one significant option missing: --scripts
        * A simple solution is to make sure that you are using trusted repos only
        * to prevent installing software that contains dangerous script code 
        * If you need to thoroughly analyze what an RPM package is doing when it is installed 
        * You can download it to your machine which allows you to use the rpm -qp --scripts command on the package 
        * To DL a package from the repo to the local dir you can use the yumdownloader command 
        * Comes from the yum-utils package 
    * Exercise 9-3 Using RPM queries (page 266)
        1. To practice working with rpm we need a package
            * It does not really matter which package that is
            * dnf install -y dnsmasq (you may get a message that the package is already installed)
        1. which dnsmasq (complete pathname of hte dnsmasq command)
        1. rpm -qf$(which dnsmasq)
            * This does an RPM file query on the result of which dnsmasq command
        1. Now that you know that the dnsmsaq binary comes from the dnsmasq package
            * rpm -qi dnsmasq to show more info about the package
        1. rpm -qi (useful but does not give the details that are needed to start working with software in the package 
            * rpm -ql dnsmasq to show a list of all files in the package 
        1. rpm -qd dnsmasq (show the available documentation)
            * Notice that this command reveals that there is a man page 
            * But there is also a doc.html file and a setup.html file in /usr/share/doc/dnsmasq-version dir
            * Open these files with your browser to get more information about the use of dnsmasq 
        1. rpm -qc dnsmasq (see which config files are used by dnsmasq)
        1. After install, it does not make much sense but it is always good to know which scripts are executed when a package is installed 
            * rpm -q --scripts dnsmasq (show the script code that can be executed from this RPM)
    * TIP: Working with RPM queries is a valuable skill on the RHCSA exam
        * If you know how to handle queries, you can find all relevant config files and the doc 
* Summary 
    * In this chapter you learned about how to work with software on RHEL
    * dnf to manage software packages coming from repos
    * rpm to perform queries on the packages on your system
    * Exam prep tasks
* Review All key topics 
    * Common dnf tasks
    * List RPM package name components 
    * Common RPM query commands 
* Complete tables and lists from memory 
* Define key terms
    * package
    * dnf
    * Red Hat Package Manager (RPM)
    * Repo
    * Dependency
    * Application Stream (AppStream)
    * Package group
    * Module
    * Stream
    * Profile
    * dependency hell
* Review Questions
* End of chapter lab
    * page 269


## Chapter 10 Managing Processes

* The following topcis are covered in this chapter 
    * Introducing process management 
    * Managing shell jobs
    * using common command line tools for process management
    * Using top to manage processes 
    * using tuned to optimize performance 
* Following RHCSA exam objectives are covered in this chapter
    * Identify CPU/memory-intensive processes and kill processes 
    * Adjust process scheduling 
    * Managing tuning profiles 
* Managing Processes 
    * Process management is an important task for a linux admin
* Do I know this already 
    * introducing process management
    * managing shell jobs
    * using common command-line tools for process management
    * using top to manage processes 
    * using tuned to optimize performance 
* Introducing process management 
    * For everything that happens on a linux server a process is started 
    * For that reason process management is among the key sills that an admin has to master 
    * To do this efficiently you need to know which type of process you are dealing with
    * Major distinction can be made between three process types 
        * Shell jobs (commands started from the command line)
            * They are associated with the shell that was current when the process was started 
            * Shell jobs are also referred to as interactive processes
        * Daemons (processes that provide services)
            * Normally started when a computer is booted 
            * Often (but certainly not in all cases) run with root privileges
        * Kernel threads (are part of the linux kernel)
            * You cannot manage them using common tools
            * But for monitoring of performance on a system, it is important to keep an eye on them
    * When a process is started it can use multiple threads 
    * A thread is a task started by a process and that a dedicated CPU can service 
    * Linux shell does not offer tools to manage individual threads 
    * Thread management should be taken care of from within the command 
    * If you want to manage a process efficiently paramount that you know what type of process you are dealing with 
    * Shell jobs require a different approach than the processes that are automatically started when a computer boots 
* Managing shell jobs 
    * When a user types a command a shell job is started 
    * If no particular measures have been taken, the job is started as a foreground process
    * Occupying the terminal it was started from until it has finished its work 
    * As a linux admin you need to know how to start shell jobs as foreground or background processes 
    * As well as what you can do to manage shell jobs
    * Running Jobs in the foreground and background 
        * By default any executed command is started as a foreground job
        * That means that you cannot do anything on the terminal where the command was started until it is done
        * For many commands that does not really matter bc the command often takes a little while to complete
        * After which it returns access to the shell from which it started 
        * Sometimes it might be useful to start commands in the background 
        * This makes sense for processes that do not require user interaction and take significant time to finish 
        * A process that does require user interaction will not be able to get that when running in the background 
        * And for that reason will typically stall when moved to the background
        * You can take two different approaches to run a proces in the background
        * If you know that a job will take a long time to complete you can start it with an & behind it 
        * This command immediately starts in the background to make room for other tasks to be started from the command line 
        * To move the last job that was started in the background back as a foreground job use fg command
        * This command immediately and with no further questions, brings the last job back to the foreground 
        * If multiple jobs are currently running in the background, you can move a job back to the foreground by adding its job ID, as shown by the jobs command 
        * A job might sometimes have been started that takes (much) longer than predicted
        * If that happens, you can use Ctrl-Z to temporarily stop the job
        * This does not remove the job from memory
        * It just pauses the job so that is can be managed 
        * Once the job is paused you can continue it as a background job by using the bg command 
        * An alt key sequence that you can use to manage shell jobs is Ctrl-C 
        * This key combo stops the current job and removes it from memory 
        * A related key combo is Ctrl-D (which sends the End Of File (EOF) character to the current job)
        * The result is that the job stops waiting for further input so that it can complete what it was currently doing
        * Result of Ctrl-D is sometimes similar to Ctrl-C but there is a difference 
        * When Ctrl-C is used, the job is just canceled and nothing is closed properly 
        * Ctrl-D the jobs stops waiting for further input and next terminates, often is just what is needed to complete in a proper way 
    * Managing Shell Jobs 
        * When you are moving jobs between the foreground and background, it may be useful to have an overview of all current jobs
        * jobs (command)
        * Table 10-2 gives overview of all jobs currently running as a background job
        * Including the job number assigned to the job when starting it in the background
        * These job numbers can be used as an arg to the fg and bg commands to perform job management tasks
        * Exercise 10-1, learn how to perfom common job management tasks from the shell 
    * 10-2 Job management overview
        * & (used at the end of a command line)
            * Starts the command immediately in the background 
        * Ctrl-Z
            * Stops the job temporarily so that it can be managed 
            * For instance, it can be moved to the background
        * Ctrl-D 
            * Sends the EOF character to the current job to indicate that it should stop waiting for further input 
        * Ctrl-C
            * Can be used to cancel the current interactive job
        * bg 
            * Continues the job that has just been frozen using Ctrl-Z in the background
        * fg 
            * Brings back to the foreground the last job that was moved to background execution
        * jobs 
            * Shows which jobs are currently running from this shell
            * Displays job numbers that can be used as an arg to the commands bg and fg 
    * Exercise 10-1 Managing Jobs 
        1. Open a root shell and type the following commands 
            * sleep 3600 &
            * dd if/dev/zero of=/dev/null &
            * sleep 7200
        1. Because you started the last command with no & after the command 
            * You have to wait 2 hours before you get back control of the shell
            * Ctrl-Z to stop the command 
        1. type jobs
            * You will see the three jobs that you just started 
            * The first two of them have the running state, the third is stopped
        1. bg 3 (to continue running job 3 in the background)
            * Note that because it was started as the last job, you did not really have to add the 3
        1. fg 1 (move job 1 to the foreground)
        1. Ctrl-C to cancel job number 1 
            * jobs to confirm that it is now gone
        1. Use the same approach to cancel jobs 2 and 3 also 
        1. Open a second terminal on your server 
        1. From that second terminal, type dd if=/dev/zero of=/dev/null &
        1. Type exit to close the second terminal 
        1. From the other terminal start top
            * You will see that the dd job is still running
            * It should show on top of the list of running processes 
            * From top press k to kill the dd job
            * It will prompt for a PID to kill 
            * Make sure to enter the PID of the process you want to terminate
            * And then press enter to apply the default values 
    * NOTE: You learned how to manage interactive shell jobs in this section
        * Note that all of these jobs are processes as well 
        * As the user who started the job you can also manage it 
        * IN the next section you will learn how to use process management to manage jobs started by other users
    * Understanding parent-child relations
        * When a process is started from a shell, it becomes a child process of that shell
        * In process management, the parent-child relationship between processes is very important 
        * The parent is needed to manage the child 
        * For that reason, all processes started from a shell are terminate when the shell is stopped 
        * This also offers an easy way to terminate processes no longer needed 
        * Processes started in the background will not be killed when the parent shell from which they were started is killed 
        * To terminate these processes, you need to use the kill command, as described later in this chapter 
        * Note: In eariler versions of the bash shell
            * Background processes were also killed when the shell they were started from was terminated
            * To prevent this the process could be started with nohup command in front of it 
            * Using nohup for this purpose is no longer needed for RHEL 9
            * If a parent process is killed while the child process still is active 
            * The child process becomes a child of systemd instead
* Using Common Command line tools for process management 
    * On a linux server, many processes are usually running
    * On an average server or desktop comp there are often more than 100 active processes
    * With so many processes being active things may go wrong
    * If that happens it is good to know how noninteractive processes can be stopped 
    * Or how the priority of these processes can be adjusted to make more system resources available for other processes
    * Understanding processes and threads 
        * Tasks on linux are typically started as processes 
        * One process can start several worker threads 
        * Working with threads makes sense, bc if the process is very busy 
            * The threads can be handled by different cpu
            * OR cpu cores available in the machine 
        * Linux admin you cannot manage individual threads (you can manage processes tho)
        * The programmer of the multithreaded app that has to define how threads relate to one another
        * Good to know that there are two different types of background processes 
            * Kernel threads 
            * Daemon processes
        * Kernel threads are a part of the linux kernel (each started with its own process identification number (PID))
        * When manageing processes, you can easily recognize the kernel processes bc they have a name that is between square brackets 
        * As an admin, you need to know that kernel threads cannot be managed
        * You cannot adjust their priority
        * Neither is it possible to kill them (except by taking the entire machine down)
    * Using ps to get process information
        * ps (most common command to get an overview of currently running processes)
        * If used without args, the ps command shows only the processes that have been started by the current user
        * You can use many different options to display different process properties
        * If you are looking for a short summary of the active processes, use ps aux 
        * If you are looking for the name and the exact command that was used to start the process ps -ef 
        * ps fax (shows hierarchical relationship between parent and child processes)
        * Example 10-2 using ps -ef to see exact commands used to start processes (page 280)
        * NOTE: For many commands options need to start with a hyphen
            * For some commands, this is not the case and using the hyphen is optional
            * ps command is one of these 
            * Old times of UNIX there were two main flavors
            * System V flavor, in which hyphens before options were mandatory
            * BSD flavor in which using hyphens was optional
            * ps command is based on both of these flavors (and some options don't have to start with a hyphen)
        * Example 10-3 Using ps fax to show parent child relationships between processes (page 281)
        * An important piece of info to get out of the ps command is the PID 
        * Many task require the PID to operate
        * This is why commands like ps aux | grep dd (which will show process details about dd, including its PID, is quite common)
        * An alt way to get the same result is to use pgrep command 
        * pgrep dd (to get a list of PIDs that have a name containing the string 'dd')
    * Understanding Process Priorities
        * On modern linux systems, cgroups are used to allocate system resources
        * In cgroups three system areas, the so called slices are defined
            * system: this is where all systemd-managed processes are running
            * user: this is where all user processes (including root processes) are running 
            * machine: this is optional slice is used for vms and containers
        * By default all slices have the same CPUweight
        * This means that CPU capacity is equally divided if there is high demand 
        * All processes in the system slice get as much CPU cycles as all processes in the user slice, and that can result in suprising behavior
        * Within a slice, process priority can be managed by using nice and renice 
    * Exploring relations between slices 
        * As mentioned before by default all processes in the system slice get as many CPU cycles as all processes in the user slice 
        * You won't get any questions about this on the RHCSA exam
        * But as it may lead to suprising situations, it is good to know how this works anyway 
        * Apply the following procedure to discover what the result can be
        1. Open a root shell and clone the course git repo:
            * git clone https://github.com/sandervanvugt/rhcsa 
        1. cp rhcsa/stree* /etc/systemd/system
        1. systemctl daemon-reload (to ensure that systemd cataches the new files)
        1. systemctl start stress1, followed by systemctl start stress2 
        1. top (to monitor cpu usage of processes)
            * You will see that there are two very active dd processes
            * Which each get about 50 percent of all CPU capacity
            * Keep the top screen open
        1. Open a terminal, and as a non root user, type while true; do true; done
        1. Observe what is happening in top
            * If you have a single core system you will see that both dd processes get 50 percent of all CPU cycles
            * And the user bash process that was just started also get 50 percent of all CPU cycles
            * This proves that one very busy user process can have dramatic consequences for the system processes
        1. If in the previous step you don't see the described behavior 
            * Type 1 in the top interface
            * This will show a line for each CPU core on your system
            * You should see multiple CPU cores 
        1. To temp shut down a CPU core, use the command echo 0 > /sys/bus/cpu/devices/cpu1/online
            * Repeat this command for each CPU except for cpu0
        1. To enable any CPU core you have just disabled use either echo 1 > /sys/bus/cpu/devices/cpu1/online or reboot
        1. Use killall dd to make sure all dd processes are terminated 
        * As you have just seen, the standard config of cgroup slices can lead to unexpected results 
        * If you don't like this behavior you can increase the priority of the system slice 
        * systemctl set-property system.slice CPUWeight=800 to set the CPUWeight of all processes in the system slices eight times as high as all processes in the user slice 
    * Managing process priorities
        * When linux processes are started they are started with a specific priority
        * By default all regular processes are equal and are started with the same priority
        * Which is the priority number 20
        * As shown by utilities like top
        * In some cases it is useful to change the default priority that was assigned to the process when it was started 
        * You can do that using nice and renice commands 
        * Use nice if you want to start a process with an adjusted priority
        * Use renice to change the priority for a currently active process 
        * Alternatively, you can use the r command from the top utility to change the priority of a currently running process 
        * Changing process priority may make sense in two different scenarios 
        * Suppose for example, that you are about to start a backup job that does no necessarily have to finish fast
        * typically backup jobs are rather resource intensive, so you might want to start the backup job in a way that does not annoy other users to much, by lowering its priority 
        * Another example is where you are about to start a very important calculation job
        * To ensure that it is handled as fast as possible you might want to give it an increase priority 
        * Taking away CPU time from other process 
        * On earlier linux versions, it could be dangerous to increase the priority of one job too much
        * Because of the risk that other processes (including vital kernel processes) might be blocked out completely 
        * On current linux kernels, that risk is minimized for these reasons
            * Modern linux kernels differentiate between essential kernel threads that are started as real-time processes and normal user processes
            * Increasing the priority of a user process will never be able to block out kernel threads or other processes that were started as real time processes 
            * Modern computers often have multiple CPU cores 
            * A single threaded process that is running with the highest priority will never be able to get beyond the boundarie of the CPU it is running on
            * As you have read before, processes are running in slices, and by default, each slice can claim as many CPU cycles as each other slices 
        * When using nice or renice to adjust process priority, you can select from values ranging from -20 and 19
        * The default niceness of a process is set to 0 (which results in the priority value of 20)
        * By applying a negative niceness, you increase the priority 
        * Use a positive niceness to decrease the priority 
        * It is a good idea not to use the ultimate values immediately
        * Instead use increments of 5 and see how it affects the application
        * TIP: do not set process priority to -20
            * It risk blocking other processes from getting served 
        * Let's take a look at examples of how to use nice and renice: 
            1. nice -n 5 dd if=/dev/zero of=/dev/null & (to an infinite I/O intensive job, but with an adjusted niceness so that some room remains for other processes as well)
            1. ps aux | grep dd (find the PID of the dd command that you just started. The PID is in the second column of the command output)
            1. renice -n 10 -p 1234 (replace 1234 with correct PID from last step)
            1. top (to verify the adjusted process priority and stop the dd process you just started)
        * Note the regular users can only decrease the priority of a running process 
        * You must be root to give processes increased priority by using negative nice values 
    * Sending Signals to processes with kill, killall, and pkill 
        * Before you start to think about the kill command or sending other signals to processes
        * Good to know that Linux processes have a hierarchical relationship
        * Every process has a parent process, and as long as it lives, the parent process is responsible for the child processes it has has created 
        * In older versions of linux killing a parent process would also kill all of its child processes 
        * RHEL 9, if you kill a parent process, all of its child processes become children of the systemd process
        * The linux kernel allows many signals to be sent to processes
        * Use man 7 signal for a complete overview of all the available signals 
        * Three of these signals work for all processes 
        * The signal SIGTERM (15) is used to ask a process to stop
        * The signal SIGKILL (9) is used to force a process to stop
        * The SIGHUP (1) signal is used to hang up a process
            * The effect is that the process will reread it config files
            * Which makes this a useful signal to use after making modifications to a process config file
        * To send a signal to a process, you use the kill command 
        * The most common use is the need to stop a process
        * Which you can do by using the kill command followed by the PID of the process
        * This sends the SIGTERM signal to the process which normally causes the process to cease its activity and close all open files 
        * Sometimes the kill command does not work because the process you want to kill can ignore it 
        * In that case you can use kill -9 to send the SIGKILL signal to the process 
        * Because the SIGKILL signal cannot be ignored it forces the process to stop but you also risk losing data while using this command 
        * In general it is a bad idea to use kill -9 
            * You risk losing data
            * Your system may become unstable if other processes depend on the process you just killed
        * TOP: use kill -l to show a list of available signals that can be used with kill 
        * There are some command that are related to kill:
        * killall
        * pkill 
        * The pkill command is a bit easier to use bc it takes then name rather than the PID of the process as an arg
        * You can use killall command if multiple processes using the same name need to be killed simultaneously
        * However recommended to use kill, followed by the exact PID of processes you want to stop
        * BC otherwise you risk terminating processes that did not need to be killed anyway 
        * Using killall was particularly common when linux env were multiprocessing instead of multithreading
        * In a multiprocessing env where a server starts several commands, all with the same name it is not easy to stop these commands one by one based on individual PID
        * Using killall enables you to terminate all these process simultaneously
        * In a multithreaded env, the urge to killall is weaker
        * Because there is often just one process that is generating several threads 
        * All these threads are terminated anyway by stopping the process that started them
        * You can still use killall to terminate lots of processes with the same name that have been started on your server 
    * Exercise 10-2 Managing Processes from the command line 
        1. Open a root shell 
            * From this shell, type dd if=/dev/zero of=/dev/null &
            * Repeat this command 3 times
        1. ps aux | grep dd 
            * This command shows all lines of output that have the letters dd in them 
            * You will see more than just the dd processes, but that should not matter
            * The processes you just started are listed last 
        1. Use the PID of one of the dd processes to adjust the nicencess, using renice -n 5 <PID>
        1. ps fax | grep -B5 dd 
            * The -B5 option shows the matching lines, including the five lines before that
            * Because ps fax shows hierarchical relationships between processes
            * You should also find the shell and its PID from which all the dd processes were started 
        1. Find the PID of the shell from which the dd processes were started and type kill -9 <pid>
            * BC the dd processes were started as background processes, they are not killed when their parent shell is killed
            * Instead they have been moved up and are now children of the systemd process
        1. Use killall to kill all remaining dd processes
    * Killing zombies
        * Zombies are processes with a special state 
        * Zombie processes are processes that have completed execution but are still listed in the process table
        * You can check if you have zombies using ps aux | grep defunct
        * Altho zombies are harmless it is annoying to have them, and you may want to do something to clean them up 
        * The issue with zombies is that you cannot kill them in the way that works for normal processes
        * Rebooting your system is a solution, but doing so is a bit too much for processes that are not really causing any harm
        * Fortunately in a recent RHEL system you can often (not in all cases) get rid of zombies by applying the following procedure 
        1. Make sure you have cloned the books git repo using git clone, https://github.com/sandervanvugt/rhcsa
        1. Enter the rhcsa dir, using cd rhcsa and use ./zombies to start the demo zombie process
        1. using ps aux | grep zombie to verify the zombie is running
            * You should see two processes, one being the parent that is responsible for the zombie
            * Other one being the zombie itself
        1. kill <childpid> (this fails)
        1. kill -SIGCHILD <parentpid>
            * This will tell the parent process to remove its child processes
            * Now the zombie will get adopted by systemd
            * After a few seconds it will be removed
        1. If the zombie was not killed by this procedure use kill -9 to kill the parent process
* Using top to manage processes
    * A convenient tool to manage processes is top
    * For common process management tasks, top is great bc it gives an overview of the most active processes currently running (hence the name top)
    * This enables you to easily find processes that might need attention
    * From top you can also perform common process management tasks
    * Such as adjusting the current process priority and killing processes
    * Figure 10-1 shows the int that appears when you start top 
    * Among the information that you can conveniently obtain from top utility is the process state
    * Table 10-3 provides an overview of the different process states that you may observe 
        * Running (R)
            * THe process is currently active and using CPU time, or in the q of runnable processes waiting to get services 
        * Sleeping (S)
            * The process is waiting for an event to complete 
        * Uniterruptible sleep (D)
            * The process is in a sleep state that cannot be stopped 
            * This usually happens while a process is waiting for I/O
            * This state is also known as blocking state 
        * Stopped (T)
            * The process has been stopped
            * While typically has happened to an interactive shell process, using the Ctrl-Z key sequence 
        * Zombie (Z)
            * The process has been stopped but could not be removed by its parent
            * Which has put it in an unmanageable state 
    * Now that you know how to use the kill and nice command line, using the same functionality from top is even easier 
    * From top, type k; top then prompts for the PID of the process you want to send a signal to
    * By default the most active process is selected 
    * After you enter the PID, top asks which signal you want to send 
    * By default signal 15 for SIGTERM is used 
    * However, if you want to insist on a bit more, you can type 9 for SIGKILL
    * Now press enter to terminate the process 
    * To renice a running process from top, type r 
    * You are first prompted for the PID of the process you want to renice 
    * After entering the PID you are prompted for the nice value you want to use 
    * Enter a positive value to decrease process priority or a negative value to increase process priority 
    * Another important parameter you can get from top is the load average 
    * The load average is expressed as the number of processes that are in a runnable state (R) or in a blocking state (D)
    * Processes are in a runnable state if they currently are running, or waiting to be services 
    * Processes are in a blocking state if they are waiting for I/O 
    * The load avg is shown in the last 1, 5, and 15 minutes 
    * And you can see the current values in the upper right corner of the top screen
    * Alternatively, you can use the uptime command to show current load stats (example 10-4)
    * Example 10-4 Using uptime for information about load average (page 289)
    * As a rule of thumb, the load average should not be higher than the number of CPU cores in your system
    * You can find out the number of CPU cores in your system by using the lscpu command 
    * If the load average over a longer period is higher than the number of CPUs in your system you may have performance problems 
    * In exercise 10-3 you investigate the load average stat and learn how to manage load average
    * Exercise 10-3 Managing Load Average 
        1. Open a root shell 
            * From this shell, type dd if=/dev/zero of=/dev/null & 
            * Repeat this command three times 
        1. top (observe the current load average)
            * After a few seconds use q to quit top 
        1. From the command line, type uptime
            * You should see the numbers that are shown as the load average is slowly increasing 
        1. lscpu and look for the number of CPU(s)
            * Also look for the core(s) per CPU parameter so that you can calculate the total number of cpu cores
        1. killall dd to kill all dd processes 
* Using tuned to optimize performance 
    * To offer the best possible performance right from the start, RHEL 9 comes with tuned 
    * It offers a daemon that monitors system activity and provides some profiles 
    * In the profiles, an admin can automatically tune a system for best possible latency, thruput, or power consumption
    * Based on the properties of an installed system, a tuned profile is selected automatically at install 
    * And after install it is possible to manually change the current profile 
    * Admins can also change settings in a tuned profile
    * Table 10-4 gives an overview of the important default profiles 
    * Table 10-4 tuned profile overview 
        * balanced 
            * the best compromise between power useage and performance 
        * desktop 
            * Based on the balanced profile, but tuned for better response to interactive apps 
        * latency-performance 
            * tuned for max throughput 
        * network-latency 
            * Based on latency performance, but with additional options to reduce network latency 
        * network-throughput 
            * Based on the throughput-performance optimizes older CPUs for streaming content 
        * powersave
            * tunes for max power saving
        * throughput-performance 
            * tunes for max throughput 
        * virtual-guest 
            * optimizes linux for running as a virtual machine 
        * virtual-host
            * optimizes linux for use as a KVM host
    * It is relatively easy to create custom profiles 
    * Also, when you are installing specific packages, profiles may be added 
    * So you may find that some additional performance profiles exist on your server 
    * To manage the performance profile, the tuned-adm command is provided 
    * It talks to the tuned daemon, so before you can use it, run systemctl enable --now tuned to start the tuned daemon
    * Next, use tuned-adm active to find out which profile is currently selected 
    * For an overview of profiles available on your server, type tuned-adm list 
    * To select another profile, type tuned-adm profile profile-name 
    * The tuned service can also recommend a tuned profile for your system: use tuned-adm recommend
    * Exercise 10-4 you can practice working with tuned 
    * Exercise 10-4 Using tuned 
        1. Use dnf -y install tuned (to ensure tuned is installed probably already is)
        1. systemctl status tuned (check whether tuned is currently running)
            * If not systemctl enable --now tuned (to enable)
        1. tuned-adm active (to see which profile currently is used)
        1. tuned-adm recommend (to see which tuned profile is recommended)
        1. To select and activate the throughput-performance profile, type tuned-adm profile throughput-performance
* Summary 
    * Managing processes is a common task for a linux system admin
    * IN this chapter you learned how to look up specific processes and how to change their priority using nice and kill 
    * You also learned how to use tuned to select the performance profile that best matches your server's workload 
* Exam preparation tasks 
* Review all key topics 
    * Table 10-2 Job management overview pg 236 
    * List Essential signals overview pg 244 
    * Table 10-3 Linux process states overview pg 247 
* Complete tables and lists from memory 
* Define key terms 
    * Process
    * thread
    * job
    * foreground process
    * backgound process
    * process identification number (PID)
    * nice 
    * kill 
    * signal 
    * zombie 
    * profile 
    * tuned 
* Review questions
* End of chapter lab


## Chapter 11 Working With Systemd

* The following topics are covered in this chapter 
    * Understanding systemd 
    * managing units through systemd
* The following RHCSA exam objectives are covered in this chapter 
    * Start, stop, and check status of network services 
    * start and stop services and config services to automatically start at boot 
* Working with Systemd 
    * In this chapter you learn about systemd 
    * Which is the system and service manager used on RHEL since RHEL7
    * You discover all the things that systemd can do
    * And after you have a good general understanding 
    * You learn how to work with systemd services 
    * Systemd is also involved in booting your system in a desired state, which is called a target 
    * That topic is covered in Chapter 17, managing and understanding the boot procedure 
* Do I know this already quiz 
    * Foundation topic section
        * Understanding systemd 
        * Managing units thru systemd 
* Foundation Topics 
* Understanding Systemd 
    * Systemd is the part of RHEL that is responsible for starting not only services but also a variety of other items
    * To decribe it in a generic way, the systemd system and service manager is used to start stuff
    * The stuff is referred to as units
    * Units can be many things
    * One of the most important unit types is the service 
    * Typically services are processes that provide specific functionality and allow connections from externel clients coming in
    * Such as the SSH service
    * The apache web server and many more
    * Apart from service, other unit types exist, such as socket, mount, and target
    * To display a list of available units, type systemctl -t help
    * Example 11-1 unit types of systemd 
    * Understanding systemd unit locations
        * The major benefit of working with systemd is that it provides a uniform interface to start units 
        * The interface is defined in the unit file
        * Unit files can occur in three locations
        * /usr/lib/systemd/system
            * Contains default unit files that have been installed from RPM packages
            * You should never edit these files directly 
        * /etc/systemd/system
            * Contains custom unit files
            * it may also contain files that have been written by an admin or generated by the systemctl edit command
        * /run/systemd/system
            * Contains unit files that have been generated automatically 
        * If a unit file exists in more than one of these locations, units in /run dir have highest precedence and will overwrite any settings that were defined elsewhere
        * Units in /etc/systemd/system have second highest precedence, and units in /usr/lib/systemd/system come last
    * Understanding systemd service units 
        * Probably the most important unit type is teh service unit 
        * It is used to start processes 
        * You can start any type of process by using a service unit, including daemon processes and commands 
        * Example 11-2 shows a service unit file, vsftpd.service, for the very secure FTP service 
        * Example 11-2 A service unit file 
        * You can see from this unit file example that unit files are relatively easy to understand
        * Systemd service unit files typically consist of the following three sections (other types of unit files have different sections)
        * [Unit]
            * Descibes the unit and defines dependencies
            * This section also contains the important After statement and optionally the Before statement
            * These statements define dependencies between different units, and they relate to the perspective of this unit
            * The Before statement indicates that this unit should be started before the unit that is specified
            * The After statement indicates that this unit should be started after the unit that is specified
        * [Service]
            * Describes how to start and stop the service and request status install
            * Normally you can expect an ExecStart line, which indicates how to start the unit, or an ExecStop line, which indicates how to stop the unit 
            * Note the Type option, which is used to specify how to process should start
            * The forking type is commonly used by daemon processes but you can also use other types,
            * such as oneshot and simple
            * which will start any command from a systemd unit
            * See man 5 systemd.service for more details 
        * [Install]
            * indicates in which target this unit has to be started 
            * The section "understanding systemd target units" a bit later in this chapter explains how to work with targets
            * This section is optional, but units that don't have an [Install] section cannot be started automatically 
    * Undserstanding Systemd Mount units 
        * A mount unit specifies how a file system can be mounted on a specific dir 
        * Mount units are an alt for mounting file systems through /etc/fstab (more in chapt 14)
        * Example 11-3 shows a mount unit file, tmp.mount
        * Example 11-3 A mount unit file (pg 299)
        * The tmp.mount unit file in example 11-3 shows some interesting additional config option in its sections
        * [Unit]
            * the conflicts statement is used to list units that cannot be used together with this unit
            * Use this statement for mutually exclusive units 
        * [Mount]
            * this section defines exactly where the mount has to be performed
            * Here you see the arg that are typically used in any mount command 
    * Understanding Systemd Socket Units
        * Another type of unit that is interesting to look at is the socket 
        * A socket creates a method for applications to communicate with one another
        * A socket may be defined as a file but also as a port on which Systemd will be listening for incoming connections
        * That way a service does not have to run continuously but instead will start only if a connection is comming in on the socket that is specified
        * every socket needs a corresponding service file 
        * Example 11-4 shows what the cockpit.socket file looks like; notice that this file requires a service file with the name cockpit.service 
        * Example 11-4 A socket unit file (page 300)
        * The important option in example 11-4 is ListenStream
        * this option defines the TCP port that systemd should be listening to for incoming connection
        * Sockets can also be created for UDP ports, in which case you would use ListenDatagram instead of ListenStream
    * Understanding systemd target units 
        * The unit files are used to build the functionality that is needed on your server 
        * To make it possible to load them in the right order and at the right moment
        * You use a specific type of unit: the target unit 
        * A simple definition of a target unit is "a group of units"
        * Some targets are used to define the state a server should be started in
        * As such, target units are comparable to the runlevels used in earlier versions of RHEL
        * Other targets are just a group of services that make it easy to manage not only individual units but also the units that are required to get specific functionality 
        * The sound.target is an example of such a target; you can use it to easily start or stop all units taht are required to enable sound on a system
        * Targets by themselves can have dependencies on other targets 
        * These dependecies are defined in the target unit 
        * An example of such a dependency relation is the basic.target 
        * This target defines all the units that should always be started 
        * You can use systemctl list-dependencies command for an overview of any existing dependencies
        * Example 11-5 shows the definition of a target unit file, multi-user.target, which defines the normal operational state of a RHEL server 
        * Example 11-5 a target unit file (page 301)
        * You can see that by itself the target unit does not contain any information about the units that it should start
        * It just defines what it requires and which services and targets it cannot coexist with
        * It also defines load ordering, by using the After statement in the [Unit] section
        * The target file does not contain any information about the units that should be included; that is defined in the [Install] section of the different unit files 
        * When admins use systemctl enable command, to ensure that a unit is automatically started while booting, the [Install] section of that unit is considered to determine to which target the unit should be added 
        * When you add a unit to a target, under the hood a symbolic link is created in the target dir in /etc/systemd/system
        * If, for instance you enabled the vsftpd service to be automatically started, you will find that a symbolic link /etc/systemd/system/multi-user.target/wants/vsftpd.service has been added, point to the unit file in /usr/lib/systemd/system/vsftp.service and thus ensuring that the unit will automatically be started 
        * In systemd terminology, this symbolic link is known as want, as it defines what the target wants to start when it is processed 
* Managing UNits through Systemd
    * Managing the current state of systmed units is an important tasks for RHEL admins 
    * Managing units means no only managing their current state but also charging options used by different units 
    * Managing systemd units starts with starting and stopping units 
    * As an admin you use the systemctl command to do that 
    * In excercise 11-1 you start, stop, and manage a unit 
    * After you config a unit so that it can be started without problems, you need to make sure that it restarts automatically upon reboot 
    * You do this by enabling or disabling the unit 
    * TIP: the sytemctl command has a large number of options, which may appear overwhelming at first sight, but there is no need to be overwhelmed
        * Just ensure that the bash-completion package is installed and use Tab completion on the systemctl command, which provides easy access to all of the available options
    * Exercise 11-1 Managing Units with systemctl 
        1. From a root shell, type dnf -y install vsftpd to install the very secure FTP service 
        1. type systemctl start vsftpd to activate the FTP server on your machine 
        1. Type systemctl status vsftpd to get output like shown in example 11-6, where you can see the vsftpd service is currently operational 
            * In the Loaded line, you can also see that the service is currently disabled which means that it will not be activated on a system restart 
            * The vendor preset also shows as disabled, which means that, by default after installation this unit will not automatically be enabled 
        1. systemctl enable vsftpd to create a symbolic link in the wants dir for the multiuser target to ensure that the service is automatically started after a restart
        1. systemctl status vsftpd again
            * You'll see that the unit file has changed from being disabled to enabled 
    * Example 11-6 Requesting current unit status with systemctl status (page 303)
    * When requesting the current status of a systemd unit you can see different kinds of information about it 
    * Table 11-2 Systemd status overview 
        * Loaded 
            * The unit file has been processed and the unit is active 
        * Active(running)
            * The unit is running with one or more active processes 
        * Active(exited)
            * The unit has successfully completed a one time run 
        * Active(waiting)
            * The unit is running and waiting for an event 
        * Inactive(dead)
            * The unit is not running 
        * Enabled 
            * The unit will start at boot time 
        * Disabled
            * The unit will not be started at boot time 
        * Static 
            * The unit cannot be enabled but may be started by another unit automatically 
    * As an admin you also often need to get a current overview of the current status of Systemd unit files 
    * Table 11-3 Systemctl unit overview commands 
        * systemctl -t service 
            * Shows only service units 
        * systemctl list-units -t service 
            * Shows all active service units (same result as previous command)
        * systemctl list-unit -t services --all
            * shows inactive service units as well as active service units 
        * systemctl --failed -t service 
            * shows all services that have failed 
        * systemctl status -l your.service 
            * shows detailed status information about services 
    * Managing dependencies 
        * In general there are two ways to manage systemd dependencies 
            * unit types such as socket, timer, and path are directly related to a service unit 
            * Systemd can make the connection because the first part of the name is the same: cockpit.socket works with cockpit.service
            * Accessing either of these unit types will automatically trigger the service type 
            * Dependencies can be defined within the unit, using keywords like Requires, Requisite, After, and Before 
        * As an admin you can request a list of unit dependencies 
        * systemctl list-dependencies followed by a unit name to find out which dependencies it has 
        * Add the --reverse option to find out which unit are required for this unit to be started 
        * Example 11-7 Showing unit dependencies (page 304)
        * To ensure accurate dependency management, you can use different keywords in the [Unit] section of a unit 
        * Requires:
            * If this unit loads, unit listed here will also load
            * If one of the other units is deactivated, this unit will also be deactivated
        * Requisite: 
            * If the unit listed here is not already loaded the unit will fail 
        * Wants: 
            * This unit wants to load the unit that are listed here, but it will not fail if any of the listed units fail 
        * Before: 
            * This unit will start before the unit specified with before 
        * After 
            * This unit will start after the unit specified with After 
    * Managing Unit Options 
        * When working with systemd unit files, you risk getting overwhelmed by it many options
        * Every unit file can be configed with different options
        * To figure out which options are available for a specific unit, use systemctl show 
        * systemctl show sshd (command shows all systemd options that be configd in the sshd.service unit 
        * Including their current default values 
        * Example 11-8 showing available options with systemctl show (pg 306)
        * When changing unit files to apply options, you need to make sure that the changes are written to /etc/systemd/system
        * Which is the location where custom unit files should be created
        * The recommended way to do so is to use the systemctl edit command 
        * This command creates a subdir in /etc/systemd/system for the service that you are editing 
        * for example, if you use systemctl edit sshd.service you get a dir with the name /etc/systemd/systemd/sshd.service.d in which a file with the name override.conf is created
        * All settings that are applied in the file overwrite any existing settings in the service file in /usr/lib/systemd/system
        * TIP: be default systemd uses the nano editor 
        * Not everybody likes that very much 
        * If you want vim to be used instead edit the /root/.bash_profile to include the following line:
        * export SYSTEMD_EDITOR="/bin/vim" and add this line to the ~/.bashrc file 
        * After you log in again, vim will be used as the default editor
        * If you would rather use /bin/vim as the default editor for all commands that need an external editor(including systemctl), you may also include export EDITOR="/bin/vim" instead 
    * Exercise 11-2 Changing unit config
        1. From a root shell - dnf -y install httpd (to install the apache web server package)
        1. systemctl cat httpd.service (to show the current config of the unit file that starts the Apache web server)
        1. systemctl show httpd.service (to get an overview of available config options for this unit file)
        1. export SYSTEMD_EDITOR=/bin/vim
            * to ensure you use vim as the default editor for the duration of this session
            * Optionally add this line to ~/.bashrc to make it persistent
        1. systemctl edit httpd.service to change the default config and add a [Service] section 
            * that includes the Restart=always
            * RestartSec=5s 
        1. Enter systemctl daemon-reload to ensure that systemd picks up the new config 
        1. systemctl start httpd (to start the httpd service)
            * system status sshd (verify that the sshd service is indeed running) should this be httpd?
        1. killall httpd (kill the httpd process)
        1. systemctl status httpd and then repeat after 5 seconds
            * You will notice that the httpd process get automatically restarted 
* Summary 
    * learned to work with systemd
    * manage systemd service state and how to change different option in systemd
    * Next chapter learn how to schedule tasks using the cron and at services
    * Exam prep tasks
* review all key topics 
    * Unit types in systemd
    * List three sections of a systemd unit file 
    * understanding systemd target units 
    * managing units with systemctl 
    * systemctl unit overview commands 
* Complete tables and list from memory 
* Define key terms 
    * systemd
    * unit
    * target
    * want
* Review questions 
* End of chapter lab


## Chapter 12 Scheduling Tasks

* The following topics are covered in this chapter 
    * Understanding task scheduling options in RHEL
    * Using systemd timers 
    * config cron automate recurring tasks
    * configing at to schedule future tasks
* The following RHCSA exam objective is covered in this chapter 
    * Schedule tasks using at and cron
* Scheduling tasks
    * On a linux server it is important that certain tasks run at certain times
    * This can be done by using the at and cron services
    * Which can be configured to run tasks in the future 
    * The at service is for executing future tasks once only
    * And the cron service is for executing recurring regular tasks
    * Apart from these services systemd is providing timer units that can be used as an alt
* Do do I know this already quiz 
    * Foundation topics section
        * understanding tasks scheduling options in RHEL
        * Using systemd timers
        * config cron to automate recurring tasks
        * config at to schedule future tasks
* Understanding tasks scheduling options in RHEL 
    * RHEL 9 offers different solutions for scheduling tasks
    * Systemd timer are now the default solution to ensure that specific tasks are started at specific moments
    * cron is the legacy scheduler service 
        * It is still supported and responsible for scheduling a few services 
    * st is used to schedule an occasional user job for future execution
* Using systemd timers 
    * Since its initial appearance in RHEL 7, systemd has been replacing many services 
    * Since the release of RHEL 9 it is also responsible for scheduling tasks
    * It is now the primary mechanism to do so 
    * Which means that if ever you are trying to find out how future tasks are executed you should consider systemd timers first 
    * A systemd timer is always used together with a service gile
    * And the names should match 
    * For example, the logroate.timer file is used to modify the logrotate.service file 
    * The service unit defines HOW the service should be started 
    * And the timer defines when it will be started 
    * If you need a service to be started by a timer, you enable the timer, not the service 
    * Example 12-1 Sample timer content (page 315)
    * To define how the timer should be started the timer unit contains a [Timer] section
    * Following three options in example 12-1 
        * OnCalendar: describes when the timer should execute
            * In this case it is set to daily which ensures daily execution
        * AccuracySec: Indicates a time window within which the timer should execute
            * Example 12-1 it is set to 1 hour 
            * If the timer needs to be executed at a more specific time
            * It is common to set it to a lower value 
            * Use 1us for the best accuracy
        * Persistent: A modifier to OnCalendar=daily, 
            * It specifies that the last execution time should be stored on disk 
            * So that the next time it executes is exactly one day later
    * In systemd timers, different options can be used to indicate when the related service should be started
    * Table 12-2 Timing Options in systemd timers (page 316)
        * OnActiveSec
            * defines a timer relative to the moment the timer is activated
        * OnBootSec
            * defines a timer relative to when the machine was booted
        * OnStartupSec
            * Specifies a time relative to when the service manager was started 
            * In most cases this is the same as OnBootSec, but not when systemd user units are used
        * OnUnitActiveSec
            * defines a timer relative to when the unit that the timer activates was last activated 
        * OnCalendar
            * defines timer based on calendar event expressions, such as daily
            * See man systemd.time for more details 
    * Exercise 12-1 Using systemd timers 
        1. systemctl list-units -t timer (to show a list of all timers)
        1. systemctl list-unit-files logrotate.* (which should show there is a logrotate.service and a logrotate.timer)
        1. systemctl cat logrotate.service (to verify the contents of the logrotate.service unit file)
            * Notice that it does not have an [Install] section
        1. systemctl status logrotate.service (which will show it marked as triggered by the logrotate.timer)
        1. install the sysstat package, using dnf install -y sysstat
        1. Verify the unit files that were added from this package
            * systemctl list-unit-files sysstat*
        1. systemctl cat sysstat-collect.timer (to show what the sysstat-collect timer is doing)
            * You will see the line OnCalendar=*:00/10 (*)
            * Which ensures that it will run every 10 minutes 
* Configuring cron to automate recurring tasks
    * task scheduling has been common on linux for a long time
    * And in the past the crond service was the primary tool to schedule tasks
    * The crond service consists of two major components
    * First is the cron daemon crond, which in RHEL 9 is also started as a systemd service 
    * This daemon looks every minute to see whether there is work to do 
    * Second this work to do is defined in the cron config
    * Which consists of multiple files working together to provide the right information to the right service at the right time
    * In this section you learn how to config cron
    * EXAM tip: even if systemd timers are now the default soluton for running recurring tasks, cron is still available 
    * Make sure you master both for purposes of preparing for the RHCSA exam
    * Managing the crond service 
        * The crond service is started by default on every RHEL system
        * Managing the crond service itself is easy 
        * it does not need much management
        * Where other service need to be reloaded or restarted to activate changes to their config 
        * This is not needed for crond
        * the crond daemon wakes up every minute and checks its config to see whether anything needs to be started
        * to monitor the current status of the crond service systemctl status crond 
        * Example 12-2 Monitoring the current state of the crond service (page 318) 
        * The most significant part of the output of the systemctl status crond command is the beginning 
        * Which indicates that the cron service is loaded and enabled 
        * The facts that the service is enabled means that it will automatically be started whenever this service is restarting
        * The last part of the command output shows current status information
        * Through the journald service, the systemctl command can find out what is actually happening to the crond service 
    * Understanding crom timing 
        * When scheduling services through cron you need to specify when exactly the services need to be started 
        * In the crontab config (which is explained in more depth in the next section) you use a time string to indicate when tasks should be started 
        * Table 12-3 cron time and date fields 
            * minute (0-59)
            * hour (0-23)
            * day of month (1-31)
            * month (1-12 (or month names))
            * day of week (0-7 (Sunday is 0 or 7), or day names)
        * In any of these fields you can use an * wildcard to refer to any value
        * Ranges of numbers are allowed as are lists and patterns
        * Some examples 
        * * 11 * * * (every minute between 11:00 and 11:59 - probably not what you want)
        * 0 11 * * 1-5 (Everyday at 11am on weekdays only)
        * 0 7-18 * * 1-5 (Every hour at the top of the hour between 7 am and 6 pm on weekdays)
        * 0 */2 2 12 5 (Every two hours on the hour on December 2 and every friday in December) (*)
        * TIP you don't need to remember all of this 
            * man 5 crontab shows all possible constructions 
    * Managing cron config files 
        * The main config file for cron is /etc/crontab
        * But you will not change this file directly 
        * It does give you a convenient overview tho of some time specifications that can be used in cron
        * It also set env variables that are used by the commands that are executed through cron
        * To make modifications to the cron jobs, there are other locations where cron jobs should be specified
        * Example 12-3 /etc/crontab sample content 
        * Instead of modifying /etc/crontab, different cron config files are used 
            * cron files in /etc/cron.d
            * Scripts in /etc/cron.hourly, cron.daily, cron.weekly, and cron.monthly
            * User-specific files that are created with crontab -e 
        * In this section you get an overview of these locations
        * NOTE: If you want to experiment with how cron works, you should allow for sufficient amount of time for the job to be executed 
            * the crond service reads it config every minute, after which new jobs can be scheduled for execution on the next minute 
            * So if you want to make sure you job is executed as fast as possible allow for a safe margin of three minutes between the moment you save the cron config and the execution time 
        * To start cron jobs can be started for specific users
        * to create a user specific cron job, type crontab -e after logging in as that user
        * Or as root type crontab -e -u username
        * These user specific cron jobs are the most common way for scheduling additional jobs through cron
        * When you are using crontab -e the default editor opens and creates a temp file 
        * After you edit the cron config the temp file is moved to its final location in the dir /var/spool/cron
        * In this dir a file is created for each user
        * These files should never be edited directly 
        * When the file is saved by crontab -e, it is activated automatically 
        * Whereas in the early days of RHEL the /etc/crontab file was modified directly, on RHEL 9 you do not have to do that anymore
        * If you want to add cron jobs, you add these to the /etc/cron.d dir
        * Just put a file in that dir (the exact name does not really matter)
        * and make sure that it meets the syntax of a typical cron job
        * example 12-4 Example cron jobs in /etc/cron.d
        * This example starts by setting env variables
        * These are the env variables that should be considered while running this specific job
        * On the last line the job itself is defined
        * The first part of this definition specifies when the job should run
        * In this case it will run 1 minute after each hour 
        * each day of the month, each month, and each day of the week
        * The job will be executed as the root user
        * The job itself involves the run parts command 
        * Which is responsible for running the scripted cron jobs in /etc/cron.hourly 
        * The last way to schedule cron jobs is through the following dirs 
            * /etc/cron.hourly
            * /etc/cron.daily
            * /etc/cron.weekly
            * /etc/cron.monthly
        * In these dirs you typically find scripts (not files that meet the crontab syntax requirements) that are put in there from RPM package files
        * When opening these scripts notice that no information is included about the time when the command should be executed 
        * The reason is that the exact time of execution does not really matter
        * The only thing that does matter is the job is launched once an hour, once a day, a week, or month
        * And anacron is taking care of everything else
    * Understanding the purpose of anacron
        * To ensure regular execution of the job, cron uses the anacron service 
        * This service takes care of starting the hourly, daily, weekly, and monthly cron jobs no matter at which exact time
        * to determine how this should be done, anacron uses the /etc/anacrontab file 
        * Example 12-5 shows the contents of the /etc/anacrontab file, which is used to specify how anacron jobs should be executed 
        * Example 12-5 anacrontab config (page 322)
        * In /etc/anacrontab the jobs to be executed are specified in lines that contain four fields, as shown in example 12-5
        * The first fields specifies the frequency of job execution, expressed in days 
        * The second field specifies how long anacron waits before executing the job
        * Which is followed by the third field that contains a job identifier
        * The fourth field specifies the command that should be executed 
        * TIP: Altho it is useful to know how anacron works, it typically is not a service that is configed directly
            * The need to config services through anacron is taken away by the /etc/cron.hourly, cron.daily, cron.weekly, and cron.monthly files
        * NOTE: It is not easy to get an overview of the cron jobs actually scheduled for execution
            * There is no single command that would show all currently scheduled cron jobs
            * crontab -l command does list cron jobs, but only for the current user account
    * Managing cron security
        * Be default all users can enter cron jobs
        * It is possible to limit which user is allowed to schedule cron jobs by using the /etc/cron.allow and /etc/cron.deny config files
        * If the cron.allow file exists, a user must be listed in it to be allowed to use cron
        * If the /etc/cron.deny file exists a user must not be listed in it to be allowed to set up cron jobs
        * Both files should not exist on the same system at the same time
        * Only root can use cron if neither file exist
    * Exercise 12-2 Running scheduled tasks through cron
        1. Open a root shell
            * cat /etc/crontab (to get an impression of the contents of the /etc/crontab config file
        1. crontab -e 
            * Opens an editor interface that by default uses vi as its editor
            * add the following line 
            * 0 2 * * 1-5 logger message from root 
        1. :wq! (to close out and write the editing session)
        1. cd /etc/cron.hourly
            * In this dir create a script file with the name eachhour that contains:
            * logger This message is written at $(date)
        1. chmod +x eachhour to make the script executable
            * If you fail to make it executable it will not work 
        1. Enter the dir /etc/cron.d and in this dir create a file with the name eachhour
            * Put the following contents in the file:
            * 11 * * * * root logger This message is written from /etc/cron.d
        1. Save the modifications to the config file and continue to the next section
            * (for optimal effect, perform step 8 after a couple of hours)
        1. After a couple of hours
            * grep written /var/log/messages 
            * Read the messages to verify correct cron operations
* Configuring at to schedule future tasks
    * To run a job through the atd service, you would use the at command
    * Followed by the time the job needs to be executed 
    * this can be a specific time, as in at 14:00 but it can also be a time indication like at teatime or at noon
    * After you type this, the at shell opens
    * From this shell you can type several commands that will be executed at the specific time that is mentioned
    * After entering the command press Ctrl-D to quit the at shell 
    * After scheduling jobs with at, you can use atq command (q for queue) to get an overview of all jobs currently scheduled 
    * It is also possible to remove current at jobs
    * to do this use atrm command (optionally followed by the number of the at job that you want to remove)
    * TIP: The batch command works like at, but it's a bit more sophisticated
        * when using batch you can specify that a job is started only when system performance parameters allow
        * typically, that is when system load is lower than .8
        * This value is a bit low on modern multi CPU systems, which is why the load value can be specified manually when starting atd, using the -l command line option
        * Use for instance atd -l 3.0 to make sure that no batch job is started when the system load is higher than 3.0 
    * Exercise 12-3 Scheduling jobs with at 
        1. systemctl status atd 
            * In the line that starts Loaded:, this command should show you that the service is currently loaded and enabled 
            * Which means that it is ready to start receiving jobs
        1. at 15:00 (or replace with any time near to the time at which you are working on this exercise)
        1. logger message from at
            * Press Ctrl-D to close the at shell 
        1. atq to verify that the job has indeed been scheduled 
* Summary 
    * In this chapter you learned how to schedule jobs for future execution
    * RHEL 9 provides three solutions to do so 
    * systemd timer have become the default solution
    * the legacy cron service is still around
    * and at can be used to schedule derred user tasks
* Exam prep tasks
* Review all key topics 
    * Timing options in systemd timers 
    * cron Time and Date fields 
    * crontab time indicators examples
    * Methods to enter crontab information
* Define key terms 
    * timer 
    * crond
    * anacron
    * at 
* Review questions
* End of chapter lab
* Lab 12-1

## Chapter 13 Configuring Logging 

* The following topics are covered in this chapter
    * understanding system logging
    * working with systemd-journald
    * config rsyslogd
    * rotatintg log files
* The following RHCSA exam objectives are covered in this chapter
    * Locate and interpret system log files and journals
    * preserve system journals 
* Configuring logging
    * Analyzing log files is an important system admin task
    * If anything goes wrong on a linux system the answer is often in the log files
    * On RHEL 9 two different log systems are used, and it is important to know which information can be found where
    * You learn how to read log files, 
    * How to config rsyslogd and journald
    * How to set up your system for log rotation so that you can prevent your disks from being completely filling up by services that are logging too enthusiastically
* Do I know this already quiz 
    * Foundation topic section
        * Understanding system logging
        * working with systemd-journald
        * configuring rsyslogd
        * rotating log files
* Understanding system logging 
    * Most services used on a linux server write information to log files
    * This info can be written to different destinations
    * And there are multiple sources to find the relevant information in system logs
    * No fewer than three different approaches can be used by services to write log information
    * Systemd-journald: With the introduction of systemd, the journald log service systemd-journald has been introduced also 
        * This service is tightly integrated with systemd which allows admins to read detailed info from the journal 
        * while monitoring service status using systemctl status command or journalctl command 
        * Systemd-journald is the default solution for logging in RHEL 9
    * Direct write: some services write logging information directly to the log files
        * Even some important services such as Apache web server and the samba file server
        * This approach to logging is not recommended
    * rsyslogd: rsyslogd is the enhancement of syslogd, a service that takes care of managing centralized log files 
        * syslogd has been around for a long time
        * Even if systemd-journald is no the default for logging
        * rsyslogd provides features not offered by systemd-journald
        * And for that reason it is still offered on RHEL 9
        * rsyslogd is still configed to work as it did in older versions of RHEL 
        * Which means that you can still use the log files it generates to get log information you need
    * Understanding the role of systemd-journald and rsyslogd 
        * On RHEL 9 systemd-journald provides an advanced log management system
        * It collects messages from the kernel
        * The entire boot procedures
        * And services and writes these messages to an event journal
        * This event journal is stored in a binary format and you can query it using journalctl command
        * The journalctl command enables you to access a deep level of detail about messages that are logged 
        * As it is a integrated part of Systemd and as such recieves all msg that have been generated by systemd units 
        * BC the journal that is written by systemd-journald is not persistent between reboots
        * messages are also forwarded to the rsyslogd service
        * Which writes the messages to different files in the /var/log dir
        * rsyslogd also offers features that do not exist in journald 
        * Such as centralized logging and filtering messages by using modules 
        * Numerous modeules are available to enhance rsyslog logging, such as output modeules that allow administratos to store messages in a database 
        * As rsyslogd advanced features are used alot, RHEL 9 still offers rsyslogd for logging as an addition to systemd-journald
        * Systemd-journald is tightly integrated with systemd
        * Therefor it logs everything your server is doing
        * rsyslogd adds some services to it 
        * In particular it takes care of writing log information to specific files (that will be persistent between reboots)
        * It allows you to config remote logging and log servers 
        * Apart from rsyslog and systemd-journald, there is the audit service 
        * This service provides auditing an indepth trace of what specific services, processes, or users have been doing
        * Config of auditing is beyond the scope of RHCSA exam but you will noteice that SELinux for instance logs detailed messages to the auditd service 
        * To get more information about what has been happening on a machine running RHEL, admins have to take three approaches 
            * Jornalctl command to get more detailed info from the journal 
            * Systemctl status <unit> command to get a short overview of the most recent significant events taht have been logged by systemd units thru systemd-journald
            * This command shows teh status of services, as well as teh most recent log entries that have been written
            * Monitor the files in /var/log that are written by rsyslogd
        * Example 13-1 using systemctl status to show relevant log information
    * Reading log files 
        * Apart from the messages that are written by systemd-journald to the journal and which can be read using the journalctl command 
        * Linux systems also have different log files in the dir /var/log 
        * Most the files in this dir are managed by rsyslogd
        * But some are created directly by specific services 
        * You can read these files by using a pager utility such as less 
        * The exact number of files in the /var/log dir will change 
        * Depending on the config of a server and the services that are running on that server 
        * Some files, however, do exist on most occasions, and as an admin, you should know which files they are and what content can be expected in these files 
    * Table 13-2 System Log files overview 
        * /var/log/messages
            * This is the most commonly used log file 
            * It is the generic log file where most messages are written to 
        * /var/log/dmesg 
            * Contains kernel log messages 
        * /var/log/secure 
            * Contains auth related messages 
            * Look here to see which authentication errors have occured on a server 
        * /var/log/boot.log 
            * Contains messages that are related to system startup 
        * /var/log/audit/audit.log 
            * contains audit messages 
            * SELinux writes to this file 
        * /var/log/maillog
            * contains mail related messages 
        * /var/log/httpd/
            * Contains log files that are written by the Apache web server (if it is installed)
            * Notice that apache writes messages to these files directly and not through rsyslog 
    * Understanding log file contents 
        * As an admin you need to be able to interpret the contents of log files 
        * Example 13-2 shows partial content from the /var/log/messages file (page 334)
        * As you can see in example 13-2 each line that is logged has specific elements 
            * Date and time: every log message starts with a timestamp
            * For filtering purposes, the timestamp is written as military time
            * Host: The host the message originated from
            * This is releveant because rsyslogd can be configd to handle remote logging as well 
            * Service or process name and PID: The name of the service or process that generated the message 
            * Message content: The content of the message, which contains the exact message that has been logged 
        * To read the content of a log file, you can use a pager utility, like less, or you can live monitor what is happening in the log file as described in the next section
    * Live log file monitoring 
        * When you are configuring service on linux it might be useful to see in real time what is happening
        * You could open two terminal sessions at the same time
        * One terminal session config and test the service 
        * In the other terminal session, you can see in real time what is happening
        * The tail -f <logfile> command shows in real time which lines are added to the log file 
        * When you are monitoring a log file with tail -f, the trace remains open until you press Ctrl-C to close it 
    * Using logger
        * Most services write information to the log files all by themselves or through rsyslogd
        * the logger command enables users to write messages to rsyslo from the command line or script 
        * Just type logger, followed by the message you want to write to the logs
        * The logger utility, in this way, offers a convenient solution to write messages from scipts 
        * this allow you to have a script write to syslog if something goes wrong
        * When using logger, you can also specify the priority and facility to log to 
        * the command logger -p kern.err hello (write hello to the kernel facility, for example, using the error priority (priority and facility are discussed in more detail later in this chapter))
        * This option enables you to test the working of specific rsyslog facilities 
    * Exercise 13-1 Using live log monitoring and logger 
        1. Open a root shell 
        1. From the root shell, type tail -f /var/log/messages
        1. Open a second terminal window 
            * In this terminal window, type su - student to open a subshell as user student
        1. su - to open a root shell but enter the wrong password 
        1. Look at the file /var/log/messages
            * You see an error message was logged here
        1. From the student shell type logger hello
            * You will see the message appearing in the /var/log/messages file in real time
        1. In the tail -f terminal, press Ctrl-C to stop tracing teh message file 
        1. tail -20 /var/log/secure
            * This shows the last 20 lines in /var/log/secure 
            * Which also shows the messages that su - password errors have generated previously 
* Working with systemd-journald 
    * The systemd-journald service stores log messages in the journal, a binary file that is temp stored in the file /run/log/journal 
    * This file can be examined using the jounralctl command 
    * Using journalctl to find events 
        * The easiest way to use journalctl is by just typing the command 
        * It shows that recent events have been written to the journal since your server last started 
        * The result of this command is shown in the less pager 
        * ANd by default you will see the beginning of the journal 
        * BC the journal is written from the moment your server boots 
        * The start of the output shows boot related log messages 
        * If you want to see the last messages that have been logged you can use journalctl -f 
        * Which shows the last lines of the messages where nog log lines are automatically added 
        * You can also type journalctl and use (uppercase) G to go to the end of the journal 
        * ALso note that the search option / and ? work in the journalctl output
        * Example 13-3 watching log information generated by systemd-journald (pg 336)
        * What makes journalctl a flexible command is that its many filtering options allow you to show exactly what you need 
    * Exercise 13-2 Discovering journalctl 
        1. journalctl 
            * You will see the content of the journal since your server last started 
            * Starting at the beginning of the journal 
            * The content is shown in less you can use common less commands to walk through the file 
        1. q (to quit the pager)
            * Now type journalctl --no-pager 
            * This shows the contents of the journal without using a pager 
        1. journalctl -f 
            * This opens the live view mode of journalctl 
            * Which allows you to see new messages scrolling by in real time
            * Ctrl-C to interrupt 
        1. journalctl (press spacebar, and then press Tab key twice)
            * When prompted to view all possibilities type y and then press enter key 
            * This shows specific options that can be used for filtering 
            * Type for instance journalctl_UID=1000 to show messages that have been logged for your student user account 
        1. journalctl -n 20 
            * The -n 20 option displays the last 20 lines of the journal (just like tail -n 20)
        1. journalctl -p err (this command shows errors only)
        1. If you want to view journal messages that have been written in a specific time period 
            * you can use the --since and --until commands 
            * Both options take the time parameter in the format YYYY-MM-DD hh:mm:ss 
            * Also you can use yesterday, today, and tomorrow as parameters 
            * So type journalctl --since yesterday to show all messages that have been written since yesterday 
        1. journalctl allows you to combine different options as well 
            * So if you want to show all messages with a priority error that have been written since yesterday use journalctl --since yesterday -p err
        1. If you need as much detail as possible, use journalctl -o verbose 
            * This show different options that are used when writing to the journal (see example 13-4)
            * all these options can be used to tell the journalctl command which specific information you are looking for 
            * Type for instance journalctl _SYSTEMD_UNIT=sshd.service to show more information about the sshd system unit (_)
        1. journalctl -dmesg (this shows kernel-related messages only)
            * Not many people use this command as the dmesg command gives the exact same result 
    * Using journalctl to find events cont
        * In the preceding exercise you typed journalctl -o verbose to show verbose output 
        * Example 13-4 shows an example of the verbose output 
        * As you can see this provides detailed information for all items that have been logged, including the PID, the ID of the associated user and group account, the command that is associated, and more 
        * This verbose information may help you in debugging specific systemd units 
    * Example 13-4 Showing detailed log information with journalctl -o verbose (pg 338)
        * There are some more interesting options to use with journalctl command 
        * The -b optionshows a boot log, which incldues just the messages that were generated while booting 
        * -x option adds explanation to the info that is shown
        * This explanation makes it easier to interpret specific messages 
        * You should be able to consider the -u option
            * which allows you to see messages that haave been logged for specific systemd unit only
        * journalctl -u sshd (to see all messages that have been logged for the sshd service)
    * Table 13-3 Most useful journalctl options (page 339)
        * -f 
            * Shows the bottom of the journal and live adds new messages that are generated 
        * -b
            * shows the boot log 
        * -x
            * adds additional explanation to the logged items 
        * -u 
            * used to filter log messages for a specific unit only 
        * -p
            * allows for filtering of messages with a specific priority 
    * Preserving the systemd journal 
        * By default the journal is stored in the file /run/log/journal
        * The entire /run dir is used for current process status information only 
        * Which means that the journal is cleared when the system reboots 
        * To make the journal persistent between system restarts you should create a directory /var/log/journal 
        * Storing the journal permanently requires the storage=auto parameter in /etc/systemd/journald.conf which is set by default
        * This parameter can have different values 
        * Storage=auto
            * The journal will be written on disk if the directory /var/log/journal exists 
        * Storage=volatile 
            * The journal will be stored only in the /run/log/journal dir
        * Storage=persistent 
            * The journnal will be stored on disk in the dir /var/log/jounral
            * This dir will be created automatically if its doesn't exist
        * Storage=none
            * No data will be stored but forwarding to other targets such as the kernel log buffer or syslog will still work 
        * Even when the journal is written to the permanent file in /var/log/journal that does not meant he journal is kept forever
        * The journal has built in log rotation that will be used monthly 
        * Also the journal is limited to a max size of 10 percent of the size of the file system that is on
        * And it will stop growing if less than 15 percent of the file system is still free 
        * If that happens the oldest messages from the journal are dropped automatically to make room for newer messages 
        * To change these settings you can modify the file /etc/systemd/journald.conf
        * Example 13-5 Setting journald paramters thru /etc/systemd/journald.conf page 340
        * Making the systemd journal parmanent is not hard to do 
        * Exercise 13-3 making the systemd journal persistent pg 341
            1. open a root shell and type mkdir /var/log/journal 
            1. Before journald can write the journal to this dir, you have to set ownership 
            * chown root:systemd-journal /var/log/journal (followed by chmod 2755 /var/log/journal)
            1. systemctl restart systemd-journal-flush (to reload the new systemd journald parameters)
            1. The systemd journal is now persistent across reboots
* Configuring rsyslogd
    * To make sure the information that needs to be logged is written to the location where you want to find it
    * You can config the rsyslogd service thru the /etc/rsyslog.conf file and optional drop in files in /etc/rsyslog.d
    * In the /etc/rsyslog.conf file you find different sections taht allow you to specify where and how information should be written
    * Understanding rsyslogd config files 
        * Like many other services in RHEL the config for rsyslogd is not defined in just one config file 
        * The /etc/rsyslog.conf file is the central location where rsyslogd is configd
        * From this file the content of the dir /etc/rsyslog.d is included 
        * The dir can be populated by installing RPM packages on a server 
        * When looking for specific log config, make sure to always consider the contents of this dir also 
    * Understanding rsyslog.conf sections 
        * The rsyslog.conf file is sued to specify what should be logged and where it should be logged 
        * to do this you will find different sections in the rsyslog.conf file 
        * #### MODULES #### 
            * rsyslogd is modular
            * Modules are included to enhance the supported features in rsyslogd
        * #### GLOBAL DIRECTIVES ####
            * This section is used to specify global parameters, such as the location where auxiliary files are written or the default timestamp format
        * #### RULES ####
            * This is the most important part of the rsyslog.conf file
            * It contains the rules that specify what information should be logged to which destination
    * Understanding facilities, priorities, and log destinations 
        * To specify what information should be logged to which destination, rsyslogd uses facilities, priorities, and destinations
        * a facility specifies a category of information that is logged 
            * rsyslogd uses a fixed list of facilities, which cannot be extended 
            * This is because of backward compatibility with the legacy syslog service 
        * A priority is used to define the severity of the message that needs to be logged 
            * When you specify a priority, by default all messages with that priority and all higher priorities are logged 
        * A destination defines where the message should be written
            * Typical destinations are files
            * But rsyslog modules can be used as a destination as well 
            * To allow further processing through a rsyslogd module 
        * Example 13-6 The RULES section in rsyslog.conf page 342
        * When you specify a destination, a file is often used 
        * If the filename starts with a hyphen (as in -/var/log/maillog)
        * The log messages will not be immediately committed to the file buyt instead will be buffered to make writes more efficient
        * Device files can also be used such as /dev/console
        * If this device is used, messages are written in real time to the console 
        * On modern servers, this often does not make sense, bc admins often log in remotely and do not see what is happening on the server console 
    * Table 13-4 rsyslogd Facilities 
        * auth/authpriv
            * messages related to authentication
        * cron 
            * messages generated by the crond service 
        * daemon
            * generic facility that can be used for nonspecified daemons
        * kern
            * kernel messages 
        * lpr
            * messages generated thru the legacy lpd print system
        * mail 
            * email related messages 
        * mark 
            * special facility that can be used to write a marker periodically 
        * news 
            * messages generated by the NNTP news system
        * security
            * Same as auth/authpriv
            * Should not be used anymore
        * syslog
            * messages generated by the syslog system
        * user
            * messages generated by the syslog system
        * uucp
            * messages generated by the legacy UUCP system
        * local0-7
            * messages generated by services that are configd by any of the local0 thru local7 facilities 
    * Understanding facilities, priorities, and log destinations cont
        * The syslog facilities were defined in the 1980s 
        * And to guarantee backward compatibility, no new facilities can be added 
        * The result is that some facilities still exist that basically serve no purpose anymore
        * And some services that have become relevant at a later stage do not have their own facility 
        * As a solution two specific facility types can be used
        * The daemon facility is a generic facility that can be used by any daemon
        * In addition the local0 thru local7 facilities can be used 
        * if services that do not have their own rsyslogd facility need to write log messages to a specific log file anyway
        * These services can be configd to use any of the local0 thru local7 facilities 
        * You next have to config the services to use these facilities as well 
        * The procedure you follow to do that is specific to the service you are using 
        * Then you need to add a rule to the rsyslog.conf file to send msg that come in thru that facility to a specific log file 
        * To determine which types of messages should be logged you can use different severities in rsyslog.conf lines
        * These severities are the syslog priorities
    * table 13-5 rsyslogd priorities 
        * debug 
            * debug messages that will give as much information as possible about service operation
        * info 
            * Informational messages about normal service operations
        * notice 
            * informational msgs about items that might become an issue later 
        * warning (warn)
            * Something is suboptimal, but there is no real error yet 
        * error (err)
            * a noncritical error has occurred
        * crit 
            * a critical error has occurred
        * alert
            * messages used when the availability of the service is about to be discontinued
        * emerg (panic)
            * message generated when the availability of the service is dicontinued 
    * Understanding facilities, priorities, and log destinations cont
        * When a specific priority is used, all messages with that priority and higher are logged according to the specifications used in that specific rule
        * If you need to config logging in a detailed way
        * Where messages with different priorities are sent to different files, you can specify the priority with an equal sign (=) in front of it 
        * as in the following line which will write all cron messages with only the debug priority to a specific file with the name /var/log/cron.debug
        * cron.=debug -/var/log/cron.debug
        * The - in front of the line specifies to buffer writes so that information is logged in a more efficient way 
        * TIP 
            * You don't need to learn the names of rsyslogd and priorities by heart 
            * They are all listed in man 5 rsyslog.conf
            * On the exam you have access to the man pages, so this information will be easily accessible 
    * Exercise 13-4 Changing rsyslog.conf rules 
        1. By default the Apache service does not log thru rsyslog but keeps its own logging
            * You are going to change that 
            * To start install apache service (dnf install -y httpd)
        1. After installing the apache service, open its config file /etc/httpd/conf/httpd.conf
            * And verify it has the following line:
            * ErrorLog syslog:local1
        1. systemctl restart httpd 
        1. create a line in the /etc/rsyslog.conf file that will send all messages that it receives for facility local1 
            * which is now used by the httpd service to the file /var/log/httpd-error.log
            * To do this include the following line in the #### RULES #### section of the file 
            * local1.error /var/log/httpd-error.log
        1. Tell rsyslogd to reload its config by using systemctl restart rsyslog 
        1. All apache error messages will now be written to the httpd-error.log file 
        1. from the firefox browser go to localhost/index.html
            * Because no index.html page exists yet, this will be written to the error log 
        1. Create a snap-in file that logs debug messages to a specific file as well 
            * To do this, type echo "*.debug /var/log/messages-debug" /etc/rsyslog.d/debug.conf (*)
        1. again restart rsyslog using systemctl restart rsyslog 
        1. Use the command tail -f /var/log/messages-debug to open a trace on the newly created file
        1. From a second terminal type logger -p daemon.debug "Daemon Debug Message"
            * You will see the debug message passing by 
        1. Ctrl-C to close the debug log file 
* Rotating Log files 
    * To prevent syslog messages from filling up your system completely you can rotate the log messages 
    * That means that when a certain threshold has been reached the old log file is closed and new log file is opened
    * the logrotate utility is started periodically to take care of rotating log files 
    * When a log file is rotated the old log file is typically copied to a file that has sthe rotation date in it 
    * So if /var/log/messages is rotated on June 8, 2023 the rotated filename will be /var/log/messages-20230608
    * As a default four old log files are kept on the system
    * Files older than that period are removed from the system automatically 
    * WARNING: Log files that have been rotated are not stored anywhere; they are just gone 
        * if your company policy requires you to be able to access information about events that have happened more than five weeks ago, for example 
        * You should either back up log files or config a centralized log server where logrotate keeps rotated messages for a significantly longer period 
    * The default settings for log rotation are kept in the file /etc/logrotate.conf
    * Example 13-7 /etc/logrotate.conf sample content (page 339)
    * The most significant settings used in this config file tell logrotate to rotate files on a weekly basis and keep four old versions of the file 
    * You can obtain more information about other parameters in this file through the man logrotate command 
    * If specific files need specific settings you can create a config file for that file in /etc/logrotate.d 
    * the settings for that specific file overwrite the default settings in /etc/logrotate.conf
    * You will find that different files exist in this dir already to take care of some of the config files 
* Summary 
    * In this chapter you learned how to config logging 
    * Read how the rsyslogd and journald services are used on RHEL to keep log information and you learned how to manage logs that are written by these services 
    * You also learned how to config log rotation and make the journal persistent 
    * Exam prep tasks 
* Review all key topics 
    * Systemd-journald explanation 
    * rsyslogd explanation 
    * system log files overview 
    * most useful journalctl options
    * making the systemd journal persistent
    * rsyslogd facilities 
    * rsyslogd priorities 
* Complete tables and lists from memory 
* Define key terms 
    * systemd-jounralctl 
    * rsyslogd
    * journalctl 
    * log rotation
    * facility 
    * priority
    * destination
* Review questions 
* Lab 13.1 


## Chapter 14 Managing storage 

* The following topics are covered in this chapter 
    * understanding MBR and GPT partitions
    * Managing partitions and file systems
    * Mounting file systems
* The following RHCSA exam objectives are covered in this chapter 
    * List, create, delete, partitions on MBR and GPT disks
    * Config systems to mount file systems at boot by universally unique ID (UUID) or label
    * Add new paritions and logical volumes, and swap to a system non destructively 
    * Create, mount, unmount, and use vfat, ext4, and xfs file systems
* Managing storage 
    * Working with storage is an important task for a linux admin
    * first set of essential storage skills 
    * Learn how to create and manage partitions, format them with the file system you need to use, and mount these file systems 
    * Do I know this already quiz 
    * Foundation topic sections
        * understanding MBR and GPT partitions 
        * Managing partitions and file systems 
        * Mounting file systems 
* Understanding MBR and GPT partitions 
    * To use a hard drive it needs partitions
    * Some OS install everything to one partition, while other OS such as Linux normally have several partitons on one hard drive
    * Using more than one partition on a system makes sense for multiple reasons 
        * It is easier to distinguish between different types of data 
        * Specific mount options can be used to enhance security or performance 
        * It is easier to create a backup strategy where only relevant portions of the OS are backed up
        * If one partition accidentally fills up completely the other partitions are still usable and your system might not crash immediately 
    * NOTE: Instead of using multiple different partitions you can also use LVM logical volumes or Stratis file systems 
        * Managing logical volumes and Stratis file systems is covered in Chapter 15, Managing advanced storage 
    * On recent RHEL two different partitioning schemes are available 
    * Before creating your first partition you should understand these schemes 
    * Understanding the MBR partitioning scheme
        * When the personal computer was invented in the early 1980s a system was needed to define hard disk layout 
        * This system became known as the master boot record (MBR) partitioning scheme
        * Whiling booting a computer the basic input/output system (BIOS) was loaded to access hardware devices 
        * From the BIOS the bootable disk device was read, and on this bootable device, the MBR was allocated 
        * The MBR contains all that is needed to start a computer, including a boot loader and a parition table 
        * When hard disks first came out for PCs in the early 1980s users could have different OSs on them 
        * Some of these included MS-DOS/PC-DOS,PC/IX (IBMs UNIX for 8086 PCs), CPM86, and MPM86
        * The disk would be partitioned in such a way that each OS installed got a part of the disk 
        * One of the partitions would be made active meaning the code in the boot sector in the MBR would read the first section of that active partition and run the code 
        * That code would load the rest of the OS 
        * This explains why four partitions were deeemed "enough"
        * The MBR was defined as teh 1st 512 bytes on a comp hard drive 
        * and in the MBR an OS boot loader was present as well as a partition table 
        * the size used for the partition table was relatively small just 64 bytes
        * with the result that in the MBR no more than 4 partitions could be created 
        * Since partition size data was stored in 32 bit values and a default sector size of 512 bytes was used
        * The max size size that could be used by a partition was limited to 2 TiB (hardly a problem in the early 1980s)
        * In the MBR, just 4 partitions could be created 
        * B/C many PC OSs needed more than 4 partitions a solution was found to go beyond the number of four
        * In the MBR one partition could be created as an extended partition
        * As opposed to the other partitions that were created as primary partitions
        * Within the extended parition multiple logical paritions could be created to reach a total number of 15 paritions that could be addressed by the linux kernel 
    * Understanding the need for GPT partitions 
        * Current Comps hard drives have become too big to be addressed by MBR partitions 
        * That is one of the main reasons why a new partition scheme was needed 
        * This paritionsing scheme is the GUID parition table (GPT)
        * Con comps that are using the new Unified Extensible Firmware Interface (UEFI) as a replacement for the old BIOs systems
        * GPT partitions are the only way to address disks 
        * Also older comp systems that are using BIOs instead of UEFI can be configed with globally unique ID (GUID) partitions
        * Which is necessary if a disk with a size bigger than 2 TiB needs to be addressed 
        * Using GUID offers many benefits 
            * The max partitions size is 8 zebibyte (ZiB) which is 1024 x 1024 x 1024 x 1024 gibibytes 
            * In GPT up to a max number of 128 partitions can be created 
            * The 2-TiB limit no longer exists 
            * Because space that is available to store paritions is much bigger than 64 bytes which was used in MBR there is no longer a need to distinguish between primary extended and logical partitons
            * GPT uses a 128 bit GUID to ID paritions 
            * A backup copy of the GUID partition table is created by default at the end of the disk, which eliminates the single point of failure that exists on MBR partition tables 
    * Understanding Storage measurement units 
        * When talking about storage we use different measurement units 
        * In some cases units like megabytes (MB) are used 
        * In some cases units like mebibyte (MiB) are used 
        * The difference between these two is that a megabyte is a multiple of 1000, and a mebibtye is a multiple of 1024 
        * In computers it makes sense to talk about multiples of 1024 b/c that is  how computers address items 
        * However confusion was created when hardware vendors a long time ago started referring to megabytes instead of mebibytes 
        * In the early days of computing the difference was not important 
        * the difference between a kilobyte (KB) and a kibibyte (KiB) is just 24 bytes
        * The bigger the numbers grow, the bigger the difference becomes 
        * A gigabyte for instace is 1000x1000x1000 bytes, or 1000000000 bytes
        * Whereas a gibibyte is 1024x1024x1024 which makes a total of 1073741824 bytes which is over 70 MB larger than 1 GB
        * On current linux distros the binary numbers (MiB, no MB) have become the standard 
        * IN the past KB, MB, and so on were used both in decimal and binary situations 
        * Sometimes they were even mixed 
        * For example 1-Mbps line speed is one million bits per second 
        * The once famous "1.44 MB" floppy disk was really 1440000 bytes in size (80 tracks x 2 heads x 9 sectors x 512 byte sectors)
        * Creating a mixed meaning of MB: 1.44 X (decimal K) x (binary K)
    * Table 14-2 disk size specifications 
        * KB | kilobyte | 1000^1 | KiB | Kibibyte | 1024^1 
        * MB | Megabyte | 1000^2 | MiB | Mebibyte | 1024^2 
        * GB | Gigabyte | 1000^3 | GiB | Gibibyte | 1024^3 
        * TB | Terabyte | 1000^4 | TiB | Tebibyte | 1024^4 
        * PB | Petabyte | 1000^5 | PiB | Pebibyte | 1024^5
        * EB | Exabyte | 1000^6 | EiB | Exbibyte | 1024^6
        * ZB | Zettabyte | 1000^7 | ZiB | Zebibyte | 1024^7
        * YB | Yottabyte | 1000^8 | YiB | Yobibyte | 1024^8
* Managing partitions and file systems 
    * As discussed in the previous section, two different types of partitions can be used on RHEL 
    * To match the different partition types, there are also two different partitioning utilities 
    * The fdisk utility has been around for a long time and can be used to create and manage MBR as well as GPT partitions 
    * The gdisk utility is used to create GPT partitions 
    * IN this section you will learn how to use both 
    * Apart from fdisk and gdisk there are other partitioning utilities as well of which parted is probably the most important 
    * Some people like it as it is relatively easy to use, but at the same time it hides some of the more advanced features 
    * For that reason this chapter focuses on working with fdisk and gdisk and introduces parted only briefly 
    * For both MBR and GPT partitions you need to specify the name of the disk device as an argument 
    * Use the lsblk command to print a list of all disk devices available on your system 
    * Table 14-3 Common disk device types 
        * /dev/sda 
            * A hard disk that used SCSI driver 
            * Used for SCSI and SATA disk devices 
            * Common on physical servers but also in VMware virtual machines 
        * /dev/nvme0n1 
            * The first hard disk on a NVM express (NVMe) interface 
            * NVMe is a server grade method to address advanced SSD devices 
            * Note at the end of the device name that the first disk in this case is referred to as n1 instead of a (as is common with the other types)
        * /dev/hda 
            * The (legacy) IDE disk device type 
            * You will seldom see this device type on modern computer 
        * /dev/vda
            * A disk in a KVM VM that uses the virtio disk driver 
            * This is the common disk device type of KVM VM 
        * /dev/xvda
            * A disk in a xen VM that uses the Xen virtual disk driver 
            * You see this when installing RHEL as a VM in Xen virtualization
            * RHEL 9 cannot be used as a Xen hypervisor, but you might see RHEL 9 VM on top of the Xen hypervisor using these disk types 
    * Naming for for disk devices 
        * First disk found on the server /dev/sda (second being /dev/sdb)
        * And so on and so forth 
* Creating MBR partitions with fdisk 
    * Exercise 14-1 Creating MBR partitions with fdisk 
        * This exercise has been written to use an installation of RHEL that contains an unused disk 
        * You can easily add a second disk to your env 
        * This can be a virtual disk that is added through your virt program
        * Or a USB flash drive if you are working on a physical installation
        * In that case make sure to replace the device names in this exercise with the device names that match your hardware 
        1. Open a root shell and type lsblk (this lists the block devices that are available)
        1. Open a root shell and run the fdisk command 
            * This command needs as its arg the name of the disk device where you want to create the partition
            * This exercise used /dev/sdb
            * Change that if needed according to your hardware 
            * fdisk /dev/sda (command)
        1. Before you do anything it is a good idea to chekc how much disk space you have available 
            * Press p to see an overview of current disk allocation
            * In the output of this command, in particular look for the total number of sectors and the last sector that is currently used 
            * If the last partition does not end on the last sector you have available space to create a new partition
            * In this case, that shouldn't be an issue b/c you are supposed to use a new disk in this exercise 
        1. type n to add a new partition
        1. Press p to create a primary partition
            * Accept the partition number that is now suggested which should be /dev/sdb1 
        1. Specify the first sector on disk that new partition will start on
            * The first available sector is suggested by default, so press enter to accept 
        1. Type +1G to make this a 1-GiB partition
            * If you were to just press enter, the last sector available on disk would be suggested 
            * If you were to use that after this exercise you would not have any disk space left to create additional partitions or logical volumes, so you should use another last sector 
            * To use another last sector, you can do one of the follow 
            * Enter the number of the last sector you want to use 
            * Enter +number to create a partition that sizes a specific number of sectors 
            * Enter +number(K,M,G) to specify the size you want to assign to the partition in KiB, MiB, and GiB
            * After you enter the partition's ending boundary, fdisk will show a confirmation
        1. At this point you can define the partition type 
            * By default a linux partition type is used 
            * If you want the partition to be of any other partition type, use t to change it 
            * For this exercise there is no need to change the partition type 
            * Common partition types include the following: 
            * 82: Linux Swap 
            * 83: Linux
            * 8e: Linux LVM
        1. If you are happy with the modifications, press w to write them to disk and exit fdisk 
        1. Type lsblk to verify that the new partition has been created successfully 
* Using extended and logical partitions on MBR 
    * In the previous procedure you learned how to add a primary partition 
    * If three MBR partitions have been created already, there is room for one more primary partition, after which the partition table is completely filled up 
    * If you want to go beyond four partitions on a MBR disk you have to create an extended partition
    * Following that, you can create logical partitions within the extended partition
    * Using logical partitions does allow you to go beyond the limitation of four partitions in the MBR; there is a disadvantage as well, tho
    * All logical partitions exists within the extended partition
    * If something goes wrong with the extended partitions you have a problem with all logical partitions existing within it as well 
    * If you need more than four separate storage allocation units you might be better off using LVM instead of logical partitions 
    * If you are on a completely new disk, you might just want to create GPT partitions instead 
    * NOTE 
        * An extended partition is used only for the purpose of creating logical partitions 
        * You cannot create file system directly on an extended partition 
    * Excercise 14-2 Creating logical partitions 
        1. In a root shell, type fdisk /dev/sdb to open the fdisk interface 
        1. Type n to create a new partition
            * To create a logical partition, when fdisk prompts which partition type you want to create, enter e 
            * This allows you to create an extended partition, which is necessary to later add logical partitions
        1. pg 379

