# Why
Piratpartiet has two servers running Varnish and keeping them both in sync started to get cumbersome. A quick search on Google gave nothing, so I wrote this script to ease the maintenance of activating new configurations on a Varnish farm.

# Dependencies
This script uses:

* bash
* rsync
* varnishadm

# How the script works:

- The directory holding the varnish configuration will be synced to all hosts in $HOSTS using ssh as carrier
- The currently active configuration on all hosts get cached in case something goes awry this configuration will get activated again
- All hosts will get the new configuration loaded. If you pass an argument that name will be used + the current date and time
- The configuration will be activated on all hosts, if an error occurs all hosts that managed to get the new configuration activated will get their configurations reverted to the old configuration.

# Configuration
The script has a couple of configuration variables at the top which most should be standard.

- `HOSTS` - In between the () a hostname separated by a space
- `VARNISH_PATH` - The location of your configuration folder
- `VARNISH_VCL` - Your main VCL-file
- `ADMIN_PORT` - The port used for the Varnish console
- `RSYNC_PARAMS` - The parameters used for rsync
- `RSYNC_USER` - The account that has access to the configuration folder, needs to exist on all hosts in your farm
- `VARNISHADM_PARAMS` - Any parameters passed to varnishadm, `-S /etc/varnish/secret` comes to mind. :)

I guess this configuration should really go into `/etc/default/varnish` instead, any takes on this?