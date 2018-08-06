Crankshaft = Raspberry Pi 💖 Android Auto
==

Crankshaft is a turn-key free (as in freedom) distribution for the Raspberry Pi. It transforms your Raspberry Pi to an [Android Auto headunit](https://www.android.com/auto/).

This is the source code repository, just in case you want to build the system yourself. To get the binary without dealing with all this stuff, please head to [GetCrankshaft.com](http://getcrankshaft.com). Crankshaft is possible thanks to the power of [OpenAuto](https://github.com/f1xpl/openauto) and [aasdk](https://github.com/f1xpl/aasdk). Crankshaft and OpenAuto are in no way related or certfied by either Google or Android.



Getting Started
--

It's easy to get started even when you're new to Raspberry Pi and know nothing about electronics. [Check here for the latest guide](https://github.com/htruong/crankshaft/wiki/Getting-started-with-Crankshaft). 

**Where to get help**: The premier place to discuss your question or idea is [the subreddit (BETA)](https://www.reddit.com/r/crankshaft/). 

**FAQs**: Several other questions such as "Does OK Google work? Can I use a custom screen?" get asked a lot and might have already been answered in the [tips and tricks](https://github.com/htruong/crankshaft/wiki/Hidden-tips,-tricks,-settings,-etc.) page. If you have questions, [check out the growing FAQs](https://github.com/htruong/crankshaft/wiki/Frequently-Asked-Questions).

**Project pictures**: If you have pictures of your project, feel free to [add to the collection](https://photos.app.goo.gl/81hQ6wTuLFNGmRHh2).


**Touchscreens**: If you don't have the official touch screen and just want to see whether Crankshaft will work with the phone you have before spending money to buy the screen, try [this trick](https://github.com/htruong/crankshaft/wiki/Frequently-Asked-Questions#i-have-a-pi3-how-can-i-test-crankshaft-compatibility-with-my-phone-before-i-spend-the-money-to-buy-the-official-screen).

**Phones and Pi combinations**: If you want to know for sure or have a chance to try it, please spend a minute to report back whether it works or not at [Hardware Compatibility List](https://github.com/htruong/crankshaft/issues/2). If Crankshaft doesn't work but you're capable of compiling software on Linux, there is a chance chance you can get it to work [following OpenAuto's simple intructions](https://github.com/htruong/crankshaft/issues/2).



**Problems and requests**: To file a bug or an enhancement idea, please file an issue on this repository. To help us help you, before reporting problems to this repository, I would appreciate if you could try [running Crankshaft under X11](https://github.com/htruong/crankshaft/wiki/Crankshaft-dev-mode). This will help in cases you use non standard hardware, for example, a custom HDMI screen. To make the distribution easier and lightweight, by default I opted to run OpenAuto under EGL instead of relying on X11, and this might cause OpenAuto to behave in ways that OpenAuto's author rather not deal with :)


How to build a Crankshaft image
--

Please see `COMPILE.md`.



Release Highlights
--

[Full Changelog](https://github.com/htruong/crankshaft/blob/master/CHANGELOG.md)

#### Version alpha0.2.4 2018-05-18

What's new:

- Syncs with latest OpenAuto and AASDK.
- Buttons now look a bit nicer.
- Featured default wallpaper: Eve's "Camping (with Dock)"!
- Dev mode does not shut down crankshaft on ntp sync anymore.

What's new for developers:

- Now you can build your own Crankshaft system on raspbian \
  Use the scripts in `rpi_buildsystem`.
- The crankshaft buildscript is improved.
- Wifi client is supported in dev mode.
- Watchdog module is fixed & really enabled.
- Dev mode will have ntp enabled.

Known issues:

- If Android Auto doesn't automatically launch, disable Android debug.
- X11 still does not show cursors on projection mode, so no mouse.
- X11 will activate screensaver if not touched for 10 minutes.

#### Version alpha0.2.3 2018-04-18

What's new:

- Now you can configure many of the settings normally you have to use hardware jumpers\
  through software settings. Open the file `/boot/crankshaft/crankshaft_env.sh` to edit.
- Startup scripts via `/boot/crankshaft`. You can use both bash and python.
- Triggerhappy actions are exposed now via `boot/crankshaft/triggerhappy.conf`
- Fix "Crankshaft shuts down immediately after NTP time sync" when you set \
  `NO_CONNECTION_POWEROFF_MINS` on `crankshaft_env.sh` to 0. Fix #77.
- Some minor bug fixes: 
  Now crankshaft should mount `boot` and `root` ro correctly.\
  Video FPS is 30 by default for now (less janky animations).

What's new for developers:

- Clearer image building instructions.

Known issues:

- If Android Auto doesn't automatically launch, disable Android debug.
- X11 still does not show cursors on projection mode, so no mouse.




Other projects
--

OpenAuto and Crankshaft are not the only people in this world experimenting with this idea. 

Some other developers worked hard on this too, and you might want to give them a try. [Here is another solution that works on the Pi](https://github.com/viktorgino/headunit-desktop), [here is one that works on an Android tablet](https://github.com/borconi/headunit).

*Conflicts of interests*: Huan Truong is a independent developer he declares no business relationship as well as no conflicts of interests between him and the following entities: Google, Android, OpenAuto/aasdk, Michal Swaz, Viktor Gino, Emil Borconi-Szedressy.
