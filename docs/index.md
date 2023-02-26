---
layout: page
title: Matter Room Climate
---

# Smart hygrometer / thermometer 

* Matter (high level protocol) via thread
* Seeed Studio XIAO nRF52840 micro controller


## Border router

* Raspberry Pi 3b as border router
    * Debian 11 Bullseye (Raspberry Pi OS Lite)
* Nordic Semiconductor nRF52840 dongle for thread connectivity
* nRF Connect SDK

### nRF Connect SDK
We'll need the nRF Connect SDK and some tools to set up the border router and also later for developing our devices. We can mostly follow Nordic's documentation on the [SDK installation](https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/getting_started/assistant.html) here, although some distributions might provide packages for some of these tools, that you then can install in the usual way.

The easy way to manage the nRF SKDs is the nRF Connect for Desktop application from Nordic Semi. They provide an [AppImage on their website](https://www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-Desktop/Download) that should run on most systems (Alternatively check [the documentation](https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/getting_started/installing.html) on how to set it up manually).

You'll also have to install [SEGGER J-Link](https://www.segger.com/downloads/jlink/).

In the nRF Connect for Desktop app, download and open the Toolchain Manager. This is where we can download and manage nRF SDKs and Toolchains. You can probably just choose the latest stable version. In my case this was nRF Connect SDK v2.2.0.

The documentation mentions that you can either set up your build environment for using the command line or use their VSCode extensions. Although I'd go for the VSCode extensions here, it seems like it's still required to install the [nRf Command Line Tools](https://www.nordicsemi.com/Products/Development-tools/nrf-command-line-tools).

Nordic Semi offers a few VSCode extensions to make your live easier. You can either use the *nRF Connect for VS Code Extension Pack* or let the Toolchain Manager handle the installation for you.

So, now we are good to go.

### nRF dongle as Radio Co-Processor
Our Raspberry Pi needs IEEE 802.15.4 connectivity to work as our Thread border router, so we have to flash our nRF dongle with some firmware to make it into a
[radio co-processor](https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/protocols/thread/tools.html#configuring-a-radio-co-processor).

In addition to the toolchain we downloaded in the last step, we'll need the [nrfutil](https://www.nordicsemi.com/Products/Development-tools/nrf-util) command line tool.

> ⚠️ The old nrfutil python tool that is available in some repositories [is deprecated](https://github.com/NordicSemiconductor/pc-nrfutil#deprecation-notice) and didn't work for me.
