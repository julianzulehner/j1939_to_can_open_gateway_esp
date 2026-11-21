# J1939 to CAN Open Gateway

This project aims to create a low-budget J1939 to CAN Open gateway which enables the use of J1939 CAN sensors which are used in automotive for test purposes in the lab.
For this project, two ESP32-C3 MINI were used. Each has one CAN transceiver. The two ESP32 communicate via UART.
The communication is unidirectional (J1939 --> ESP32 --> UART --> ESP32 --> CANOpen).

## Limitations
The J1939 side is limited to the TE Connectivity OPS3 oil property sensor, but you can configure other sensors.

The CANopen side is not fully implemented and includes only the features required for this project. 
New objects can be implemented in the object dictionary, but be aware that the implemented hash table might create hash collisions. For the set of objects used in this project, however, it works.

## Description

Two ESP32 development boards are connected together, communicating via UART.<br>

The first ESP32 reads the CAN messages from the TE Connectivity OPS3 oil 
property sensor, which uses J1939 sensor at a baud rate of 250kBits/s.
The data is parsed and sent via UART to the second device. <br>

The second ESP32 incorporates the CANopen application layer and works on a 
baud rate of 125kBits/s. Parts of CiA 301, CiA 305, and CiA 404 are implemented.
- NMT slave
- Node guarding
- SDO service
- TPDO service on sync
- LSS protocol (CiA 305)
- TPDO mapping according to CiA 404 (Analog input sensor)

This project was made from scratch for educational reasons. If someone is 
planning to use CANOpen with ESP32 I highly recommend the 
[CANopenNode](https://github.com/CANopenNode/CANopenNode) repository instead.
<br> 

In any case, feel free to use this code as an example or as a reference.


## Prototype 
As a prototype, the components were wired as follows. Please find the names of the components used in the wiring diagram below.

<img src="./images/wiring_diagram_j1939_to_CANopen.jpg" alt="Wiring diagram of J1939 to CANOpen Gateway" width="700">

This prototype is protected by a 3D-printed casing. 

<img src="./images/20240917_082733228_iOS.jpg" width="250">

## Dependencies
- [ESP-IDF toolchain](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/index.html) in VS Code (for straightforward compiling and flashing).

## Version History

- v1.0.2
    - First working version with incomplete implementations
    - Only one TPDO configured
    - TPDO transmit on every sync message indepent of configuration

## License

This project is licensed under the MIT License - see the LICENSE file for details

## Acknowledgments
- [CANopenNode](https://github.com/CANopenNode/CANopenNode)
