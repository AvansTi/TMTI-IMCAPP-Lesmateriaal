# Setup of the compiler environment

The installation of the ESP-ADF toolchain used in TI-2.3 consist of multiple steps. In this chapter all necessary steps will be described.

## Step 1: Make toolchain for Windows

This manual is based on the installation steps as written on the [ESP-IDF](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/windows-setup.html) website.

Windows doesn’t have a built-in “make” environment, so as well as installing the toolchain you will need a GNU-compatible environment. We use the [MSYS2](https://msys2.github.io/) environment to provide this.

The quick setup is to download the Windows all-in-one toolchain & MSYS2 zip file from dl.espressif.com:

[https://dl.espressif.com/dl/esp32_win32_msys2_environment_and_toolchain-20181001.zip](https://dl.espressif.com/dl/esp32_win32_msys2_environment_and_toolchain-20181001.zip)

Unzip the zip file to ```C:\``` (or some other location, but this guide assumes ```C:\```) and it will create an ```msys32``` directory with a pre-prepared environment.

TODO write about opening the msys32 environment.

## Step 2: Get ESP-ADF and ESP-IDF

Besides the toolchain, you also need ESP32-specific API (software libraries and source code). They are provided by Espressif in [ESP-IDF](https://github.com/espressif/esp-idf) repository. For the audio API we are using [ESP-ADF](https://github.com/espressif/esp-adf)

To get AvansTi specific version of this libraries you have to use the following forked github page [ESP-ADF](https://github.com/AvansTi/esp-adf)

After installating the toolchain, you have to nativate to ```C:\msys32\home\USERNAME\```, where you have to change ```USERNAME``` to your username.

TODO

## Step 3: Set Environment Variables

The toolchain uses the environment variable ```IDF_PATH``` to access the ESP-IDF directory and the environment variable ```ADF_PATH``` to access the ESP-IDF directory. These variables should be set up on your computer, otherwise projects will not build.

These variables can be set temporarily (per session) or permanently. Please follow the instructions

### Windows

The user profile scripts are contained in ```C:/msys32/etc/profile.d/``` directory. They are executed every time you open an MSYS2 window.

1. Create a new script file in ```C:/msys32/etc/profile.d/``` directory. Name it ```export_idf_path.sh```.
2. Identify the path to ESP-IDF directory. It is specific to your system configuration and may look something like ```C:\msys32\home\USERNAME\esp\esp-idf```
3. Add the export command to the script file, e.g.:
```output
export IDF_PATH="C:/msys32/home/USERNAME/esp/esp-adf/esp-idf"
export ADF_PATH="C:/msys32/home/USERNAME/esp/esp-adf"
```
Remember to replace back-slashes with forward-slashes in the original Windows path.
4. Save the script file.
5. Close MSYS2 window and open it again. Check if ```IDF_PATH``` and ```ADF_PATH``` is set, by typing:

```output
printenv IDF_PATH
printenv ADF_PATH
```

The path previusly entered in the script file should be printed out.

If you do not like to have IDF_PATH set up permanently in user profile, you should enter it manually on opening of an MSYS2 window:

```output
export IDF_PATH="C:/msys32/home/USERNAME/esp/esp-adf/esp-idf"
export ADF_PATH="C:/msys32/home/USERNAME/esp/esp-adf"
```

## Step 4. Install the Required Python Packages

TODO: IS DIT NODIG? Checken op clean PC.

The python packages required by ESP-IDF are located in ```IDF_PATH/requirements.txt```. You can install them by running:

```output
python -m pip install --user -r $IDF_PATH/requirements.txt
```

>Please check the version of the Python interpreter that you will be using with ESP-IDF. For this, run the command ```python --version``` and depending on the result, you might want to use `python2`, `python2.7` or similar instead of just `python`, e.g.:
{: .tip}

## Step 5. Start a Project

Now you are ready to prepare your application for ESP32. You can start with `get-started/hello_world` project from examples directory in IDF.

Copy `esp-adf/esp-idf/examples/get-started/hello_world` to the `~/esp` directory:

