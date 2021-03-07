# Install and Create Emulators using AVDMANAGER and SDKMANAGER

## TL;DR

For generic skin emulator with default apis (without google apis):

1. **List All System Images Available for Download:** `sdkmanager --list | grep system-images`

2. **Download Image:** `sdkmanager --install "system-images;android-29;default;x86"`

3. **Create Emulator:** `echo "no" | avdmanager --verbose create avd --force --name "generic_10" --package "system-images;android-29;default;x86" --tag "default" --abi "x86"`

       I recommend adding these lines to: ~/.android/avd/generic_10.avd/config.ini

       skin.name=1080x1920        # proper screen size for emulator
       hw.lcd.density=480
       hw.keyboard=yes            # enables keys from your laptop to be sent to the emulator
       
       If you cannot do this, you can still pass -skin 1080x1920 as an argument when starting the emulator. 

4. **Run Emulator:** `emulator @generic_10 &`

## About

- The goal of this gist is to quickly pre-install a range of system images to provide our project teams the ability to run emulators on a range of API levels, from API 19 to API 28.
  - These can be run locally or on the base build agent.
- **Note:** X86 is the fastest architecture for emulators, though x86_64 would probably be better to test against because most phones are 64 bit now.
- We create two sets of emulators here, one set with pixel hardware emulation and one set with default oem emulation.

See: [Google Documentation on Start the emulator from the command line](https://developer.android.com/studio/run/emulator-commandline) for more info

## Steps

1) Run the **sdkmanager --install** commands.
2) Run the **avdmanager** commands.

## Extra Steps

- Add aliases to run the emulators with parameters more easily. Or add these parameters to your build steps in TeamCity.
  - Instead of using `emulator @{EMULATOR NAME}` to run devices, you can use the aliases if they are added.
- If you run this locally, you can use the `-read-only` parameter to run multiple devices at the same time. You can then manually run automation against various APIs for added device coverage during regression.

## Step 1 - Run the sdkmanager commands

### KITKAT (4.4) API 19

`sdkmanager --install "system-images;android-19;google_apis;x86"`

### LOLLIPOP (5.0) API 21

`sdkmanager --install "system-images;android-21;google_apis;x86"`

### LOLLIPOP (5.1) API 22

`sdkmanager --install "system-images;android-22;google_apis;x86"`

### MARSHMELLOW (6.0) API 23

`sdkmanager --install "system-images;android-23;google_apis;x86"`

### NOUGAT (7.0) API 24

`sdkmanager --install "system-images;android-24;google_apis;x86"`

### NOUGAT (7.1) API 25

`sdkmanager --install "system-images;android-25;google_apis;x86"`

### OREO (8.0) API 26

`sdkmanager --install "system-images;android-26;google_apis;x86"`

### OREO (8.1) API 27

`sdkmanager --install "system-images;android-27;google_apis;x86"`

### PIE (9.0) API 28

`sdkmanager --install "system-images;android-28;google_apis;x86"`

## Step 2 - Use AVDMANAGER to create emulators

### Pixel Emulator with Google Apis and x86 architecture

`echo "no" | avdmanager --verbose create avd --force --name "pixel_4.4" --device "pixel" --package "system-images;android-19;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "pixel_5.0" --device "pixel" --package "system-images;android-21;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "pixel_5.1" --device "pixel" --package "system-images;android-22;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "pixel_6.0" --device "pixel" --package "system-images;android-23;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "pixel_7.0" --device "pixel" --package "system-images;android-24;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "pixel_7.1" --device "pixel" --package "system-images;android-25;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "pixel_8.0" --device "pixel" --package "system-images;android-26;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "pixel_8.1" --device "pixel" --package "system-images;android-27;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "pixel_9.0" --device "pixel" --package "system-images;android-28;google_apis;x86" --tag "google_apis" --abi "x86"`

### Generic Emulator with Google Apis

`echo "no" | avdmanager --verbose create avd --force --name "generic_4.4" --package "system-images;android-19;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "generic_5.0" --package "system-images;android-21;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "generic_5.1" --package "system-images;android-22;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "generic_6.0" --package "system-images;android-23;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "generic_7.0" --package "system-images;android-24;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "generic_7.1" --package "system-images;android-25;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "generic_8.0" --package "system-images;android-26;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "generic_8.1" --package "system-images;android-27;google_apis;x86" --tag "google_apis" --abi "x86"`

`echo "no" | avdmanager --verbose create avd --force --name "generic_9.0" --package "system-images;android-28;google_apis;x86" --tag "google_apis" --abi "x86"`

## Extra Steps - Aliases and notes on resolutions

### Aliases to run emulators more optimally

**Note:** Add this alias to `~/.bashrc` or `~/.zshrc`, or just run using these parameters for best results. `-skin 768x1280` is useful to run default emulators successfully because they have a very low resolution out-of-the-box.

`alias generic_4.4='emulator @generic_4.4 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 768x1280 &'`

`alias generic_5.0='emulator @generic_5.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 768x1280 &'`

`alias generic_5.1='emulator @generic_5.1 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 768x1280 &'`

`alias generic_6.0='emulator @generic_6.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 768x1280 &'`

`alias generic_7.0='emulator @generic_7.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 768x1280 &'`

`alias generic_7.1='emulator @generic_7.1 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 768x1280 &'`

`alias generic_8.0='emulator @generic_8.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 768x1280 &'`

`alias generic_8.1='emulator @generic_8.1 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 768x1280 &'`

`alias generic_9.0='emulator @generic_9.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 768x1280 &'`

**Note:** Add this alias to `~/.bashrc` or `~/.zshrc`, or just run using these parameters for results. Pixel emulators should run at default resolution of 1080x1920 by default, but can specify this just in-case with the parameter: `-skin 1080x1920`

`alias pixel_4.4 ='emulator @pixel_4.4 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 1080x1920 &'`

`alias pixel_5.0 ='emulator @pixel_5.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 1080x1920 &'`

`alias pixel_5.1 ='emulator @pixel_5.1 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 1080x1920 &'`

`alias pixel_6.0 ='emulator @pixel_6.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 1080x1920 &'`

`alias pixel_7.0 ='emulator @pixel_7.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 1080x1920 &'`

`alias pixel_7.1 ='emulator @pixel_7.1 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 1080x1920 &'`

`alias pixel_8.0 ='emulator @pixel_8.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 1080x1920 &'`

`alias pixel_8.1 ='emulator @pixel_8.1 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 1080x1920 &'`

`alias pixel_9.0 ='emulator @pixel_9.0 -no-boot-anim -netdelay none -no-snapshot -wipe-data -skin 1080x1920 &'`

**Note** You can run all of the emulators above with a `-read-only` parameter to run multiple emulators at the same time, but this is an experimental feature right now.

## Other

1) Certain emulators, like Pixel, need to be started at a higher resolution than default oem emulators. Either define this in the `~/.android/avd/{name of avd}/config.ini` file, or start emulator with `-skin {RESOLUTION}` as seen above.
2) `emulator -list-avds` will print list of available devices
3) `avdmanager list` , `avdmanager list target`, `avdmanager list devices` , `avdmanager list avd`

``` text
-   avdmanager list              : Lists existing targets or virtual devices.
-   avdmanager list avd          : Lists existing Android Virtual Devices.
-   avdmanager list target       : Lists existing targets.
-   avdmanager list device       : Lists existing devices.
```
