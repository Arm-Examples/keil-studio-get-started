# keil-studio-get-started
Get started example for use in Keil Studio

## How to setup your Development Environment using Keil Studio VSCode Extension:
1. Download & Install [Microsoft Visual Studio Code](https://code.visualstudio.com/download) for your operating system.
2. Launch Visual Studio Code. From the 'View' menu open 'Extensions' (ctrl+shift+x). Search for "Keil Studio Pack" and select the install button.
3. From the 'View' menu open 'Source Control'. Select 'Clone Repository' and copy the url for this repo: https://github.com/Arm-Examples/keil-studio-get-started into the input dialog
4. Specify the destination folder to clone to and select 'Open' when asked 'Would you like to open the cloned directory?'
5. Open the 'Explorer' view (ctrl-shift-e) and select the file 'vcpkg-configuration.json'. This file instructs [Microsoft vcpkg](https://github.com/microsoft/vcpkg-tool#vcpkg-artifacts) to install the prerequisite artifacts required by the 'Arm CMSIS csolution' extentsion for building the projects of the solution.
    - ctools: [CMSIS-Toolbox](https://github.com/Open-CMSIS-Pack/devtools/blob/main/tools/projmgr/docs/Manual/Overview.md)
    - cmake 
    - ninja 
    - gcc: arm-none-eabi-gcc (GNU Arm Embedded Toolchain)
6. In case vcpkg shows an error in the VSCode status bar, you can see furth information in the "OUTPUT" for 'vcpkg'.
In case of 'Error: Unable to resolve dependency ... in <registry>' you may need to update the registry by running 'vcpkg: Run vcpkg command'
from the 'View' menu's 'Command Palette...' (ctrl+shift+p) typing: `z-ce update <registry>`. 
7. By default the 'Arm CMSIS csolution' extension is configured to automatically convert *.csolution.[yml|yaml] files into a *.cprj file for each 'context' of the solution. If you do not see any *.cprj file side by side the 'hello.cproject.yml' you can right click on the 'get-started.csolution.yml' file in the 'Explorer' View and run 'convert'. The convert command may fail due to missing packs. In this case run the command 'CMSIS: Install required packs for the active solution' from the 'Command Palette' (ctrl-shift-p).
8. Open the 'CMSIS' view from the side bar and press the 'Build' button. The last line of the ninja build output will tell you where you can
find the application elf file. Alternatively you can select 'Build' or 'Rebuild' from the context menu of the `*.cprj` file of the solution context
(e.g. hello.debug+avh.cprj)

Note: Any terminal that is openened within VSCode after vcpkg got activated for the folder, will have all the above tools added to the path. 
This allows you to run tools from the [CMSIS-Toolbox](https://github.com/Open-CMSIS-Pack/devtools/blob/main/tools/projmgr/docs/Manual/Overview.md) like:
- [`cpackget`](https://github.com/Open-CMSIS-Pack/cpackget#usage) for installing and uninstalling CMSIS-Packs
- [`csolution`]() for updating, validating and converting from the CMSIS Project Management [YML input format](https://github.com/Open-CMSIS-Pack/devtools/blob/main/tools/projmgr/docs/Manual/YML-Input-Format.md#yaml-input-format)
  to the CMSIS Build [XML `cprj` format](https://open-cmsis-pack.github.io/devtools/buildmgr/latest/element_cprj.html) used by `cbuildgen`.
- [`cbuildgen`](https://open-cmsis-pack.github.io/devtools/buildmgr/latest/cbuildgen.html#cbuildgen_invocation) 
- [`cbuild`](https://github.com/Open-CMSIS-Pack/cbuild#usage) for an orchestrated build of one or more `configurations` of a csolution.

## Execute Project

The project is configured for execution on Arm Virtual Hardware (AVH) modelling an MPS2 board running an Arm Cortex-M3 processor. This model is part of the Keil MDK Professional Edition for Windows and removes the requirement for a physical hardware board.

```bash
./ $ VHT_MPS2_Cortex-M3 -f vht-config.txt -a ./out/hello/AVH/Debug/hello.elf
```
