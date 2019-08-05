﻿# Sysmon Threat Intelligence Configuration #
Peronal fork from ion-storm

See the develop Branch for more bleeding edge updates: https://github.com/ion-storm/sysmon-config/tree/develop

This config is based off of the OR logic in sysmon 8.00 and 8.04, sysmon 8.02 breaks this functionality.  Also 8.00 introduced a memory leak that will consume all available memory on your system if you frequently reload the config file.  Upgrading to 8.04 is mandatory.

This is a Microsoft Sysinternals Sysmon configuration file template with default high-quality event tracing.

The file provided should function as a great starting point for system monitoring in a self-contained package. This configuration and results should give you a good idea of what's possible for Sysmon.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**[sysmonconfig-export.xml](https://github.com/ion-storm/sysmon-config/blob/master/sysmonconfig-export.xml)**

Because virtually every line is commented and sections are marked with explanations, it should also function as a tutorial for Sysmon and a guide to critical monitoring areas in Windows systems. It demonstrates a lot of what I wish I knew when I began with Sysmon in 2014.

Pull requests and issue tickets are welcome, and new additions will be credited in-line or on Git.

Note: Exact syntax and filtering choices are deliberate to catch appropriate entries and to have as little performance impact as possible. Sysmon's filtering abilities are different than the built-in Windows auditing features, so often a different approach is taken than the normal static listing of every possible important area.

This now has an Auto Updater script to update to the latest Sysmon config hourly.  This is great for mass deployments without having to manually update thousands of systems.

## Use ##

### Auto-Install with Auto Update Script:###
~~~~
Install Sysmon.bat
~~~~

### Install ###
Run with administrator rights
~~~~
sysmon.exe -accepteula -i sysmonconfig-export.xml
~~~~

### Update existing configuration ###
Run with administrator rights
~~~~
sysmon.exe -c sysmonconfig-export.xml
~~~~

### Uninstall ###
Run with administrator rights
~~~~
sysmon.exe -u
~~~~

## Hide Sysmon from services.msc ##
~~~~
Hide:
sc sdset Sysmon D:(D;;DCLCWPDTSD;;;IU)(D;;DCLCWPDTSD;;;SU)(D;;DCLCWPDTSD;;;BA)(A;;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)
Restore:
sc sdset Sysmon D:(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)

~~~~

### Graylog Configuration ###

(https://github.com/ion-storm/Graylog_Sysmon)
