# ncupgrade

This Bash script upgrades a local Nextcloud installation based on the [Nextcloud documentation for manual upgrades](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst).  
Before the upgrade a backup of the running Nextcloud instance will be created [(also based on the official documentation)](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/backup.rst) before upgrading.  

**In any case: use at own risk!**  

## Requirements

- local Nextcloud installation  
- packages `curl`, `sudo` and `gnupg`  
- the script needs to be run with root privileges or as webserver user (in this case the webserver obviously can't be stopped during upgrade)
- if you want to stop the webserver during upgrade process (like recommended in the documentation), notice:  
-- the script needs then to be run with root privilege  
-- the script uses a `systemctl` call to stop and start the webserver  
-- use option `-w WEBSERVER` and replace WEBSERVER with the service name of your webserver  

## Quick Guide

1. Clone the repository to your server and enter the repo:  
`git clone https://github.com/BernieO/ncupgrade`  
`cd ncupgrade`  

2. Run the script with root privileges and following arguments:  
- the path to your Nextcloud installation (must be first argument)  
- option -w and your webservers service name (to stop and start the webserver during upgrade)  
- for example: `sudo ./ncupgrade /path/to/nextcloud -w nginx`  

3. Check the output of the script carefully for errors. For troubleshooting [check this out](https://github.com/nextcloud/documentation/blob/master/admin_manual/maintenance/manual_upgrade.rst#troubleshooting)  
The script creates a backup of Nextclouds directory which may be used for restoring the previous version.  

4. Login to your Nextcloud webinterface and reenable all compatible 3rd party apps.  

## Advanced

All options need to be specified as command line arguments. It is mandatory to pass as very first argument the path to your Nextcloud instance as well as passing option `-w WEBSERVER` or `-k` to the script. Find detailed description of all available options below.

## Options

```
Usage: ./ncupgrade [DIRECTORY] [option [argument]] [option [argument]] [option [argument]] ...

Arguments in capital letters to options are mandatory.
Paths (FILE / DIRECTORY) are absolute paths or relative paths to working directory.

-bd | --backup-directory DIRECTORY
       Use directory DIRECTORY to store backups.
       If this option is not given, folder 'nextcloud_backups/' in script's directory is created and used.
-h  | --help
       Print version number and a short help text
-k  | --keep-webserver-running
       Don't stop webserver during upgrade. Though the Nextcloud ducumentation recommends to stop the webserver
       during upgrade, this might not always be possible (for example in shared hosting environments or if other
       webservices running on the same webserver need to stay online).   
       Either this option or -w WEBSERVER need to be passed to the script.
-w | --webserver WEBSERVER
       Stop service WEBSERVER during upgrade with systemctl.
       This is recommended in the Nextcloud documentation, because clients might behave
       unexpectedly, if they don't get a proper maintenance response due to missing/wrong endpoints during upgrade.
       Note that the script has to be run with root privileges to stop and start the webserver.
       Either this option or -k need to be passed to the script.
-z  | --zip
       use zip to compress backup folder instead of creating a gzipped tarball (tar.gz)
```
