# Oscup: Open Source Custom UART Protocol
 [![Check Arduino status](https://github.com/arduino-libraries/NTPClient/actions/workflows/check-arduino.yml/badge.svg)](https://github.com/arduino-libraries/NTPClient/actions/workflows/check-arduino.yml)
 [![Compile Examples Status](https://github.com/arduino-libraries/ArduinoBLE/workflows/Compile%20Examples/badge.svg)](https://github.com/arduino-libraries/ArduinoBLE/actions?workflow=Compile+Examples) 
 [![Spell Check Status](https://github.com/arduino-libraries/ArduinoBLE/workflows/Spell%20Check/badge.svg)](https://github.com/arduino-libraries/ArduinoBLE/actions?workflow=Spell+Check)
 [![License](https://poser.pugx.org/aimeos/aimeos-typo3/license.svg)](https://packagist.org/packages/aimeos/aimeos-typo3)
 
 Contents
========

* [Description](#Description)
* [How it Works](#How-it-Works)
* [Commands](#Commands)
* [Public Functions](#Public_Functions)
* [Lets Keep in Touch](#Lets-Keep-in-Touch)
* [About](#About)

 ### Description
 `OSCUP` is an open source UART protocolo designed for working with ESP32 ARM Processors. The code well documented helps to figure out how to implement a custom protocol on UART port. 
 With this protocol you can transmit and receive data wich are tracked by a fixed preamble. Next implementation will ad ACK and NACK for each packet sent.

 ### How it Works
 It relies on primitive libraries provided by Espressiff, such as /device/uart.h for interfacing with the low level hardware and functions. The protocol provides two function  `write` and  `read` for sending and receiving data.
 When you create a new Oscup object you need to pass it an ID which keeps track of the device who sent the packet, and the communication's baudrate. Once the object is created, you can call write and read functions.

 ### Commands
 Every time the protocol writes data on UART, it inserts a command inside the packet. The command is mandatory, otherwise you may ask yourself why you want to use a protocol 
 (just use arduino Serial). On the reciever, obviously, you must distinguish between the commands you recieve. There are avaialble 4 main commands:
  - `SHARE`: this command indicates that the sender just want to share this data with the receiver (for minor reasons). You can use it if you just want to print data on the other device.
  - `CONFIRM`: this command indicates that the data that will be sent are a consequence of an action (for example, we pressed a button on device 1, we send data to device 2 and we want that device 2 not only print this data but also store them).
  - `ACK`: It will be used internally 
  - `NACK`: It will be used internally
Obviously, you can configure the action you prefer to undertake each command. We suggest not to use ACK and NACK, as for the other two, the previous indications are only guidelines that we have defined for using those two commands. Also, you can configure new commands on arduino (command = uint8_t) and send them directly in the write function

 ### Public Functions
  - `begin`: initializes the UART parameters and forwards it to the control hardware. It is mandatory to call it inside void setup().
  - `testWrite`: executes a write test on uart using a fixed string as payload.
  - `write`: the write function takes a command "user-defined", the length of the payload and the effective payload, which has a fixed length of 255 bytes. This function writes this data on UART and returns an error code.
  - `read`: It reads the data incoming and insert them in a packet_t struct, defined in .h file. It returs the lenght of the readed buffer if everything works fine, otherwise a negative error.
  - `get_timer`: returns the timer's counter
  - `get_APB_clk`: return the frequency of APB. Usually APB is used to set periphericals frequency on embedded processors.
  

 ### Lets Keep in Touch
 Follow us on YouTube: Https://youtube.com/c/ProjectoOfficial <br/>
 Follow us on Instagram: https://www.instagram.com/OfficialProjecTo/ <br/>
 Follow us on Facebook: https://www.facebook.com/MiniProjectsOfficial <br/>

 ### About
 This software is provided as it is, without any warranties. <br/>
 Authors: Dott. Daniel Rossi, Dott. Riccardo Salami
