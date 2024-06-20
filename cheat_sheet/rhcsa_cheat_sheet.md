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
* VI basic (pretty versed with vi already)
    *
