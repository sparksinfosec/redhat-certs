# Red Hat Cerified Engineer Ansible Automation Study guide 

* First book before the student workbook 
* Explore hands on labs for red hat ansible automation platform (page 4 in the book)

## Book Notes 

### Preface 

* Who should read this book 
* Why we wrote this book
* Navigating this book 
    * chapter 1 
        * gives an overview of the topics covered in the exam and discusses the benefits of certification
    * chapter 2 
        * provides an intro to ansible, including basic concepts and lays the groundwork for the rest of the book 
    * chapter 3 
        * introduces ansible playbooks, and walks through how to run your first playbook 
    * chapter 4 
        * focuses on how ansible manages hosts and how to organize the target automation against them 
    * Chapter 5 
        * looks at flow control and examines how to influence the execution of automation activities 
    * Chapter 6 
        * looks at how to manipulate files in ansible including basic operations and templating 
    * chapter 7
        * deep dive into ansible modules and how to develop a new module
    * Chapter 8 
        * covers how to organize ansible content using roles and collections, their purpose and how to enable you to package and share ansible content with others 
    * Chapter 9 
        * introductes ansible execution environments as a method for running ansible automation, the challenges they solve and how they can be created 
    * Chapter 10 
        * covers how to effectively manage systems using ansible and look at management related activies including filesystem management and security considerations 
* Conventions used in this book 
* Using code examples 

### Chapter 1 Exam details and resources 

* Why should you be certified
* Ex294 prerequisites 

### Chapter 2 Introduction to Ansible 

* Ansible is an automation tool for managing your infra elements such as cloud virtual or bare metal servers, network, and app config
* Like other autoation tools ansible uses a code first approach to describe the state of your infra
    * so you can expect the same results every time you run it 
* Ansible focuses on three important topics to make it the perfect tool for your IT operations 
    * ansible provides instructions to automate operations 
    * ansible provides config management 
    * ansible lets you automate the deployment of your app into the infra 
