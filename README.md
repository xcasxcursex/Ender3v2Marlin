# Auto-built Creality Ender 3 V2 Latest Firmware


For people too poor or stupid to just pay a few bucks to this dude: https://marlin.crc.id.au/firmware/Ender%203%20V2%20-%20Stock/



Based on https://github.com/frealmyr/marlin-build


Using configuration examples from:

https://github.com/xorn/custom_ender3_v2_bltouch

https://www.chepclub.com/ender-3-v2-firmware.html

https://marlin.crc.id.au/faq/Ender%203%20V2/#hybrid


## Changes from Marlin stock Ender 3 V2 configuration:
- Extrusion
  - Adds G10 / G11 Firmware based retraction (Use M207, M208, M209 to configure)
  - Adds M600 - Filament Change
  - Adds M603 - Set Filament Load / Unload length
  - Adds M701 - Load Filament
  - Adds M702 - Unload Filament
  - Nozzle Parking enabled
- Motion
  - Adds G2 / G3 - Arc support
  - S-Curve Acceleration enabled
  - Junction Deviation enabled \ Jerk disabled
- Hardware Support
  - Bed set to 235 x 235 - As per Creality spec
  - SDIO Support enabled - Faster SD card access
  - Advanced OK enabled - Comms performance improvement to clients eg. OctoPrint
  - TMC Hybrid Threshold enabled - Stepper driver tweak, will provide more torque at the expense of more noise, when motor reaches high speeds
  - Uses hardware EEPROM, not emulated on SD Card - Better performance accessing storage
