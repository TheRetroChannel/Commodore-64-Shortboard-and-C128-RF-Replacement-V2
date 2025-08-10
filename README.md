## This project has been superseded by the [RFOFF](https://www.tindie.com/products/36736/) and no further updates or support will be provided. You are welcome to build this RF replacement but I would highly recommend the RFOFF which provides a much better output.

![Board](https://github.com/TheRetroChannel/Commodore-64-Shortboard-and-C128-RF-Replacement-V2/blob/main/images/RF%20V2%20SB128.jpg)

The RF modulator in the C64/128 handles amplification and filtering for all video signals (including the ones on the C64 DIN connector). Unfortunately it does a very poor job and this is even more apparent with modern displays and upscalers, even CRTs with their inherent softening can reveal issues with the original RF modulator. One way to signifcantly improve the video output is to replace the RF modulator with a more modern and finely tuned solution, and why not add a few quality of life features while were at it.

This is an RF modulator replacement (RF delete) for the shortboard Commodore 64 ASSY 250469 and Commodore 128

For ASSY KU-14194HB, 250407, 250425 and 250466 see [C64 Longboard RF replacement V2](https://github.com/TheRetroChannel/Commdore-64-RF-replacement-Longboard-V2). 

Note ASSY 326298 is not compatible with either of these RF modulator replacements but there are some [simple mods](https://youtu.be/agDFLPP9yIw) that can improve the video output of this revision.

A YouTube build and installation video is available [HERE](https://youtu.be/t5yx6tAaMuE)

## Feature summary
* Superior video output compared to the original RF modulator
* Direct S-Video output for S-Video capable displays and upscalers
* Adjustable luma:sync ratio (contrast control)
* Signal passthrough to the C64/128 AV DIN - for those who prefer to use the standard DIN connector
* 3.5mm stereo audio output with the left channel dedicated to SID audio, and right channel selectable between SID audio (dual mono), composite video, and external (for dual SID setups, LumaCode, etc.)
* Optional C128 jailbar filter

## Changes from V1
* Component values tweaked and extra filters added - even better video output
* Added support for LumaCode
* Added direct composite output via 3.5mm jack
* Added contrast control - something Commodore should have done
* Removed composite enable header and trimmer - no longer required thanks to point 1
* Removed direct luma/chroma connections - no longer required thanks to point 1
* Removed adjustable luma chroma pots - no longer required thanks to point 1
* Removed hard reset circuit - did anyone even use it?
* Better routing (slightly less pretty) and solid ground plane on bottom layer
* Board dimensions tweaked for better fitment

## Comparison shots

![64 comparison](https://github.com/TheRetroChannel/Commodore-64-Shortboard-and-C128-RF-Replacement-V2/blob/main/images/COMPARISONS%20250407%20PAL.png)
 
## Gathering components
The easiest way to order PCBs is through the shared project page on PCBWay.

**For C64C, Commodore 128D (plastic case) and 128 flat use [this link](https://www.pcbway.com/project/shareproject/Commodore_128_and_C64_Shortboard_RF_Modulator_Replacement_V2_c93a9d28.html)**

**For Commodore 128DCR (metal case) use [this link](https://www.pcbway.com/project/shareproject/Commodore_128DCR_metal_case_only_RF_Modulator_Replacement_V2_75604b06.html)**

Once added to your cart, scroll down to find the **Remove product No.** option and select **Specify a location**. PCBWay should then print their product number under the 3.5mm audio jack. You should be safe to leave all other options as the default ie. 2 layer FR-4, 1.6mm board thickness, HASL with lead, etc. Alternatively you can download the [gerber files](files)

Note PCBWay give me a small credit when ordering using the shared project pages.

The [BoM](files/BOM_C128_C128DCR_C64_Shortboard_RF_V2.xlsx) lists all components required and also includes friendly part names and example part links from AliExpress and Mouser for ease of ordering. Most are generic components so you can use your preferred parts supplier, but the recessed S-Video connector is a very specific type and hard to find outside of AliExpress.

## Build
Component values are printed on the front side of the PCB under the part itself (where possible) this was done to ease the build process while still giving a "clean" look once the board has been populated. I prefer to start by soldering the flat components (diodes, resistors) and then the taller ones (capacitors, transistors, switch, AV connectors).

Once all topside components have been soldered into place, install the 4 individual and 2 rows of 4 pin headers on the underside. For the rows of 4 it is recommeneded to only solder one pin, then check their alignment to make sure they are straight before soldering the remaining 3 pins. If you solder them all at once, it will be very hard to straighten them afterwards. 

Cut up another 4 individual headers and pull the black plastic spacers off with some pliers. Push these spacers onto each of the individual pin headers on the underside of the RF board. ![SPACERS](https://github.com/TheRetroChannel/Commodore-64-Shortboard-and-C128-RF-Replacement-V2/blob/main/images/C64C%20SPACERS.jpg)

## Install
Remove the original RF modulator, there are 4 tabs that need to be straightened and 8 signal connections to be desoldered - be very careful with these as they are easily damaged if not desoldered properly!

Insert the RF replacement into the mainboard (do not solder it in yet) and then the mainboard into the case. The rear ports should line up correctly in the case with no adjustment required (assuming the extra plastic spacers have been added as above). Once you have confirmed the alignment is correct, remove the mainbaord and proceed with soldering the ground posts and signal connections.

## Setup
### Right Channel Switch
Set the selector switch to the desired "right channel" output. A 3.5mm to 2x RCA cable or splitter is recommended

**CVBS**: Left channel is SID audio, right channel is composite video.

**MONO**: Both left and right channels are SID audio.

**EXTIN**: Left channel is SID audio, right channel will be whatever is connected to the "input" pin nearby. The most common use for this would be dual SID setups or LumaCode. For example if used with Lumacode, LUM from the VIC-II-dizer would connect to "input", and GND to "ground".

Remember audio signals can be safely spilt, but not video signals. You can for example use the 3.5mm jack for composite video on the right channel, and split the left channel audio into left and right (dual mono).

The board can also safely drive both composite and S-Video outputs at the same time but not dual S-Video or dual composite (using both the RF replacement output and C64/128 DIN connector). In most cases you shouldn't need to use the C64/128 DIN connector, but all the standard video and audio signals will still be available there if required.

### Contrast fine tune
Commodore used a fixed value resistor for all RF modulators which doesn't take into account variances in the video output of each and every VIC-II. I've added this option so the output can be tailored for your VIC-II and display combination.

Set the potentiometer to the mid position and power on the C64/128. Change the foreground colour to white: POKE53281,1 and the border colour to light grey: POKE53280,15

Adjust the potentiometer to obtain the ideal contrast. Too low and the white will appear light grey, too high will cause white to bloom and text will appear to shrink. This adjustment may also have an effect on jailbars if present in the borders, so it is recommended to play around until you find a sweet spot.
**Note this adjustment may have little to no effect depending on your display or upscaler - in which case it is recommended just to leave the trimpot at its mid position.**

### C128 jailbar filter 
This is a low pass filter designed to lessen the jailbar effect on Commodore 128 machines (or C64 if you have bad jailbars). A 1nF ceramic capacitor can be added at C1 but it is recommended to experiment with this before soldering into place. 

With the 128 powered on (mind the nearby PSU in the DCR version), insert the capacitor so the legs touch both holes of C1 without touching the mainboard underneath. You should observe a noticeable reduction in jailbars with the capacitor inserted, but this comes at the expense of overall sharpness. It is recommended to load up your favourite program and see which look you prefer. Personally I prefer to leave it out but you do you.
![128FILTER](https://github.com/TheRetroChannel/Commodore-64-Shortboard-and-C128-RF-Replacement-V2/blob/main/images/C128%20FILTER%20COMPARISON.png)


**Marvel at the beauty of your Commodore, force your friends, relatives, and random people on the internet to do the same.**

-------

To help me continue doing this kind of thing or just to say thanks, consider signing up as a [Patron](https://www.patreon.com/theretrochannel)
