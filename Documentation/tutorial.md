# How to make an Ibis Tracker (Stacked Smol Slimes: SlimeVR Compatible nRF Trackers)

> [!NOTE]
> Ibis trackers are SlimeVR Compatible full body tracking devices. They are "Smol Slimes", which means they use nRF instead of WiFi to connect to your PC. nRF is similar to Bluetooth, but with lower latency. To learn more, please visit the SlimeVR Documentation on Smol Slimes.

Ibis Trackers are completely open source, which means you can build your own if you have the time. They are identical to the product we sell. This guide will show you the process we take for each tracker.

## Parts Required

To make your trackers, you’ll need access to a 3D printer. You can also buy the 3D printed parts from us. You’ll also need:

- [ ] Stanley Knife (or something very sharp)
- [ ] Wire Cutters
- [ ] Wire Strippers
- [ ] Kapton Tape
- [ ] Fine tip soldering iron specifically for electronics (best if it has temperature control)
- [ ] Solder Flux
- [ ] Other tools that may make the process easier

### Tracker Components

Each tracker is made up of only a few components:

- [ ] IMU Module (ICM-45686 or LSM6DSR)
- [ ] SuperMini (ProMicro) nRF52840 or Seeed Studio equivalent board
- [ ] 120mAh LiPo Battery
- [ ] Small, tactile push button
- [ ] Board pins (should have come with your SuperMini)
- [ ] Wire for the antenna mod

## Component Preparation

To ensure each component fits correctly and works, there are a few steps we need to take before we assemble each tracker.

### IMU

The IMU will most likely come in rows of 5, and will have some little defects we want to shave off. Before then, if you still have them connected, you’ll need to add some Kapton tape to the back of them. This prevents solder from seeping through onto the SuperMini board later.

<img 
    src="../Images/process/imus.jpg" 
    alt="LSM6DSR IMU modules joined still from factory." 
    title="LSM6DSR IMU modules joined still from factory."
    width="400">

<img 
    src="../Images/process/imus-back-kapton-tape.jpg"
    alt="Add Kapton tape to the back of the IMUs, aligning the tape so the pins can still make contact with the side of the module."
    title="Add Kapton tape to the back of the IMUs, aligning the tape so the pins can still make contact with the side of the module."
    width="400"
    >

<img src="../Images/process/imus-back-kapton-tape-2.jpg" width="400" title="Cut the excess tape off." alt="Cut the excess tape off.">

<img src="../Images/process/imu-kapton-back-split.jpg" width="400">

<img src="../Images/process/imus-split-front.jpg" width="400">

Once you’ve separated and taped your IMU’s, you’ll want to shave off the excess from the top and bottom. This isn’t a required step, but helps clean them up a bit.

<img src="../Images/process/imu-prep-unprepped.jpg" width="400">
<sub>Left: Shaved/cleaned up IMU vs. unshaved IMU on the right</sub>

#### Pre-Soldering The IMU

This step is as far as I can tell, unique to our process. I designed a “Soldering Cube” to help make this process less likely to destroy part of the SuperMini.

<img src="../Images/process/soldering-cube-imu.jpg" width="400">

