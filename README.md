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
  - Re-enabled thermocouple minimum - Fire safety (Disables the heater when the temp sensor acts broken)


### Jerk vs JD, SCurve vs LA ... Fight!

Two pairs of features exist, which are mutually exclusive from one another - choices must be made: Jerk vs Junction Deviation and S-Curve Acceleration vs Linear Advance
So, what are they, how good are they? This will decide for us:


#### Jerk vs Junction Deviation

Jerk: Jumps to full speed if it's close enough already. 
Provides a constant, when change in speed is below this no acceleration will be applied - it will just 'jerk' to full speed. Smaller numbers make acceleration start to happen at smaller changes in speed.
Has the effect of reducing ringing when number is lower because it makes acceleration occur which reduces vibration from sudden changes in speed.
Has the effect of slowing print times because the printer reaches full speed less often due to more time in acceleration phase.

JD: Slows down for corners, slower for sharper turns. 
Provides a constant which adjusts tightness of corners. Smaller numbers make more acceleration occur on the same corner.
Has the effect of reducing ringing when number is tuned corretly because it makes acceleration occur (always) which reduces vibration from sudden changes in speed.
Does not slow print times as algorithm ensures same average speed across the movement.

Junction Deviation is the default in Marlin, but some users have concerns that it may be negatively impacting print quality or times. Of course, others disagree, so in attempt to make an objective decision by analyzing the algorithms, explanation by devs, etc, I have no doubt that this feature can and should be superior to its redundant counterpart - and no question as to why Marlin devs made it the default. I do expect some effort will be required to appropriately tune the deviation, acceleration and speed settings, but the same can be said of jerk.

JD wins. 

See here for in-depth discussion: https://github.com/MarlinFirmware/Marlin/issues/11672
And here: https://github.com/synthetos/TinyG/wiki/Jerk-Controlled-Motion-Explained


#### S-Curve vs Linear Advance

S-Curve Acceleration: Smooths out movement.
Provides acceleration curves applied to all movement which ensure no sudden jolts.
Has the effect of reducing ringing because it makes acceleration occur which reduces vibration from sudden changes in speed.
Free quality limited only by the torque of your steppers.


Linear Advance: More accurate extrusion.
Modulates filament flow with relation to print speed.
Has the effect of improving print quality because it prevents (partial) over- and under-extrusion resulting from changes in speed.
Has the effect of allowing faster printing due to more accurate extrusion.

Sadly, these two features do not yet play nicely together. Since the S-Curve effects ALL axes, that means extrusion, too. Having the two features both managing feed rates is crossing the beams.
An experimental option is present, which allows both to be used simultaneously, but I'm confident that it wouldn't be marked as "experimental" by the devs, if they were fully confident in it. So, we have to choose.

The benefits of each feature are well known and accepted, so choosing "which is best?" is too hard. A "which is least worst?" approach will do. The only real argument against either of them is that Linear Advance may be less effective in a Bowden setup. So, if I have to choose one to ditch, it's LA....but, there are also arguments that bowden setups benefit the most from LA.

Really, I can't decide. So I'm going with the experimental option for now, and enable both.
