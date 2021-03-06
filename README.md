# Magic Charging Switch (cs)
# VR25 @ XDA Developers


**Description**
- Stop charging at a set % level below 100 to extend battery lifespan.
- Notes: this is a terminal program & your terminal emulator app must be excluded from battery optimization &/or Doze for cs to work properly. You don't need to keep your screen ON, nor the terminal running in foreground. Due to a shell limitation, the "stop charging mechanism" may be late by at least 1% battery level -- it's not a big deal, though.

**Disclaimer**
- Don't quote me on the above. Do your own research on lithium-ion batteries! This module tweaks low level Android settings -- I shall not be held responsible for any nuclear disaster potentially triggered by the use/misuse of it.


**Usage**
- cs % % --> pause charging at first %; resume charging if battery drops below second % (optional)
- cs --help --> self-explanatory
- cs -d [timeout (optional)] --> disable charging
- cs -e [timeout (optional)] --> enable charging
- cs -i --> show battery info
- cs debug --> gather debugging data & save it to /sdcard as cs_debug*
- just "cs" --> run cs with previous settings


**Tips/Notes**

"cs 80" --> stop charging at 80%.

"cs 80 20" --> pause charging at 80%; resume if battery drops below 20%.

"-d" & "-e" options can take a "timeout" argument to automatically enable & disable charging, respectively (i.e., "cs -d 30m" --> keep charging disabled for 30 minutes, "cs -e 1h" --> charge for 1 hour).

"cs -e 120 && cs -d 30m && cs -e 1h" --> charge for 120 seconds, pause for 30 minutes, then charge again for 1h.

"cs -e 30m && cs -d 30m && cs 90" --> charge for 30 minutes, pause for 30 minutes, then charge again, but this time until battery level is greater or equal to 90%.

Ideally, you want your battery level between 40-60% - best, 20-80% - average, 10-90% - fair.

cs auto-generates a Tasker project XML file for automation every time a `cs %` or `cs % %` command is executed. The user has to disable "Beginner Mode" in Tasker settings, then import the project "cs_tasker".

Charging control file and its parameters can be specified in /sdcard/cs_ctrl.txt (you have to create the file). The format is "switch /path/to/ctrl/file ON OFF" -- where ON OFF may be 1 0, enable disable, enabled disabled, etc. (device-dependent).

Examples:
- `switch s=/sys/module/pm8921_charger/parameters/disabled 0 1`
- `switch s="/sys/devices/platform/7000c400.i2c/i2c-1/1-006b/charging_state" enabled disabled`


**Online Support**
- [Battery University](http://batteryuniversity.com/learn/article/how_to_prolong_lithium_based_batteries)
- [GitHub Repo](https://github.com/Magisk-Modules-Repo/Magic-Charging-Switch)
- [XDA Thread](https://forum.xda-developers.com/apps/magisk/module-magic-charging-switch-cs-v2017-9-t3668427)
