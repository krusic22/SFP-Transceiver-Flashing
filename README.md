# SFP Programming
---
This repository holds scripts that can be used for reading and writing data to and from SFP modules.

They've been tested to work on a **Raspberry Pi Zero W**, others might work but are untested (feedback is appreciated).


# Contributing
---
Look at the planned additions. Working on any of them is a great start. Currently no code quality standard is set, so trash is most likely to be accepted. Please mark additions with **[ADD]**. 

# Planned additions
---
| State        | Function                        |
|------------- | ------------------------------- |
|✅            | Basic reading and writing       |
|❌            | Automatic dump formatting       |
|❌            | Dump analysts                   |
|❌            | Dump editor + checksum corrector|
|❌            | Compatibility database          |
|❌            | Health monitor                  |
|❌            | User writable data modifier     |
|❌            | Wiki about modules and mods     |

# Contributing Dumps
---
Dumps are always welcome, even if you just find a random module in the trash.
Dumps should look something like this:
```bash
#Module: HP 1Gb SFP RJ-45 Module
#Tested on: HP ProCurve
#Monitoring: No
#Unlocked: No, hardware mod required.
03
04
FF
```

# Q&A
**Can I dump module data with other devices too?**

Yes you can. On Cisco hardware you can use ``sh idprom int (interface) detail``.
On HP ProCurve you can use the **debug mode** to dump and write data to modules ``edomtset`` (press enter) ``edomtset`` (press enter) ``XCVRI2CREAD (port) 0x0 0xA0 128``.

**You said that we can write data using ProCurve switches, how?**

Enter the debug mode as described above. Make sure to backup the module and that the switch isn't doing anything important as it could crash. Personal recommendation is also to use SSH instead of the Console port then doing this, as some characters can crash or disrupt the serial device. Do **NO MORE** then 10 commands at the time, as any additional commands might get lost due to how the switch software works.
Example: 
```
<command> <port> <location> <table> <data>
XCVRI2CWRITE 52 0x00 0xA0 0x03
XCVRI2CWRITE 52 0x01 0xA0 0x04
```