You can get a Soldering Cube here: [https://github.com/brisfknibis/ibis-trackers/blob/main/3D%20Print%20Models/Soldering%20Fixture/Solder%20Cube.stl]

Take your pins, and split them in half. You’ll need a row of six:


<img src="../Images/process/header-pins.jpg" width="400">

<img src="../Images/process/header-pins-split.jpg" width="400">

Push the plastic on the 6 pins down towards the bottom. I use a breadboard to push the pins down easily. I also do this on my soldering mat, so they don’t go ALL the way to the bottom. about 1mm at the end is right.

<img src="../Images/process/header-pins-6.jpg" width="400">

Place the pins in the soldering cube with the IMU.

Tile the cube on the side so we can more easily solder the pins.

<img src="../Images/process/soldering-cube-side-split.jpg" width="400">

I prefer to solder the left, then the right most pins, then the inner ones. Just a little bit of solder first, then if you want, you can strengthen the connections with a bit more solder.

<img src="../Images/process/soldering-cube-soldered-partial.jpg" width="400">

<img src="../Images/process/soldering-cube-soldered.jpg" width="400">

Once you’re happy with your joints, I recommend cleaning it with a bit of Isopropyl alcohol or PCB cleaner to remove any flux from the soldering process.

<img src="../Images/process/soldering-cube-soldered-clean.jpg" width="400">

Remove the IMU from the soldering cube, and snip the pins as close to the plastic as possible. You can attempt to just slide the plastic off, but this risks pulling the pins off the IMU.

<img src="../Images/process/imu-soldered-cut.jpg" width="400">

Now onto the SuperMini!

### SuperMini nRF52840

For the SuperMini development board, there are 3 steps to prepare this one. It’s also your main tracker board, so most steps will focus on this device.

#### Preparing the board

As with the IMU, you’ll want to shave off the excess from the sides of the unit. This is a requirement, otherwise it will not fit inside the case.

<img src="../Images/process/supermini-unprepped.jpg" width="400">
<sub>SuperMini Module with edges that need to be cleaned up.</sub>



<img src="../Images/process/supermini-prepped.jpg" width="400">
<sub>SuperMini nRF52840 with cleaned up edges. I used a Stanley knife for this one.</sub>



#### Flashing the Firmware

Before we start soldering, it’s best to ensure that the SuperMini actually works. Connect it via USB to your PC, and open the Serial Terminal in nRF Connect for Desktop app. The first sign of a good board is that it should be blinking like the following:

https://github.com/user-attachments/assets/df2efdcd-7cdc-43db-9c79-72d2ddccd075

Next, we need to short the RST button to the GND pin. Alternatively, you can act as ground and use something metal to short the RST pin like this:

https://github.com/user-attachments/assets/f4e1e084-4e9f-4b25-8d95-d314f9fac9a3

Once you’ve shorted the pin by tapping it 2 times (sometimes it takes 2-5 times) the red light will fade/flash solid. Then, you can copy the .UF2 bootloader file to update the device BEFORE we flash it with the tracker firmware.

Download the Bootloader firmware here: [https://github.com/SlimeVR/Adafruit_nRF52_Bootloader/releases/download/0.9.2-SlimeVR.7/update-slimenrf_promicro_bootloader-0.9.2-SlimeVR.7_nosd.uf2]

To copy the firmware, simply copy and paste the bootloader file above to the “NiceNano” drive that appears in your computer. It should look like a USB Drive.

<img src="../Images/process/nicenano-pc.png" width="400">

Your SuperMini will reset, and the drive will disappear. If you see it in the Terminal, it most likely worked. It may appear like a “Feather” device in your Serial Terminal.

<img src="../Images/process/serial-terminal-feather.png" width="400">
[Updated Bootloader. Non-updated will look the same, or may have a different name.]

<img src="../Images/process/serial-terminal-nicenano.png" width="400">
[A SuperMini in “DFU” mode, ready to be flashed with firmware]

Next, we need to flash the SlimeVR Tracker Firmware.

Download the latest SlimeVR Tracker Firmware here: [https://github.com/Shine-Bright-Meow/SlimeNRF-Firmware-CI/releases/download/latest/SlimeNRF_Tracker_NoSleep_SPI_StackedSmol.uf2]

Short the RST pin again and copy the above file. Once done, the tracker should appear in the terminal like this:

<img src="../Images/process/serial-termainl-slimenrf-tracker.png" width="400">

You can now connect to the tracker, and check everything so far is working:

<img src="../Images/process/serial-terminal-connect.png" width="400">

Looks like we’re working!

In the text input above, type “info”:

<img src="../Images/process/serial-terminal-info-screen.png" width="400">
(Info screen for a tracker with no IMU attached.)

Great! That’s enough for us to continue to the next stage.

#### Pre-Soldering the Board 

There are a few points I prefer to pre-solder to make life easier for us later. Fill the following pins with solder. We’re adding solder to the battery connectors, button contacts, and the antenna for the antenna mod (right side only!)

<img src="../Images/process/supermini-solder-points.jpg" width="400">
[Add solder to these points]


<img src="../Images/process/supermini-prepped-2.jpg" width="400">
[Pre-Soldered SuperMini. 006, GND, B+, GND (right side) and the right side of the C3 antenna.]

Lastly, it's easiest to solder the button on now.

<img src="../Images/process/supermini-button.jpg" width="400"> 

#### Assembly

To connect the IMU to the SuperMini, we need to solder the 6 pins from the left side of the IMU to the 6 pins on the left side of the SuperMini starting from the THIRD PIN, 011.

<img src="../Images/process/imu-soldered-supermini-placement.jpg" width="400"> 
[Note the placement of the pins, with the top pin on the IMU going into 017 on the SuperMini.]

Flip the SuperMini upside down with the IMU inserted into the correct pins, and snip off the excess pin length:

<img src="../Images/process/supermini-pins-back.jpg" width="400"> 
[SuperMini with IMU pins that need to be snipped]

<img src="../Images/process/supermini-back-pins-cut.jpg" width="400"> 
[Pins have now been snipped!]

Solder the pins from the back, and clean off any excess Flux from your solder job using isopropyl alcohol or PCB cleaner.

<img src="../Images/process/supermini-pins-soldered.jpg" width="400">
[SuperMini with pins soldered from the back for the IMU.]

<img src="../Images/process/supermini-pins-soldered-front.jpg" width="400">

Usually, you should solder the pins so they are creating a good contact. This one is okay because the pins are connected correctly from the back. Notice on most of these, they don’t appear to have a good soldered connection on the top. I find this to be okay, and even optimal, because too much solder can short the connections with one another.

#### Check the Connection

Before we do the final assembly steps, you’ll want to connect the tracker to your PC and check to see if the IMU is detected. If it’s detected, you should see info logs about motion and status switching. Type “info” into the text box, and you should see something like this:

<img src="../Images/process/serial-terminal-info-with-imu.png" width="400">
[IMU will show as the model if it is detected.]

If your terminal is being spammed with yellow warnings, type “Reboot” and this should hopefully clear it. If no IMU is detected, you may need to go back and check your soldering connections and try again.

In our case, everything is working as expected, so we can solder the last pin, “002”, on the right hand side. Note that the pin labels are underneath the pins, not above them, so you want to solder a pin in the hole between “002” and “029”.

<img src="../Images/process/supermini-imu-side-pin-circled.jpg" width="400">

NOTE: If you are using ICM-45686 modules, you will ALSO need to solder the lowermost pin on the IMU to pin 111 on the SuperMini. Leaving you with two soldered pins on the right side.

![supermini-imu-side-pin-circled-icm45686](https://github.com/user-attachments/assets/d6f67178-33d3-4086-ae8a-2b783254ddf4)

A good way to connect these is by using the remaining pins from the pin rows. Using the remaining pins, place them in the holes.

<img src="../Images/process/supermini-pins-setting.jpg" width="400">

Solder pin “002”.

<img src="../Images/process/supermini-pins-set-soldered.jpg" width="400">

You should be able to then pull out the rest of the pins from the plastic, leaving just the one remaining.

<img src="../Images/process/supermini-pin-soldered.jpg" width="400">

Fold the pin down so it’s touching the IMU, then snip the top.

<img src="../Images/process/supermini-pin-sodlered-2.jpg" width="400">
[Bent the pin towards the IMU]

<img src="../Images/process/supermini-imu-pin-bent-soldered-.jpg" width="400">
[Snipped pin]

Solder the connection, and be sure to clean off any flux.

<img src="../Images/process/supermini-pin-bent-soldered-imu-complete.jpg" width="400">

#### Connecting the Wire Mod

SuperMinis have horrendous signal strength by themselves. To improve the signal, the best option is to cut a wire 31mm long (3.1cm) and connect it to the RIGHT side of the C3 antenna.

<img src="../Images/process/31mm-wire.jpg" width="400"> 
[Wire cut at 31mm (3.1cm), with an extra mm or two]

<img src="../Images/process/31-mm-wire-antenna.jpg" width="400"> 
[Connect the wire to only the right side of the antenna]

<img src="../Images/process/31mm-wire-soldered.jpg" width="400"> 
[Soldered wire]


#### Connecting The Battery

To be a little safer with the battery, you can use some masking tape to cover the positive wire's tip. This makes sure that the battery cannot accidentally shock you or damage the components.

A little trick I like to use is setting the board on its side with the Antenna Mod, and pushing the battery's Negative terminal through.

<img src="../Images/process/battery-placement.jpg" width="400"> 
[Board on its side]

<img src="../Images/process/battery-ground-wire-soldered.jpg" width="400"> 
[Soldered battery negative terminal. Note it is going into the GND pin]

Once you have soldered the negative terminal, you can then solder the positive terminal to B+.

### You just built a Stacked Smol Slime Tracker!

<img src="../Images/process/completed-tracker.jpg" width="400"> 

Put it in a case, and enjoy!