* Ansible overview 
    * Why ansible 
        * Due to complexity of infra, managing resources manually is simply not an option anymore 
        * Changes applied manually can introduce errors with unintended consequences 
        * Automation is key to maintaing complexy under control?
        * Ansible lets you store your infra as code, making it maintainable and reproducible every time
        * How does ansible work to communicate with nodes and execute operations against them? 
    * Ansible nodes 
        * Push out approach 
        * instructions are transmitted from a central location to each of the managed instances (or hosts)
        * this approach allows the remote (or managed) machines need no specialized software (or agent) to be installed
        * ansible is considered to be an agentless technology 
        * This approach keeps nodes more performant, as no extra software needs to be installed 
        * Also eliminates an vector attack from the node (more secure)
        * Also supports a pull approach but this is not the default and will not be covered?
        * When you start using ansible your first set up a control node 
        * Usually a local machine where you will install ansible and store all the instructions to push to the managed nodes 
        * The control node connects to each of the different managed nodes and applies all the instructions defined for each case for example
            * installing system packages
            * copying some files from the control to the managed nodes
            * adding users
        * communication occurs over the network (usually but not always) over ssh making all these interactions secure
        * What are these instructions and executing instructions against the managed nodes?
    * Ansible modules 
        * Ansible connects to managed nodes and pushes out small programs called modules 
        * Implements the logic to execute against the node 
        * Once ansible is connected to the nodes 
            * it transfers the modules required by your instructions to the remote node(s) for execution
            * Then these modules are executed
            * Ansible removes them when it finishes 
        * Ansible comes with a set of built in modules that provide support for most of the common tasks that you will need 
        * However you can also source modules from external sources or create custom modules of your own to extend the capabilities provides by ansible 
        * Modules are typically written using python or powershell when target windows instances 
        * preparing local machine 
    * Installing and running ansible 
        * Different set of requirements for control nodes and managed nodes 
            * Control nodes can be installed on an unix machine with python 3.9 or later installed 
            * As well as on windows machines using WSL installed 
        * managed nodes allow for additional flexibility 
            * python 2 or 3 are supported 
    * Installing ansible 
        * There are three options for installing ansible on a control node 
            * install the release with the OS package manager (yum, dnf, apt)
            * Install with pip (python package manager)
            * install from source or tarbell
        * sudo dnf install ansible 
            * pip is the perfered way for MacOS
        * sudo dnf install ansible-navigator ansible-core ansible-builder ansible-runner ansible-sdk
        * ansible-core is the only one I could find 
        * ansible --version
    * remote machine setup
        * Ansible only needs to be installed into the control node 
        * Remote machine have two minimal requirements 
            * access to the hsot using ssh 
            * python2 (version 2.7 or later) or python3 (version 3.5 or later)
        * Remote machine might be a VM, cloud VM, or a physical machine in a data center
            * start up two vms 
        * host and guest machines 
            * Host and guest 
                * Host - the physical machine where you install the OS that manages the comp
                * Guest - the VM machine that is installed, executed, and hosted on the host physical machine
        * oracle vm virtual box
    * Cleaning up 
    * Core Ansible components 
        * Important to understand the four core compoents of Ansible: inventories, CLIs, hosts, and config options 
        * Hosts 
            * Two kinds of hosts in ansible 
                * control hosts and managed hosts 
                * Control host is where the ansible CLI is executed 
                * This can be your local machine
                * CI/CD server machine
                * A container
                * or any host that can execute ansible 
                * Managed hosts (also referred to as nodes)
                    * target devices (servers, network appliances, or any computer you want to config with ansible)
            * The ansible inventory file defines all the managed hosts and groups of managed hosts to run automation tasks
            * b/c nodes are associated to one or more groups within inventories, you can run commands (and playbooks) against specific hosts and/or groups
            * Makes applying a change to multiple hosts eaiser than applying the change host by host
            * for example
               * if you have three nodes (classified under the backend group
               * you can install a particular piece of software such as java, with a single command instead of repeating it individually against each host
            * Inventory files are written in either INI or YAML format
               * most common format is INI
               * Host are defined by their DNS names, hostname, or IP
            * Two IPs
               * 192.168.1.92
               * 192.168.1.93
               * No group is defined
               * all hosts are ungrouped
               * Even tho no group is defined explicitly, ansible implicitly creates two groups
                  * all and ungrouped
               * The all group contains every host defined in the inventory file, groped or not
               * The ungrouped group contains all hosts that do not have another group besides all (both host fall in this category from the above example)
               * same example in the YAML file below
                  * ungrouped:
                     * hosts:
                        * 192.168.1.92:
                        * 192.168.1.92:
               * side bar
                  * default location for the anisble inventory is /etc/ansible/hosts
                  * If you set host there you are setting the inventory globally and it is not necessary to specify the inventory file location using -i option
                  * You can override the default ansible inventory file location by setting the new location in the ANSIBLE_INVENTORY env variable or within an ansible.cfg file
         * Groups
            * Assume that the 192.168.1.92 host ia a web server and the 102.168.1.93 host is a DB server
            * You will probably need to apply different commands in each instance
            * So group them so they are IDd in the inventory file
            * To create a group, set a new INI section with the group's name in the file
            * An INI section is defined on a line in square brackets ([ and ]) with the section's name between brackets
            * INI
               * [webserver]
               * 192.168.1.92
               * [dbservers]
               * 192.168.1.93
            * equivalent inventory in YAML format is shown in the following snippet
               * webservers:
                  * hosts:
                     * 192.168.1.82
               * dbserver:
                  * hosts:
                     * 192.168.1.93
            * You can set more than one host in each group
            * You can put the same host in more than one group
            * group names should follow the variable name format
            * Summary, variable name can only include letters, numbers or underscores
            * Python keywords or playbooks keywords are not valid variable names
            * variable names cannot begin with a number
         * Adding variables to inventory
            * page 39
