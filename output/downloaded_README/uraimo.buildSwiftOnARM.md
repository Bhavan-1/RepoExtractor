🚨**WIP**: Use the [swift-3.1.1](https://github.com/uraimo/buildSwiftOnARM/tree/3.1.1) branch for a stable release, check out the [issues](https://github.com/uraimo/buildSwiftOnARM/issues) to verify the current status.🚨

# Building Swift on ARM

A few, very simple, bash scripts to clone, configure and build Swift 4.1.2 on ARM devices. 

Derived from [package-swift](https://github.com/iachievedit/package-swift) by [@iachievedit](https://twitter.com/iachievedit), some patches from [swift-arm](https://github.com/swift-arm/) by [@hpux735](https://twitter.com/hpux735), support for 4.1 derived from the work of [@chnmrc](https://github.com/chnmrc/swift4arm).

## Supported Architectures

* ✅ ARMv7 (RaspberryPi 2/3, ODroid, CHIP, etc...)
* ✅ ARMv6 (Original RaspberryPi, Pi Zero, etc... )
* ✅ aarch64 (Pine64, etc...)

## Prebuilt binaries

Swift 4.1.2 armv7(RaspberryPi 2/3)  or Ubuntu Mate 16.04.4 is available [here](https://www.dropbox.com/s/f6g1kw02w0cjq5w/swift-4.1.2-RPi23-Ubuntu1604_b3.tgz?dl=0) or [here](https://www.dropbox.com/s/zs7kf3clc43e93j/swift-4.1.2-RPi23-RaspbianStretch_b3.tgz?dl=0) for Raspbian Stretch. See the required dependencies below.

## Instructions

For the latest updates on Swift on ARM, check out my blog [here](https://www.uraimo.com/category/raspberry/).

Check out Helge Heß's project [dockSwiftOnARM](https://github.com/helje5/dockSwiftOnARM) to build Swift in a Docker container or to [build a cross-compiling toolchain](https://github.com/AlwaysRightInstitute/swift-mac2arm-x-compile-toolchain) that will allow you to build arm binaries directly from your Mac using a precompiled swiftc for ARM.

The scripts:

- clone.sh - Install dependencies and clones the main Swift repository and all the related projects

- checkoutRelease.sh - Resets all repos, updates them, checks out a specific tag (4.1.1 at the moment) and apply the patches

- build.sh - Build

- clean.sh - Clean all build artifacts 


## Building instructions

First of all, use a suitably sized sd-card, at least 16Gb in size.

Configure a swap file of at least 3Gb, on Ubuntu:

    sudo fallocate -l 3G swapfile
    sudo chmod 600 swapfile
    sudo mkswap swapfile
    sudo swapon swapfile
    
You'll need to manually enable the swap file with `swapon` *each time you reboot* the RaspberryPi (or the system will just run without swap).

On Raspbian, open `/etc/dphys-swapfile` and edit:

    CONF_SWAPSIZE=2048
    
Save the file and:

    sudo /etc/init.d/dphys-swapfile stop
    sudo /etc/init.d/dphys-swapfile start
    
Now, call the included scripts as follows:

1. Launch `clone.sh` that will install the required dependencies (_git cmake ninja-build clang-3.8 python uuid-dev libicu-dev icu-devtools libbsd-dev libedit-dev libxml2-dev libsqlite3-dev swig libpython-dev libncurses5-dev pkg-config libblocksruntime-dev libcurl4-openssl-dev autoconf libtool systemtap-sdt-dev libcurl4-openssl-dev libz-dev_), fix clang links and clone apple/swift with all its dependecies.

2. Run `checkoutRelease.sh` that will select the current release (4.1.1) and apply the needed patches. These patches cover the basic Raspi2/3 with Xenial case, but I've had many reports of successful build on different setups, but beware, additional patches could  be needed on different boards/OSs.

3. Once done, start the build with `build.sh`.

4. Once the build completes a few hours later, you'll have a `swift-4.1.1.tgz` archive containing the whole Swift compiler distribution. Once decompressed you'll find the Swift binaries under `usr/bin`.

I recommend to perform all these operations in a permanent background `tmux` or `screen` session (`CTRL+B d` to detach from the session and `tmux a` to reattach to it when you ssh again into the RaspberryPi).

Additional steps could be required in some cases (on a RaspberryPi 1 or for Raspbian) [check the latest ARM posts on my blog for additional info](https://www.uraimo.com/category/raspberry/).

To build a different release than the one currently configured in the script, open `checkoutRelease.sh` and `build.sh` and modify the variables on top, with the branch name for the release and the release name for the tgz respectively.

## Previous Releases

You can compile old releases checking out the specific tag:

* [Swift 3.1.1](https://github.com/uraimo/buildSwiftOnARM/tree/3.1.1)
* [Swift 3.1](https://github.com/uraimo/buildSwiftOnARM/tree/3.1)
* [Swift 3.0.2](https://github.com/uraimo/buildSwiftOnARM/tree/3.0.2)

