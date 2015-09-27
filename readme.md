BelugaBoard - an STM32F4 based embedded uClinux system
======================================================
----------
Version 1.1 - 04/08/2015
This repository contains the hardware files (schematics, bill of materials and fabrication files (gerbers, stackup Report and NCDrill files)) for the BelugaBoard, an [STM32F429ZI](www.st.com/web/en/catalog/mmc/FM141/SC1169/SS1577/LN1806/PF255419#) based embedded Linux board.
This board is a scholar project developed at French engineering school [INSA Lyon](http://www.insa-lyon.fr/), department of electrical engineering.

Introduction
------------
The goal was to develop a board built around an ARM Cortex-M4 capable of running a GNU / Linux system.
The microcontroller is an ARM Cortex-M4 produced by STMicroelectronics, the STM32F429ZI.
There are 256Mb SDRAM and 256Mb NOR Flash memories implemented.
The following peripherals have been implemented:
• Color LCD 480x272 interface
• USB On-The-Go (host and slave) interface
• SWD debug interface
• A number of General Purpose Input / Outputs (GPIOs) that can also be used for various devices such as an I2C, SPI, USART, I2S buses, ADC, DAC..

The board is autonomous and can be powered by a 5V standard USB power supply.
A porting uClinux 2.6.33 (February 2010) on the platform is available and maintained by Emcraft company. A custom solution is being developed.


01_Schematics_BOM_Layout
------------------------
/BOM/PRT_STM32F429ZI_Eval-Board.xls : Bill of Materials for one board (Microsoft Excel file).
/Gerber/* : Gerber fabrication files, can be opened with the free gerbv (http://gerbv.geda-project.org/) for example.
/NC Drill/* : Drill fabrication files.
/Report Board Stack/SB7043.xls : stackup report (Microsoft Excel file).
/Schematics_PCB-Prints.PDF : contains 3D rendering of the board (top and bottom), multilayer 2D rendering of the layout and schematics.

02_STM32CubeMX
--------------
STM32 Cube-MX is a graphical tool developed by STMicroelectronics that allows configuring STM32 microcontrollers very easily and generating the corresponding initialization C code through a step-by-step process.
This tool also makes pinout planning for the MCU much easier and more graphical.
It can be downloaded for free at www.st.com/stm32cube-pr2

/PRT.ioc : STM32CubeMX configuration file generated for this board.

For any further information or query, please contact [bouslikhin.badr@gmail.com](mailto:bouslikhin.badr@gmail.com)