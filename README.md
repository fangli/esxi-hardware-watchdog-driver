# esxi-hardware-watchdog-driver

This is an ESXi VIB package for hardware watchdog heartbeating and timeout resetting.

Requirement
===========

* Designed to work with ESXi >= 5.x, 6.x etc., *tested in ESXi6.5*
* You can see the Watchdog timer configurations in BIOS, something like "Enable/Disable", "Expire Time", "Actions" etc
* IPMI is supported by the motherboard
* The motherboard have a hardware watchdog timer

Install
=======

1. Download and copy vib to ESXi host
2. Run following command in ESXi SSH
3. Reboot

```bash
# esxcli software vib install -v /full/path/to/esxi-hardware-watchdog.vib -f
```

Uninstall
=========

```bash
# esxcli software vib remove -n hardware-watchdog
```

Is it working correctly?
========================

Search for keyword `hardware-watchdog` in /var/log/syslog.log


How it works?
=============

I made it as simple as possible. Basically, this VIB adds a startup script, which runs command `/bin/ipmitool_wd mc watchdog reset` every 60 seconds in ESXi host.

Warning
=======

This vib has a community acceptance level.

This VIB is supported by community and no one takes responsibility for any damage. If you found a bug in this driver, DO NOT try to get support from vmware, use Github Issue instead. I'm happy to work with you.

`ipmitool_wd` is the common ipmitool binary, I just use `ipmitool_wd` for filename conflict avoidance, just in case. The binary in this repo is grabbed from https://github.com/hobbsh/static-ipmitool , **IF YOU USE IT IN PRODUCTION, YOU MAY WANT TO BUILD YOUR OWN STATIC LINKED VERSION FROM SOURCE CODE FOR 100% TRUST AND RELIABILITY**
