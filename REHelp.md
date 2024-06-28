# Introduction
The guide below helps you get started on the firmware RE. The compiled version of the vunerable application can be found at: [Binaries](Binaries/completeFirmware.bin).
# Stuff That Won't Work
- `file`
- `strings` (kindof)
- `binwalk`
# Ghidra Basics
## File Import
1. File -> New Project (Non-Shared Project)
2. Provide Project Directory and Name
3. File -> Import File (Target Binary)
4. Set Language (ARM | Cortex | 32 | Little | Default)
5. Set Options ('flash' at 0x00000000 with the default size)
   1. _Note/copy the default size of the flash region_
6. Select OK for the remaining prompts
7. Double click the file to open (Do not analyze immediately)
## Manually Setup Additional Memory Maps
1. Display Memory Map
2. Add Memory Block
   1. Block Name: ram | Start Addr: 0x20000000 | Length: 0x41000
   2. Block Name: flash_mirror | Start Addr: 0x08000000 | Length: LENGTH_OF_FLASH_FROM_IMPORT | File Bytes (Firmware File at Offset 0)
## Add Ghidra Scripts
1. Display Script Manager
2. Manage Script Directories
3. Add Bundle (Navigate to Bundle Directory)
4. Refresh
## ARM Analysis
1. Analysis -> Auto Analyze
2. Enable ARM Agressive Instruction Finder (Prototype)
3. Analyze
## Ghidra Analysis Basics
- Rename (L)
- Recast (CTRL/CMD + L)
- Go to Previous Location (ALT/OPTION + LEFT)
- Double Click FUN XREFs to go to Decompiled Source
- Find References: 
   - Search -> Strings
   - Symbol Tree -> Namespaces -> Peripherals
# SVD Loader
1. Download [SVD Loader](https://github.com/leveldown-security/SVD-Loader-Ghidra/tree/master)
1. Download the target CMSIS file
   1. _For this example you can use: [STM32F429.svd](https://github.com/tinygo-org/stm32-svd/blob/main/svd/stm32f429.svd)_ 
2. Run SVD Loader
3. Choose SVD file
4. Confirm proper load by displaying the Memory Map
# Type Loader
This tool is made to help automate the tedious process of adding vendor specific HAL types: 
- https://github.com/So11Deo6loria/typeLoader 
