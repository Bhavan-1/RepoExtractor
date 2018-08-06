# WinDynamicDesktop
Port of macOS Mojave Dynamic Desktop feature to Windows 10

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=H8ZZXM9ABRJFU)

## How do I use this?

The first time you run WinDynamicDesktop, it will automatically download the macOS Mojave wallpapers from [here](https://files.rb.gd/mojave_dynamic.zip) and extract them to your disk. I have not included the files directly in this repository for copyright reasons. If you want to select a different set of images, see the section below for how to do so.

You will also need to input your location when running the program for the first time. This location is not used for any purpose other than to determine the times of sunrise and sunset where you live.

After you enter your location, the program will minimize to your system tray and it will run in the background. Right-clicking on the system tray icon opens a menu with options to update the location, start WinDynamicDesktop when Windows boots, or exit the program.

## Why did you develop this?

When the Dynamic Desktop feature was announced for macOS Mojave which shifts through 16 images of the same desert scene taken at different times of day, I wanted to write a Windows program that would do the same thing. Windows has the ability built-in to cycle through different wallpapers, but only at regular intervals, not based on the times of sunrise and sunset. This program adds that feature for the Mojave wallpapers to the Windows desktop.

## Can I customize the images?

Yes. By default WinDynamicDesktop uses the Mojave wallpapers, but if you create an `images.conf` file in the same folder as the EXE you can customize the images that are used. The default `images.conf` can be found [here](src/images.conf). It is formatted in JSON and must contain the following values:

* `themeName` - String which is the name of the wallpaper theme shown in the user interface
* `imagesZipUri` - String containing URL to download images.zip file from, or *null* if the content in the images subfolder is provided by the user
* `imageFilename` - String containing the filename of each wallpaper image, with `{0}` substituted for the image number
* `dayImageList` - Array of numbers listing the image numbers to display throughout the day (between sunrise and sunset)
* `nightImageList` - Array of numbers listing the image numbers to display throughout the night (between sunset and sunrise)

## Legal and privacy stuff
I do not own the Mojave wallpaper pictures used by WinDynamicDesktop, they belong to Apple. The icon used in this program was made by [Roundicons](https://www.flaticon.com/authors/roundicons) from [flaticon.com](https://www.flaticon.com/) and is licensed by [CC 3.0 BY](http://creativecommons.org/licenses/by/3.0/).

When you enter your location, WinDynamicDesktop uses the [LocationIQ service](https://locationiq.org/) to convert your location to latitude and longitude. Your location info is never sent anywhere without your consent.