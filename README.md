# basicFirmwareExample
Developing firmware is an essential skill that cyber security professionals should be familiar with to gain a deeper understanding to the foundation of most systems that are being relied on. Often hackers and enthusiasts dabble in embedded firmware development on open-source solutions, such as Arduino. These solutions are fine for experimentation and learning but lack speed and reliability when handling the intricate tasks involved for more complex projects. Furthermore, they abstract the developer away from low-level operations that, if understood, will result in better cybersecurity professionals. 

This workshop aims to demonstrate firmware in two-parts forwards and backwards. We will briefly review firmware, development, tools, and even generate a basic application intended for the STM32F429ZI-DISCOVERY board. The second part of this workshop will demonstrate how the firmware we develop here can be reversed to discover critical functionality with a simple binary file. 

# Forwards
This code contains a basic skeleton for the intended firmware application. Users will need to develop the initialization code as well as a few function calls both the easy way (HAL drivers) and the hard way (bit shifting / mapping). We hope this demonstrates the benefit of fully understanding low-level firmware in reverse engineering efforts. We are happy to help in any way explain the firmware development process in greater detail throughout the workshop. If you'd also like to develop the firmware from scratch yourself you can start with the following tools: 
- [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html)
- [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)

# Backwards
Once the code is compiled, you can begin your reverse engineering efforts. If you want to skip this step because you know everything there is to know already about firmware development, you can also download the compiled application [here](https://github.com/So11Deo6loria/basicFirmwareExample/raw/main/Binaries/workingBasicFirmwareExample.bin). The general approach here will be to identify the architecture, endianness, and size to analyze the binary file. Next use a tool called [SVD-Loader](https://github.com/leveldown-security/SVD-Loader-Ghidra) to dereference the peripherals more effectively. Finally, you should be able to rename/retype your way all the way back to the source code you started with for the most part. 
_Extra Credit: You should be able to patch the executable and redeploy at this point in a variety of different ways!_
