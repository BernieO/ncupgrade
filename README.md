# ncupgrade

This Bash script performs an upgrade of a local Nextcloud installation based on the [Nextcloud documentation for manual upgrades](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst#upgrade-manually)  
**Use at own risk!**  

## Requirements

- local Nextcloud installation  
- package `curl` 
- this script needs to be run as root, because the webserver needs to be stopped and restarted  

## Quick Guide

1. Clone the repository to your server and enter the repo: 
`git clone https://github.com/BernieO/ncupgrade` 
`cd ncupgrade`  

2. Copy the example configuration file in the same directory as the script:  
`cp examples/ncupgrade.conf.example ncupgrade.conf`  

3. Edit the configuration file and adjust values to your needs:  
`nano ncupgrade.conf`  

4. Login to your Nextcloud Webinterface and disable all 3rd party apps.  

5. Unless Nextcloud uses a SQLite3 database it is strongly recommended to make a dump of the database before running this script. For MySQL/MariaDB a dump can be created with (password for USERNAME will be prompted):  
`mysqldump -u USERNAME -p --lock-tables --all-databases > databasedump.sql`  

6. Run the script with `./ncupgrade` and enter the version you want to upgrade your nextcloud installation to. Or enter alternatively "latest" to upgrade to the latest available stable version.  

7. Check the output of the script for errors. For troubleshooting [check this out](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst#troubleshooting)  

8. Login to your Nextcloud webinterface and reenable all compatible 3rd party apps. 

For further upgrades steps 1-3 can be omitted.
