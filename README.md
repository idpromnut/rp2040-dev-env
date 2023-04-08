# rp2040-dev-env

Basic RP2040 development environment.

# Firmware

## Dev Tool Setup

### _VSCode_

Install [VSCode](https://code.visualstudio.com/download)

### _VSCode Plugins_

- [C/C++ from Microsoft](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
- [CMake Tools from Microsoft](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)
- [CMake Language support](https://marketplace.visualstudio.com/items?itemName=twxs.cmake)


## Windows (10)

### Install dependencies

- [GNU Arm toolchain](https://developer.arm.com/downloads/-/gnu-rm)
- [MinGW](https://github.com/niXman/mingw-builds-binaries/releases)
- [CMake](https://cmake.org/download/)
- [Python](https://www.python.org/downloads/)
- [Git](https://git-scm.com/download/win)


### Install RP2040 Build Tools

```
git clone -b master "https://github.com/raspberrypi/pico-sdk"
cd pico-sdk 
git submodule update --init 
cd ..
git clone -b master "https://github.com/raspberrypi/pico-examples"
```

### Configure VSCode

#### Configure CMake

In *CMake Tools*, select Extension Settings and navigate to "Cmake: Build Environment". Add PICO_SDK_PATH and set it to the location that you installed the PICO SDK (in the above step). This should be in the directory that you ran the above script in. Add the same PICO_SDK_PATH + path into the "Cmake: Configure Environment".

Navigate to "Cmake: Cmake Path". Enter in the path to the Cmake binary.

Navigate to "Cmake: Generator" and enter "MinGW Makefiles"


## Linux (Debian)

### Install RP2040 Build Tools

```
wget https://raw.githubusercontent.com/raspberrypi/pico-setup/master/pico_setup.sh
chmod +x pico_setup.sh
 ./pico_setup.sh
sudo reboot
```
### Configure VSCode

#### Configure SDK path

In *CMake Tools*, select Extension Settings and navigate to "CMake: Build Environment". Add PICO_SDK_PATH and set it to the location that you installed the PICO SDK (in the above step). This should be in the directory that you ran the above script in.

Navigate to the "CMake: Generator" and select "Unix Makefiles".

Close the settings.

### Project

Add code + basic CMake file.

#### Build

1. At the bottom of VS Code, you should see a blue status bar. If you installed CMake Tools, it should be populated with extra CMake functionality.
2. Click No active kit to bring up a drop-down menu at the top of VS Code. Click _Scan for kits_. When this is done, click No active kit again. You should see your installed GNU Toolchain compiler available as an option. Click it (GCC for arm- none-eabi) to set the compiler for your build process.
3. On the same status bar, click Cmake: [Debug]: Ready, and click Debug in the drop-down menu that appears at the top of VS Code. This should run CMake and create a build directory in your project folder.
4. Click the Build button in the status bar (at the bottom of the window). This will call make to build your project. You should see new, compiled binaries appear in the build folder.

#### Upload

1. The easiest method of uploading your compiled program is to use the UF2 bootloader that comes with the Pico.
2. Make sure the USB cable is not plugged into your Pico. Press the BOOTSEL button and hold it down while plugging the USB cable into the Pico. Once the USB cable is attached, release the BOOTSEL button.
3. The Pico should enumerate as a storage device named RPI-RP2 on your computer.
4. Navigate into your build folder. Copy blink.uf2 (unfortunately, copying files from within VS Code does not work--you will have to do it from a file explorer window). Paste the file into the top level of your RPI-RP2 drive.
5. The Pico should automatically reboot and begin running your code.


## Resources

1. [https://www.digikey.ca/en/maker/projects/raspberry-pi-pico-and-rp2040-cc-part-1-blink-and-vs-code/7102fb8bca95452e9df6150f39ae8422](https://www.digikey.ca/en/maker/projects/raspberry-pi-pico-and-rp2040-cc-part-1-blink-and-vs-code/7102fb8bca95452e9df6150f39ae8422)
2. [https://www.youtube.com/watch?v=BAoTBg8MJJ4&ab_channel=JoeJackson](https://www.youtube.com/watch?v=BAoTBg8MJJ4&ab_channel=JoeJackson)


