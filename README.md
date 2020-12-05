Auto-built Creality Ender 3 V2 Latest Firmware


For people too poor or stupid to just pay a few bucks to this dude: https://marlin.crc.id.au/firmware/Ender%203%20V2%20-%20Stock/


Based on https://github.com/frealmyr/marlin-build


Using configuration examples from:

https://github.com/xorn/custom_ender3_v2_bltouch

https://www.chepclub.com/ender-3-v2-firmware.html


Changes from Marlin stock Ender 3 V2 configuration:

 - Bed set to 235 x 235
 - Adds G2 / G3 Arc support
 - Adds G10 / G11 Firmware based retraction (Use M207, M208, M209 to configure)
 - Adds M600 - Filament Change
 - Adds M603 - Set Filament Load / Unload length
 - Adds M701 - Load Filament
 - Adds M702 - Unload Filament
 - Enabled Advanced OK
 - Enabled CLASSIC_JERK (actually stock)
 - Enabled S_CURVE_ACCELERATION
 - Enabled Smart Filament Runout Sensor (Add M412 S0 in your Start G-Code if you do not have a filament sensor).
 - Uses hardware EEPROM, not emulated on SD Card. (also stock)
