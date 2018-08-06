# Welcome

## Picroft - 2018-3-14 "Pi Day" release!
The Picroft project is an enclosure for a stock Raspberry Pi connected to a speaker and basic USB microphone.  This is built around a Raspbian Jessie Lite installation.  The entire project is available as a pre-built micro-SD image ready to be burned and placed into a Raspberry Pi.  You can download the pre-built image here:

 [![Download img](https://github.com/MycroftAI/enclosure-picroft/raw/master/microsd-icon.png "Download img") Picroft 2018-3-14 image](https://mycroft.ai/to/picroft-image)
 
SHA256 checksum for the `raspbian_Picroft_2018-03-14.zip` image:
```32864c5da8e5d84d91554a6b0e9240271fbc1af147b44ac7ac7e77e57c7614ea```

## Requirements

* Raspberry Pi 3 (Older versions do not have sufficient processing power, and if they work they will be very slow)
* MicroSD Card (8 GB or larger)
* Any analog speaker
* USB Microphone.  Tested with CM108-based microphones.

## Installation

[Official Raspberry Pi Image Installation Instuctions](https://www.raspberrypi.org/documentation/installation/installing-images/)

[Etcher](https://etcher.io/) Cross-Platform GUI SD card creator for RPi

### Advanced Installation
- [Windows](https://www.raspberrypi.org/documentation/installation/installing-images/windows.md)
- [OSX/MacOS](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)
- [Linux](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md)

## Usage

Upon boot, Picroft will search for an Ethernet connection.  If none is found, the Wifi Setup process will begin to get the device connected to any available network.

Once connected, you must pair the device at https://home.mycroft.ai using the code spoken by the device.  You can also read the code on the screen.

After that, you can simply speak to Picroft as you would to any Mycroft implementation.  For example:

  "Hey Mycroft, what time is it?"
  "Mycroft, how tall was Abraham Lincoln?"


## Old Versions
* [2018-03-14](https://drive.google.com/a/mycroft.ai/uc?id=177BGTTOHUlFsij1mSLi-IJZ87xf9s982&export=download)
  - Corrected auto_run.sh typo, -ne instead of -eq was preventing script updates
  - Turned off “wait for network” in raspi-config
  - Updated to mycroft-core 18.2.2
  - SHA256: ```32864c5da8e5d84d91554a6b0e9240271fbc1af147b44ac7ac7e77e57c7614ea```
* [0.9.1](https://drive.google.com/a/mycroft.ai/uc?id=0Bzao3lLsdthPaE1VWXRzRUVsWWM&export=download)
  - Preloaded with mycroft-core 0.9.14
  - better pairing
  - launch CLI after boot
  - SHA256: ```d3041e41e7b6f1ca4f4b9ad3b4a665702b9dc32b285884d9bfdad8aefb9b788d```
* [0.9](https://drive.google.com/a/mycroft.ai/uc?id=0Bzao3lLsdthPZUNneUg5djhtTGM&export=download)
  - Preloaded with 17.08a
  - auto-upgrading from this repo
* [0.8](https://rebrand.ly/Picroft-0_8)
  - Switch to Home backend
* [0.5.1](https://rebrand.ly/Picroft-0_5_1)
  - Fixed several audio issues with 0.5 image
* 0.5
  - Original image
  - Connected to Cerberus backend

## Help and more info
Check out the project wiki [here](https://github.com/MycroftAI/enclosure-picroft/wiki).  
There's also the general [Documentation](https://docs.mycroft.ai/).

## There are two scripts run on startup
* `audio_setup.sh` configures your specific audio setup.
* `custom_setup.sh` is a stub meant to initialize any other IoT devices or services you might need like a DLNA server or syslog for example.

## Using USB Audio as Output

Typically the USB audio should be connected to hwplug:1,0 but to verify run the following:

`aplay -L`

Find the hwplug output for the device you want to use, take this and update the /etc/mycroft/mycroft.conf file accordingly:

"play_wav_cmdline": "aplay -Dhw:0,0 %1" this line now becomes "play_wav_cmdline": "aplay -Dplughw:1,0 %1"

You can now run ./auto_run.sh to start the program back up and test and ensure the output comes through the USB speakers.

---

There is an active *Picroft* community within the [Mycroft's Mattermost](https://chat.mycroft.ai/community/channels/picroft) which are welcome to join!
