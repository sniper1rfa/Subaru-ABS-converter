# Subaru-ABS-converter
Read hall sensors, output variable reluctance (VR) sensors.

This converts modern hall sensor inputs to older VR outputs using a Maxim 9921 IC to read 2-wire hall sensors with a Teensy 3.2. 
Use this device if you are installing new hubs that use hall wheel speed sensors on old cars with variable reluctance ABS tone-rings.

The output stage is a 2-bit digital output fed to an audio transformer (1:1 600ohm:600ohm). 
The transformer removes the DC bias and presents an inductive source to the OEM ABS inputs (to circumvent open- or short-circuit error detection).

Set the input wheel tooth count to the OEM VR wheel tooth count. 

Set the output wheel tooth count to 2x the number of magnetic poles (count poles using magentic film, see image of subaru encoder). 
The Max9921 counts both the rising and falling edge of each magnetic pole, hence the multiplier.

Set Teensy clock to 24MHz to reduce thermal issues. CPU may freeze at high temperatures. First suspect for stability problems is the crystal oscillator. 

This also includes a generic digital output labeled "VSS". This allows the device to present a VSS signal calculated as the average of both inputs.
The VSS output can be used to provide a VSS signal in the case of a new transmission without a built-in VSS sensor.
The VSS output, as installed in my car, just drives an LED and is used for status reporting. This needs to be modified if you want a proper VSS output.

There is an additional op-amp stage, but this has been left un-routed due to pure laziness. 

This setup produces and unknown amount of jitter, but it should be relatively small. 

Outputs will be disabled by >1 error per 10 seconds in the default config. 

Be sure to cut the USB power trace on the teensy prior to soldering to the board.

Use at your own risk. 
