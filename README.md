# ncupgrade

This Bash script creates a backup and performs an upgrade of a local Nextcloud installation based on the [Nextcloud documentation for manual upgrades](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst).  

**In any case: use at own risk!**  

## Requirements

- local Nextcloud installation  
- packages `curl`, `sudo` and `gnupg`  
- the script needs to be run with root privileges or as webserver user (in this case the webserver obviously can't be stopped during upgrade)
- if you want to stop the webserver during upgrade process (like recommended in the documentation), notice:  
-- the script needs then to be run with root privilege  
-- the script uses a `systemctl` call to stop and start the webserver  
-- use option `-sw WEBSERVER` and replace WEBSERVER with the service name of your webserver  

## Quick Guide

1. Clone the repository to your server and enter the repo:  
`git clone https://github.com/BernieO/ncupgrade`  
`cd ncupgrade`  

2. Run the script with root privileges and following arguments:  
- the path to your Nextcloud installation (must be first argument)  
- option -sw and your webservers service name (to stop and start the webserver during upgrade)  
- for example: `./ncupgrade /path/to/nextcloud -sw nginx`  

3. Check the output of the script carefully for errors. For troubleshooting [check this out](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst#troubleshooting)  
The script creates a backup of Nextclouds directory which may be used for restoring the previous version.  

4. Login to your Nextcloud webinterface and reenable all compatible 3rd party apps.  

For further upgrades steps 1-3 may be omitted.  

## Advanced

All options need to be specified as command line arguments. It is mandatory to pass as very first argument the path to your Nextcloud instance. Find detailed description of all available options below.

## Options

```
Usage: ./calcardbackup [DIRECTORY] [option [argument]] [option [argument]] [option [argument]] ...

Arguments in capital letters to options are mandatory.
Paths (FILE / DIRECTORY) are absolute paths or relative paths to working directory.

-bd | --backup-directory DIRECTORY
       Use directory DIRECTORY to store backups.
       If this option is not given, folder 'nextcloud_backups/' in script's directory is created and used.
-sw | --stop-webserver WEBSERVER
       Stop webserver during upgrade. This is recommended by the documentation, because clients might behave
       unexpectedly, if they don't get a proper maintenance response due to missing/wrong endpoints during upgrade
-z | --zip
       use zip to compress backup folder instead of creating a gzipped tarball (tar.gz)
```
