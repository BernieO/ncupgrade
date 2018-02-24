# ncupgrade

This Bash script creates a backup and performs an upgrade of a local Nextcloud installation based on the [Nextcloud documentation for manual upgrades](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst).
It may also be used to migrate from ownCloud to Nextcloud. In this case you need to make sure to [follow a valid migration path](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/migrating_owncloud.rst).  

**In any case: use at own risk!**  

## Requirements

- local Nextcloud installation  
- packages `curl`, `sudo` and `gnupg`  
- this script needs to be run as `root`, because the webserver needs to be stopped and restarted  

## Quick Guide

1. Clone the repository to your server and enter the repo:  
`git clone https://github.com/BernieO/ncupgrade`  
`cd ncupgrade`  

2. Copy the example configuration file in the same directory as the script:  
`cp examples/ncupgrade.conf.example ncupgrade.conf`  

3. Edit the configuration file and adjust values to your needs:  
`nano ncupgrade.conf`  

4. Run the script with `./ncupgrade` and enter the version you want to upgrade your nextcloud installation to. Or enter alternatively "latest" to upgrade to the latest available stable version.  

5. Check the output of the script carefully for errors. For troubleshooting [check this out](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst#troubleshooting)  
The script creates a backup of Nextclouds directory which may be used for restoring the previous version.  

6. Login to your Nextcloud webinterface and reenable all compatible 3rd party apps. 

For further upgrades steps 1-3 may be omitted.
