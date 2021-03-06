# QAV-R 5" KISS ESC Racer

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/preview.jpg)
![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/preview2.jpg)
{% youtube %}https://www.youtube.com/watch?v=wMYgqvsNEwQ{% endyoutube %}

## Parts List

### Vehicle (needed for flying)
* Autopilot: [Pixracer](../flight_controller/pixracer.md) from [AUAV](https://store.mrobotics.io/mRo-PixRacer-R14-Official-p/auav-pxrcr-r14-mr.htm) including ESP8266  WiFi- and [ACSP5](https://store.mrobotics.io/product-p/auav-acsp5-mr.htm)  power-module
* Frame:  [Lumenier QAV-R 5"](http://www.getfpv.com/qav-r-fpv-racing-quadcopter-5.html)
* Motors:  [Lumenier RX2206-11 2350KV](http://www.getfpv.com/lumenier-rx2206-11-2350kv-motor.html)
* ESCs:  [KISS 24A Race Edition](http://www.getfpv.com/kiss-24a-esc-race-edition-32bit-brushless-motor-ctrl.html)
* Props: HQProp 5x4.5x3 [CW](http://www.getfpv.com/hqprop-5x4-5x3rg-cw-propeller-3-blade-2-pack-green-nylon-glass-fiber.html) [CCW](http://www.getfpv.com/hqprop-5x4-5x3g-ccw-propeller-3-blade-2-pack-green-nylon-glass-fiber.html)
* GPS / Ext. Mag.: M8N taken from a [3DR Pixhawk Mini set](https://store.3dr.com/products/3dr-pixhawk) and rewired
* Battery: [TATTU 1800mAh 4s 75c Lipo](http://www.getfpv.com/tattu-1800mah-4s-75c-lipo-battery.html)
* RC Receiver: [FrSky X4R-SB](http://www.getfpv.com/frsky-x4r-sb-3-16-channel-receiver-w-sbus.html)
* Remote Control: [FrSky Taranis](http://www.getfpv.com/frsky-taranis-x9d-plus-2-4ghz-accst-radio-w-soft-case-mode-2.html)
* FC dampening: [O-Rings](http://www.getfpv.com/multipurpose-o-ring-set-of-8.html)
* GPS Mount: [GPS mast](http://www.getfpv.com/folding-aluminum-gps-mast-for-dji.html)

### FPV (optional)
* Camera: [RunCam Swift RR Edition](http://www.getfpv.com/fpv/cameras/runcam-swift-rotor-riot-special-edition-ir-block-black.html) **includes must-have high quality wide angle lens from GoPro!**
* Video Tx: [ImmersionRC Tramp HV 5.8GHz 600mW](http://www.getfpv.com/fpv/video-transmitters/immersionrc-tramp-hv-5-8ghz-video-tx.html)
* Video Antennas: [TBS Triumph 5.8GHz CP](http://www.getfpv.com/fpv/antennas/tbs-triumph-5-8ghz-cp-fpv-antenna-3275.html) (SMA port fits ImmercionRC Tx)
* FPV voltage source plug: [Male JST Battery Pigtail](http://www.getfpv.com/male-jst-battery-pigtail-10cm-10pcs-bag.html)

> **Info** These parts cover the sending side for standard FPV 5.8GHz analog FM video. You need to have a compatible receiver and display device to actually consume the live video stream.


## Assembling the Basic Frame

I assembled the basic center plate and the arms like shown in this video between 09:25 and 13:26:
<p align="center">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/7SIpJccXZjM?start=565&end=806" frameborder="0" allowfullscreen></iframe>
</p>

I mounted the four motors to the frame with the cables coming out towards the center of the frame. I used two of the longer motor screws that come with the frame for each motor and put them in the two holes which are further apart.

## Building the Power Train

The KISS ESCs are known for their good performance but they also come with two disadvantages:
- The software they use is not open source (unlike BLHeli)
- There exists to my knowledge no hardware package with presoldered wires and or plugs

This means we need to solder at least 6 joints on every ESC but it's still totally worth it.

> **Tip** Always tin both sides you want to connect with solder before actually soldering them together. This will make it a lot easier and it will be less likely to have cold soldering joints.

<span></span>
> **Tip** Make sure that you use an apropriate cable gauge for the power connections that transport the high current all the way from the battery to the motors. All signal cables can be very thin in comparison.

<span></span>
> **Tip** Put heat shrink on the cables before you start soldering! Heatshrinking the ESCs, the power module and the free floating uninsolated wire soldering joints after a successful function test will protect them from dirt, moisure and physical damage

### Motors
First I cut all three motor cables to directly fit when the ESCs are mounted on the arms shifted towards the center but still let enough slack to allow easy placement of the parts and not produce any tension on the cables. Then I soldered them in the order they come out of the motor to the output contacts of the ESCs which are oriented with the switching MOS-FETs facing updwards to get good air cooling during flight. Choosing this cable order resulted in all the motors spinning counter-clockwise in my tests and I switched where necessary the direction of rotation by bridging the dedicated [JP1 solder jumper](https://1.bp.blogspot.com/-JZoWC1LjLis/VtMP6XdU9AI/AAAAAAAAAiU/4dygNp0hpwc/s640/KISS-ESC-2-5S-24A-race-edition-32bit-brushless-motor-ctrl.jpg) to conform the [Quadrotor x configuration](../airframes/airframe_reference.html#quadrotor-x).

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/power-motor-connections.jpg)

### Power Module
First I soldered the XT60 connector which comes with the frame to the labeled battery side of the [ACSP5 power module](http://fs5.directupload.net/images/160304/a72l2mbz.jpg) that was shipped with the pixracer and added the elco capacitor delivered with the power module with the correct polarity to the same side.

Now comes the tricky part. I soldered all four ESC voltage source + and - ports to the corresponding pad on the labeled ESC output side of the power module. Make sure to not have any cold solder joint here because the quad will not end up well with a loose connection in flight. Using the additional power distribution board of the frame would make the job a lot easier but also takes too much space on such a small frame...

> **Tip** If you are also including the FPV parts don't forget to also solder your JST male power plug to the ouput side of the power module. You'll need it for your [FPV setup](#fpv-setup) later on.

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/power-module.jpg)

### Signal Cables

I used thin cables with a standardized pin header connector which were cut in half for the ESC signal because this will allow easy plugging on the pixracer pins later on. Only the labeled `PWM` port on the [KISS ESCs](https://1.bp.blogspot.com/-0huvLXoOygM/VtMNAOGkE5I/AAAAAAAAAiA/eNNuuySFeRY/s640/KISS-ESC-2-5S-24A-race-edition-32bit-brushless-motor-ctrl.jpg) is necessary for flying. They will be connected to the correct motor signal output of the pixracer. The `TLM` port is for ESC telemetry and I soldered them on for future use as the needed protocol is not currently supported by PX4.

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/power-esc-signals.jpg)

I tested all ESC motor pairs and their rotation directions using a cheap PWM servo tester before proceeding further.

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/motor-test.jpg)

## Connecting & Mounting Electronics

> **Tip**
> Double check the pin assignment of every component you connect. Sadly not every hardware component out there is plug and play even if it may look like this at first glance.

You'll need the [hardware documentation of the Pixracer](https://docs.px4.io/en/flight_controller/pixracer.html) for this step to find all needed connectors. I tried to route all the cables under the Pixracer board to have a clean build and save space for FPV camera and transmitter in the future.

I mounted the Pixracer using the nylon spacers and screws that get shipped with the QAV-R frame but **put some small O-rings** between the board and the spacers to add a bit of vibration dampening. Make sure to **not tighten the screws too much or too less**, do it such that the board clearly touches both sides but is not clamped with any tension. The board should not dangle in any way but be slightly movable if you apply force to it with your fingers.

> **Warning**
> This can heavily influence the vibration noise level your gyroscope and accelerometer sensors measure during flight.

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/mount-oring.jpg)

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/center-connections.jpg)
![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/center-overview.jpg)

### RC Receiver

I hooked up the FrSky S-BUS receiver using the cable shipped with the Pixracer but cut away the unnecessary cable branch.

For the smart telemetry port I used the cable shipping with the receiver. I removed all unnecessary pins from the connector using tweezers and switched the white loose end cable to the correct pin of the connector to have the "smart" signal connected. I then soldered the loose end to a cable fitting the FrSky port following this [scematic](https://docs.px4.io/images/grau_b_pixracer_frskys.port_connection.jpg). I also skipped the ground (GND) pin because like the voltage supply positive pin it is already connected trough the RCin S-BUS cable.

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/rc-receiver-connections.jpg)

### RC Antenna Mount

To have a good RC link while not risking to have the antenna in the props I employed a rugged mount method using heat shrinks and zip ties.

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/rc-antenna-mount-material.jpg)

For this method you cut the big end with the hole off the zip tie, put the rest together with the antenna cable through a long heat shrink and mount this to your frame spacers using a bigger but shorter heat shrink.

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/rc-antenna-mount.jpg)

### ESC signal

For the ESC signals I followed the [hardware documentation of the Pixracer](https://docs.px4.io/en/flight_controller/pixracer.html) and the [Quadrotor x configuration](../airframes/airframe_reference.html#quadrotor-x) motor numbering scheme. As we have no ground or positive BEC voltage connections we connect our `PWM` ESC signal cables each to its topmost pins of the corresponding output connector.

### GPS / External Magnetometer

I took the GPS cable which fits the connector of the used GPS and came with the Pixracer set. Sadly the pin assignment was completely wrong and I rewired the connector again using tweezers according to the [3DR Pixhawk Mini user manual](https://docs.px4.io/en/flight_controller/pixhawk_mini.html#connector-pin-assignments-pin-outs) GPS port.

#### Pixracer GPS/I2C Port
| Pin  | Assignment |
| ---- | ---------- |
| 1    | GND        |
| 2    | SDA        |
| 3    | SCL        |
| 4    | RX         |
| 5    | TX         |
| 6    | +5V        |

#### M8N 3DR pixhawk mini GPS Connector
| Pin     | Assignment | Connect to Pixracer Pin |
| ------- | ---------- | ----------------------- |
| 1 (red) | SCL        | 3                       |
| 2       | SDA        | 2                       |
| 3       | VCC 5V     | 6                       |
| 4       | RX         | 5                       |
| 5       | TX         | 4                       |
| 6       | GND        | 1                       |

I mounted the GPS module using the listed generic multicopter GPS mast because mounting it any closer to the main body made the magnetometer readings totally unusable. An experiment mounting the module directly to the far back of the top of the frame showed 6 times magnetometer magnitude noise most likely caused by the magnetic field of the ESC currents. Note that I shortened the mast by ~2cm to make it better fit the cable length and the frame dimensions. The GPS module is sticked with double sided tape to top plate of the mast.

## FPV Setup

This are instruction for the optional 5.8GHz FPV live video transmission. You'll need the additional FPV parts listed at the beginning. The FPV transmission described here is electronically independent of the flight controller, it only takes the battery voltage after the power module.

I first did a bench test to make sure everything is working correctly. For this connect the video signal cable that comes with your transmitter and plug it to the back of your FPV camera and to the matching plug of the transmitter. Screw the  Then connect the JST power plug to your draft vehicle or to some other voltage source. The transmitter LED should light up. Use your 5.8GHz receiver device tuned in to the correct channel to check for the video. To configure the transmitter to an other channel and adjust the transmission power please refer to the [Tramp HV User Manual](https://www.immersionrc.com/?download=5016).

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/fpv-wiring.jpg)

Like you can see I mounted the transmitter from the inside to the "roof" of the frame using a ziptie. Always put a self sticking piece of foam in between when mounting electronics like this to avoid physical damage during flight. Make sure to place the transmitter such that the antenna connector fits to the dedicated hole of the frame.

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/fpv-tx.jpg)

The magnificent FPV camera set in the part list comes not only with the best FPV lens I've seen so far but also includes multiple camera mounts one of which is very flexible for adjusting the camera angle and nicely fits into the QAV-R frame. I mounted it like you can see in the next picture. The two screws and nuts to lock the camera mount to the frame were taken from the spare ones remaining from the frame set.

![](../../assets/airframes/multicopter/qav-r-5-kiss-esc-racer/fpv-cam.jpg)

## Software Configuration

> **Warning**
> Always make sure to have either battery or propellers pyhsically removed from your vehicle during any initial configuration. Better safe than sorry!

For general configuration instruction please refer to the [step-by-step guide](https://docs.px4.io/en/config/).

For this build I pulled the latest PX4 master because it supports the "FMU as task" improvements is [explained just below](#improve-racer-performance) and flashed it to the Pixracer. I used [QGC](http://qgroundcontrol.com/) daily build configure the following:
- Choose the [Quadrotor x configuration](../airframes/airframe_reference.html#quadrotor-x) Airframe
- Calibrate the sensors
- Set the battery to 4S (4 cell LiPo) with charged cell voltage 4.15V and empty cell voltage 3.5V
- Calibrate the voltage devider through typing in the current accurate voltmeter measurement
- Calibrate the RC cannels with the Taranis already configured for two additional switch inputs. One switch in the top right corner of the Taranis front plate for the mode switch and the other switch in the top left corner of the front plate as arm switch.

### Arm switch

To use an arm switch manually set the parameter `RC_MAP_ARM_SW` to the corresponding switch RC channel. The vehicle should from then on immediately arm/disarm whenever your switch is tuned on/off. The state of the switch is not forced to the vehicle and therefore all other arming/disarming methods still work. If the switch positions are reversed just change the sign of the parameter `RC_ARMSWITCH_TH` or also change it's value to alter the threshold value. Make sure to test this under safe conditions!


### Improve Racer Performance

This build was done to evaluate and improve PX4 racing quad performance. Recently progress was made in reducing the rate/inner control loop delay and the following options therefore increase the rate controllers performance:
- **Activate the Oneshot125 protocol** to communicate to the ESCs <br>
  set `PWM_RATE = 0` (takes effect after the next reboot)
- **Run the FMU as task** instead of in the work queue <br>
  set `SYS_FMU_TASK = 1` (takes effect after the next reboot)

### Tuning

Here's the general [Tuning Guide](https://docs.px4.io/en/advanced_config/pid_tuning_guide_multicopter.html) with instructions on all the basics. I just add some personal hints here on what I did for this build.

I first made sure `PWM_MIN` is set such that all motors still safely turn idle when arming but with a value as low as possible. For me it was `1075`.

I did first tuning in acro mode with all `MC_ACRO_...` all set to 100 deg/s to have useful hover control. And arrived after the two optimizations from above at the following tuning gains:
```
... stands for ROLL and PITCH
MC_...RATE_P = 0.06
MC_...RATE_I = 0.1
MC_...RATE_D = 0.001
MC_YAWRATE_P = 0.1
```
Note that these gains will likely not work well for you but I wanted to give them just as a reference.

After you found a good tuning for the rate controller, flying in manual mode with the default attitude controller gains should already be pretty acceptable and tuning it further isn't very hard anymore.

### Log Examples
[Log in FPV acro flight (maximum values: 108km/h speed, 85A total current draw)](https://logs.px4.io/plot_app?log=9c311942-bc7c-4b0c-8be8-eeb64fa8192c)
[Log in (mostly) manual LOS flight for the entire battery](https://logs.px4.io/plot_app?log=6de8b8cd-74f9-4eae-ad2f-76867e916f4f)