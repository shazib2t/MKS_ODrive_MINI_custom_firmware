# Custom ODrive Firware for MKS-ODrive-Mini based on HW V3.6

![ODrive Logo](https://static1.squarespace.com/static/58aff26de4fcb53b5efd2f02/t/59bf2a7959cc6872bd68be7e/1505700483663/Odrive+logo+plus+text+black.png?format=1000w)

This project is all about accurately driving brushless motors, for cheap. The aim is to make it possible to use inexpensive brushless motors in high performance robotics projects, like [this](https://www.youtube.com/watch?v=WT4E5nb3KtY).

| Branch | Build Status |
|--------|--------------|
| master | [![Build Status](https://travis-ci.org/madcowswe/ODrive.png?branch=master)](https://travis-ci.org/madcowswe/ODrive) |
| devel  | [![Build Status](https://travis-ci.org/madcowswe/ODrive.png?branch=devel)](https://travis-ci.org/madcowswe/ODrive) |

[![pip install odrive (nightly)](https://github.com/madcowswe/ODrive/workflows/pip%20install%20odrive%20(nightly)/badge.svg)](https://github.com/madcowswe/ODrive/actions?query=workflow%3A%22pip+install+odrive+%28nightly%29%22)

Please refer to the [Developer Guide](https://docs.odriverobotics.com/developer-guide) to get started with ODrive firmware development.


### Repository Structure
 * **Firmware**: ODrive firmware
 * **tools**: Python library & tools
 * **docs**: Documentation

### Other Resources

 * [Main Website](https://www.odriverobotics.com/)
 * [User Guide](https://docs.odriverobotics.com/)
 * [Forum](https://discourse.odriverobotics.com/)
 * [Chat](https://discourse.odriverobotics.com/t/come-chat-with-us/281)



## *** Main Changes in this branch
* The SW Firmware is 0.5.1 as this is best known firmware for this low cost ODrive alternative from other vendor.
* The firmware is compiled for V3.6 56V varient board. If you  have other varient please recompile this firmware.
* Added Encoder estimates to publish in the CAN bus alongside heartbeat msg
* This changes mainly done for ODrive ROS2 package as there is no official support for V3.6 based hardware for encoder estimates.

## *** Compiling instruction

* Please make changes in the /Firmware/tup.config for the board varient as 'CONFIG_BOARD_VERSION=v3.6-56V'.

* Under /Firmware use `$ make` command. 
* If there is compiling issues follow the official guideline for proper libraries or tool e,g. arm compiler.
* if you face issues with arm compiler follow this QA from https://askubuntu.com/questions/1243252/how-to-install-arm-none-eabi-gdb-on-ubuntu-20-04-lts-focal-fossa

## Flashing the controller

* Once connected with ST-link v2 use the following command under `/Firmware/build` directory
* `sudo openocd -f interface/stlink.cfg -f target/stm32f4x.cfg -c init -c "reset halt" -c "flash write_image erase ODriveFirmware.elf" -c "reset run" -c exit`

