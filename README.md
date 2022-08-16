<!-- PROJECT LOGO -->
<br />
<p align="center">
   <img src="https://github.com/mcauser/MCUDEV_DEVEBOX_H7XX_M/blob/master/docs/STM32H7XX_M.jpg" alt="Logo" width="300" height="300">

  <h3 align="center">Bare metal stm32h7</h3>

  <p align="center">
    A bare metal implementation of a UART example for the stm32h743 with a simple makefile and without using HAL libraries. 
    <br />
    
  </p>
  
  
</p>



<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#detailed-description">Detailed description</a></li>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

This example shows how to establish a serial communication between the stm32h743 microcontroller and a laptop using the UART peripherals. 
To demonstrate the connection, the user can use the serial communication program minicom to interact with the board and command the blinking pattern of the LED. 



This project does not rely on HAL libraries and the code can be built and flashed using GNU make (so that you do not need any IDE such as STM32CubeIDE) and the GNU ARM Embedded Toolchain. The code was tested with the stm32h743vit6 development board from <a href="https://github.com/mcauser/MCUDEV_DEVEBOX_H7XX_M">DevEBox</a> but could be easily adapted for any configuration. The board can be purchased on  <a href="https://www.banggood.com/STM32H750VBT6-or-STM32H743VIT6-STM32H7-Development-Board-STM32-System-Board-M7-Core-Board-TFT-Interface-with-USB-Cable-p-1661383.html?cur_warehouse=CN&ID=6288383">Banggood</a>. 


### Detailed description
The program configures the PA1 pin as a LED (ouput push-pull) and the PB12, PB13 pins for UART5. 

The UART protocole is kept in the default configuration (`8N1`) and the baud rate is set to `38400`.

The system clock frequency is set to 480MHz, assuming the presence of a 25MHz high speed external (HSE) crystal. If you do not use a HSE or if you have an older version of the chip* you might have to modify the clock configuration function or rely on the default internal oscillator (64MHz). In that case you will have to change the baud rate register (e.g. with the internal oscillator at 64MHz, baud rate of 38400, the BRR should be modified with: uint16_t uartdiv = 64000000 / 38400;)

The program allows a user to interact with the microcontroller to flash the PA1 LED (D2) a given number of times (between 0 and 9). The program then returns an echo message. 

*Note that stmicroelectronics recently introduced a new version of their chip (version V) able to operate at up to 480MHz.



### Built With

* [GNU make](https://www.gnu.org/software/make/)
* [GNU ARM Embedded Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)
* C



<!-- GETTING STARTED -->
## Getting Started


### Prerequisites

You need to install the following:
* GNU make
* git 
* st-link 
* GNU ARM toolchain 
* minicom or PuTTY

### Installation

1. Clone the repo
   ```sh
   git clone https://github.com/martindoff/bare-metal-stm32h7-uart.git
   ```
2. Go to directory 
   ```sh
   cd bare-metal-stm32h7-uart
   ```
3. Build
   ```sh
   make
   ```
3. Flash the board (connect via st-link V2 debugger) 
   ```sh
   make flash
   ```
4. Disconnect the st-link V2 debugger and connect the board to a development computer with a USB TTL serial adapter according to the following schematics:
<img src="https://github.com/martindoff/baremetal-stm32h7-uart/blob/main/stm32-uart.jpg" alt="Logo" width="300" height="300">

5. Find the name of the COM port. In macOS, this can be found in the /dev directory and starts by the prefix 
`/dev/cu`. 
6. Configure the COM port. For example, using `minicom`: 
 ```sh
   minicom -s
   ```
The configuration can be done as follows:
* Select the "Serial Port Setup" entry and press Enter. 
* Modify the path name to match the name of the COM port found previously (press 'A'). 
* Disable flow control ('F' and 'G'). 
* Change the port settings by typing 'E':   set the baud rate to `38400` ('D') and configure the port to `8N1` ('Q'). 
* Type Enter twice to go back to the main menu and choose the option "Save setup as..." to give a name to the configuration, e.g. `config`. 

If you exit `minicom`, you can retrieve your configuration as explained in step 7. Otherwise go to step 8 directly. 

7. To open `minicom` and retrieve the saved setting in `config`: 
 ```sh
   minicom config
   ```
8. In the active `minicom` terminal, interact with the stm32h743 by typing a digit between 0 and 9 (any entry out of this range will be converted to 0 by the program running on the microcontroller).
Observe the LED blink as much time as prompted (laptop -> stm32h743) and notice the message returned by the microcontroller (stm32h743 -> laptop).  

<!-- ROADMAP -->
## Roadmap

Starting from this simple bidirectional UART communication example, more complex projects will be built. For example, hardware-in-the-loop simulations can be enabled by exchanging data via the UART protocol between the microcontroller and a development computer. 

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.



<!-- CONTACT -->
## Contact

Martin Doff-Sotta - martin.doff-sotta@eng.ox.ac.uk

Linkedin: https://www.linkedin.com/in/mdoffsotta/





<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/github_username/repo.svg?style=for-the-badge
[contributors-url]: https://github.com/github_username/repo/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/github_username/repo.svg?style=for-the-badge
[forks-url]: https://github.com/github_username/repo/network/members
[stars-shield]: https://img.shields.io/github/stars/github_username/repo.svg?style=for-the-badge
[stars-url]: https://github.com/github_username/repo/stargazers
[issues-shield]: https://img.shields.io/github/issues/github_username/repo.svg?style=for-the-badge
[issues-url]: https://github.com/github_username/repo/issues
[license-shield]: https://img.shields.io/github/license/github_username/repo.svg?style=for-the-badge
[license-url]: https://github.com/github_username/repo/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/github_username
