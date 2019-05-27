# Setup of the environment

The installation of the ESP-ADF toolchain used in TI-2.3 consist of multiple steps. In this chapter all necessary steps will be described.

## Step 1: Make toolchain for Windows

This manual is based on the installation steps as written on the [ESP-IDF](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/windows-setup.html) website.

Windows doesn’t have a built-in “make” environment, so as well as installing the toolchain you will need a GNU-compatible environment. We use the [MSYS2](https://msys2.github.io/) environment to provide this.

The quick setup is to download the Windows all-in-one toolchain & MSYS2 zip file from dl.espressif.com:

[https://dl.espressif.com/dl/esp32_win32_msys2_environment_and_toolchain-20181001.zip](https://dl.espressif.com/dl/esp32_win32_msys2_environment_and_toolchain-20181001.zip)

Unzip the zip file to ```C:\``` (or some other location, but this guide assumes ```C:\```) and it will create an ```msys32`` directory with a pre-prepared environment.

TODO write about opening the msys32 environment.

## Step 2: Get ESP-ADF and ESP-IDF

Besides the toolchain, you also need ESP32-specific API (software libraries and source code). They are provided by Espressif in [ESP-IDF](https://github.com/espressif/esp-idf) repository. For the audio API we are using [ESP-ADF](https://github.com/espressif/esp-adf)

