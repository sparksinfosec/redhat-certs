# Config files dedicated study

## Config files

* Bash 
    * source ~/.bashrc (reload the bashrc file after changes)
    * /etc/profile (generic bash startup file containing all system settings that are processed in a login shell)
    * /etc/bashrc (processed while opening a subshell)
    * ~/.bashrc (user specific version of /etc/bashrc)
    * ~/.bash_profile (user specific /etc/profile)
    * /etc/profile.d (drop in files)
    * /etc/skel (files that are copied to user home dir upon creation)
* /etc/hosts (setting up hostname resolution globally)
    * IP_address hostname (set up for hostname in the file)
* User files
    * /etc/passwd
    * /etc/shadow
    * /etc/sudoers
        * visduo
        * %whell ALL=(ALL) ALL
        * lisa ALL=/bin/mount /dev/sdb, /bin/umount /dev/sdb
        * %users ALL=/usr/bin/passwd, ! /usr/bin/passwd root
        * /etc/sudoers.d/linda (drop in)
* /usr/share/doc (additional man page info)
* GRUB
    * /etc/default/grub
    * grub2-mkconfig -o /boot/grub2/grub.cfg 
    * grub2-mkconfig -o /boot/efi/EFI/redhat/grub.cfg
* Tuning 
    * /etc/tuned/tuned-main.conf
    * Custom tuned profiles 
        * /etc/tuned
        * each profile has to have a tuned.conf
        * /etc/tuned/myprofile/tuned.conf
            * tuned-adm profile myprofile (set custom profile called myprofile)
    * sysctl 
        * /etc/sysctl.d/*.conf (*)(.conf is required)
* Journald
    * /etc/systemd/journald.conf 
    * /var/log/journal
    * rsyslog 
        * /etc/rsyslog.conf
    * logrotate
        * /etc/logrotate.conf
* Autofs
    * /etc/auto.master
        * /nfsdata /etc/auto.nfsdata
    * /etc/auto.nfsdata
        * files -rw nfsserver:/nfsdata
    * wildcard 
        * /etc/auto.master
            * /homes /etc/auto.homes
        * /etc/auto.homes 
            * * -rw nfsserver:/home/ldap/&
* cron
    * /etc/crontab (main config)
    * /etc/cron.d (drop in)
    * /etc/cron.{hourly,daily,weekly,monthly} (drop in for scripts that need to be scheduled on a regular basis)
        * make sure execute bit is set
* anacron
    * /etc/anacron (config)
* NTP chronyd
    * /etc/chrony.conf (specify sync parameters)
* REPOS
    * /etc/yum.repos.d/
* Subscription manager (likely not needed)
    * /etc/pki/product (indicates the instaled RHEL products)
    * /etc/pki/consumer (IDs teh RH account for registration)
    * /etc/pki/entitlment (indicates which subscription is attached)
* Network manager 
    * /etc/NetworkManager/system-connections
    * /etc/sysconfig/network-scripts/ (legacy files still support but deprecated)
* hostname and DNS
    * /etc/hosts 
    * /etc/resulv.conf (DNS resolution
        * nameserver IP_address
    * /etc/nsswitch.conf (determines order of hostname resolution)
* User defaults 
    * /etc/default/useradd (applies to useradd only)
    * /etc/login.def (system wide - important options like password aging)
* SSH config 
    * /etc/ssh/sshd_config (server daemon config)
    * /etc/ssh/ssh_config (client config)
    * ~/.ssh/config (user specific config 
        * Host bare_metal_server
            * Hostname 1.2.3.4
            * port 22 (optional)
            * User steve
        * Make sure its 600 for the config file chmod 600
    * ~/.ssh/
        * authorized_keys 
        * known_hosts
        * public and private keys 
* SELinux 
    * /etc/sysconfig/selinux (default state of SELinux)
* Containers
    * /etc/container/registries.conf (registry access config fils)
    * ~/.config/containers/registries.conf (user specific config)
    * ~/.config/systemd/user (create systemd files for automatic containers)
    * /etc/systemd/system (rootless automatic containers)
    



## Man Pages

* man 7 regex (regex helpful resource)
* man test (for test conditional bash)
* man logrotate (logrotate great examples)
* man ssh_config 
* man pages for selinux-policy-doc
* man semanage-fcontext
* man semanage-port
* man podman-generate-systemd
* man podman-generate
