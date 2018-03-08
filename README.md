# ncupgrade

This Bash script creates a backup and performs an upgrade of a local Nextcloud installation based on the [Nextcloud documentation for manual upgrades](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst).  

**In any case: use at own risk!**  

## Requirements

- local Nextcloud installation  
- packages `curl`, `sudo` and `gnupg`  
- this script needs to be run as `root`, because the webserver needs to be stopped and restarted  

## Quick Guide

1. Clone the repository to your server and enter the repo:  
`git clone https://github.com/BernieO/ncupgrade`  
`cd ncupgrade`  

2. Run the script with following arguments:  
-  the path to your Nextcloud installation (must be first argument)  
- option -sw and your webservers service name (to stop and start the webserver during upgrade)  
`./ncupgrade /path/to/nextcloud -sw nginx`  

3. Check the output of the script carefully for errors. For troubleshooting [check this out](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst#troubleshooting)  
The script creates a backup of Nextclouds directory which may be used for restoring the previous version.  

4. Login to your Nextcloud webinterface and reenable all compatible 3rd party apps.  

For further upgrades steps 1-3 may be omitted.  
