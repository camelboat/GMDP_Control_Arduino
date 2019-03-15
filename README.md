# GMDP_Control_Arduino

## Air-conditioner_Decode_Control

This folder contains codes for both decoding the IR remote controller for regular air-conditioner and using the decoding result to control the air-conditioner through IR-transmitter

### Decode.ino
This is basically the IRrecvDumpV2 example program provided by IRremote.h. Default parameters would work for most of the air-conditioner type listed in the program, however, when we test it for decoding the IR remote controller of Green Air-contioner, these default parameters didn't work properly since the coding of Green controller has a comparably large interval in the middle of its instruction. To solve the problem, we modify both the maximum length of receiving bits at one time to 255 and the maximum waiting time for distinguishing the end of an instruction.

(More details will be added)

A typical decoding result of an instruction of the Green remote controller looks like this:

```
Encoding  : UNKNOWN
Code      : 58D0B818 (32 bits)
Timing[139]: 
     +8850, -4500     + 550, - 650     + 550, - 650     + 550, -1750
     + 500, -1750     + 550, - 650     + 550, - 650     + 550, -1750
     + 500, - 650     + 550, - 650     + 550, -1750     + 550, -1700
     + 550, - 650     + 550, - 650     + 550, - 650     + 550, - 650
     + 550, - 650     + 500, - 650     + 550, - 650     + 550, - 650
     + 550, - 650     + 550, - 600     + 600, -1700     + 550, - 650
     + 550, - 650     + 550, - 650     + 550, - 650     + 550, - 650
     + 500, - 650     + 550, -1750     + 550, - 650     + 550, -1700
     + 550, - 650     + 550, - 650     + 550, -1750     + 550, - 650
     + 500, -19950     + 500, -1750     + 550, - 650     + 550, - 650
     + 550, - 650     + 550, -1700     + 550, - 650     + 550, - 600
     + 600, - 650     + 550, -1700     + 550, - 650     + 550, - 650
     + 550, - 650     + 550, - 650     + 550, -1700     + 550, - 650
     + 550, - 650     + 550, - 650     + 550, - 650     + 550, - 650
     + 500, - 700     + 500, - 650     + 550, - 650     + 550, - 650
     + 550, - 650     + 550, - 600     + 600, - 650     + 500, - 650
     + 550, - 650     + 550, -1750     + 550, -1700     + 550, -1750
     + 550, -1750     + 500
unsigned int  rawData[139] = {8850,4500, 550,650, 550,650, 550,1750, 500,1750, 550,650, 550,650, 550,1750, 500,650, 550,650, 550,1750, 550,1700, 550,650, 550,650, 550,650, 550,650, 550,650, 500,650, 550,650, 550,650, 550,650, 550,600, 600,1700, 550,650, 550,650, 550,650, 550,650, 550,650, 500,650, 550,1750, 550,650, 550,1700, 550,650, 550,650, 550,1750, 550,650, 500,19950, 500,1750, 550,650, 550,650, 550,650, 550,1700, 550,650, 550,600, 600,650, 550,1700, 550,650, 550,650, 550,650, 550,650, 550,1700, 550,650, 550,650, 550,650, 550,650, 550,650, 500,700, 500,650, 550,650, 550,650, 550,650, 550,600, 600,650, 500,650, 550,650, 550,1750, 550,1700, 550,1750, 550,1750, 500};  // UNKNOWN 58D0B818
```

From this we can know that the length of instruction coding for this IR remote controller is 139bits. Each numbermeans the time of maintaining the signal level, while + means high level and -means low level, so that it can be transformed into 0-1 sequence.

### Controller.ino
This is the program that uses the decoding results output from Decode.ino to control the air-contioner through the IR transmitter. Default frequency for IR remote controller is 139kHz.

## Future Work

###3/15
We are going to use the serial output from the Raspberry Pi to tell the controller program running on Arduino Uno to select the instruction that user want to use.

