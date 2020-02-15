[![Build Status](https://travis-ci.org/trentmillar/platformio-qs.svg)](https://travis-ci.org/trentmillar/platformio-qs)
# PlatformIO Quick Start 
Simple quick start "blink" using PlatformIO on boards: `Uno`, `DOIT ESP32 DevKit v1`, `NodeMCU v1.0 (ESP-12E)` 

## Pre steps

#### Did you install PlatformIO's CLI?

##### on mac,
1. `pip install -Upip3 install -U https://github.com/platformio/platformio-core/archive/develop.zip`
2. `vi ~/.bashrc` (or .profile or zshrc...) and add `EXPORT = PATH="$PATH:~/.platformio/penv/bin"`
3. close your terminal and reopen or `source ~/.bashrc` to reload the PATH
4. (optional) activate the virtual environment, `. activate` which should now be in the PATH
5. can you run the cli? `pio`? if not go here, https://docs.platformio.org/en/latest/installation.html

#### PlatformIO extension to VSCode
1. Just search for and install the extension `PlatformIO`
2. Open `settings.json` in VSCode (from the Command Palette type `Preferences Open Settings (JSON)`)
3. Add the following (inside `{...}`),
   ```
    "platformio-ide.customPATH": "~/.platformio/penv/bin",
    "platformio-ide.useDevelopmentPIOCore": true
   ```
    **note**, customPATH probably isn't necessary since we added it to the `PATH` 
4. Restart VSCode

## Setting up the project

The following is based on, https://docs.platformio.org/en/latest/quickstart.html

In step 3 the three boards are boards I am planning on using in this project. To use other boards just run `pio boards` and find the **ID** of the boards(s)

1. Open VSCode then open the folder the project will live
2. Open a terminal (preferably in VSCode) can `cd` to your working folder
3. run `pio project init -b esp32doit-devkit-v1 -b nodemcuv2 -b uno`
   - this will create a new file *platformio.ini* a Travis CI file, and some scaffolding, *include, src, lib, test* folders
4. confirm the *platformio.ini* contains the boards,
    ```
    [env:esp32doit-devkit-v1]
    board = esp32doit-devkit-v1
    framework = arduino
    platform = espressif32

    [env:nodemcuv2]
    board = nodemcuv2
    framework = arduino
    platform = espressif8266

    [env:uno]
    board = uno
    framework = arduino
    platform = atmelavr
    ```

## Running/Uploading the program to a board
1. use the cli an run , `pio run` this will take a minute to fetch the board firmware and build it. Look in the newly created folder */.pio* to see what is pulled down
2. once everything is built then you need to upload the program (*/src/main.cpp*) to a board, this example uploads to the ESP8266 board, `pio run -e nodemcuv2 -t upload`. Note, if you have all your boards connected via a serial port then you don't need to specify `-e` or which environment to upload to
   
That is it, your board should be flashing. Note, in *main.cpp* your LED_BUILTIN pin may be 13 (Uno), verify your board's schematics for the pin usage.

## Notes
This project doesn't need VSCode or the PlatformIO extension in VSCode. If you look closely at the commands executed, all that is needed is PlatformIO Core and the included CLI.