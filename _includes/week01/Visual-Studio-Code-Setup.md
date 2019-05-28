# Setup Visual Studio Code

After installing all the tools necessary for building the software, it's now time to install the IDE for editting the code. It's recommanded to use Visual Studio Code as programming environment since it well integrate with the ESP build tools.

## Step 1: Install and download Visual Studio Code

Visual Studio Code is a light-weight,open source and platform independed IDE developed by Microsoft. The latest version is available at [https://code.visualstudio.com/](https://code.visualstudio.com/). Please download and install Visual Studio Code.

## Step 2: Configuring Visual Studio code

After the installation you have to start Visual Studio code and install the essential extensions.

### Step 2.1. Extensions

1. C/C++ (Author: Microsoft)
2. Native Debug (Author: WebFreak)

TODO add image and explaination.

### Step 2.2. Project settings

First, we create a new project in VS Code, using `esp-adf\esp-idf\examples\get-started\blink`. Put `blink` project into anywhere you want, and open this folder in VS Code.

#### IntelliSense

To enable code completion and navigation, we need to generate a `c_cpp_properties.json` file first. Enter `Ctrl+Shift+P` to open `Command Palette`, then choose `C/Cpp: Edit Configurations (JSON)` to generate a new `c_cpp_properties.json` file.

TODO ADD FIGURE

The modified `c_cpp_properties.json` file has shown as below. Please change `includePath` to adapt your own case.

```json
{
    "configurations": [
        {
            "name": "ESP32-Win",
            "includePath": [
                "${workspaceRoot}",
                "C:/msys32/opt/xtensa-esp32-elf/lib/gcc/xtensa-esp32-elf/5.2.0/include",
                "C:/msys32/opt/xtensa-esp32-elf/lib/gcc/xtensa-esp32-elf/5.2.0/include-fixed",
                "C:/msys32/opt/xtensa-esp32-elf/xtensa-esp32-elf/include",
                "C:/msys32/opt/xtensa-esp32-elf/xtensa-esp32-elf/sysroot/usr/include",
                "C:/msys32/home/User/esp/esp-adf/esp-idf/components",
                "C:/msys32/home/User/esp/esp-adf/components"
            ],
            "intelliSenseMode": "clang-x64",
            "browse": {
                "path": [
                    "${workspaceRoot}",
                    "C:/msys32/opt/xtensa-esp32-elf/lib/gcc/xtensa-esp32-elf/5.2.0/include",
                    "C:/msys32/opt/xtensa-esp32-elf/lib/gcc/xtensa-esp32-elf/5.2.0/include-fixed",
                    "C:/msys32/opt/xtensa-esp32-elf/xtensa-esp32-elf/include",
                    "C:/msys32/opt/xtensa-esp32-elf/xtensa-esp32-elf/sysroot/usr/include",
                    "C:/msys32/home/User/esp/esp-adf/esp-idf/components",
                    "C:/msys32/home/User/esp/esp-adf/components"
                ],
                "limitSymbolsToIncludedHeaders": true,
                "databaseFilename": "${workspaceRoot}/.vscode/browse.vc.db"
            }
        }
    ],
    "version": 4
}
```

> Note: The IntelliSense of VS Code does not treat `includePath` recursively, which means you might need to fill all of subfolder's path manually. Here is one convenient trick to help you. Open any cpp file, and find any green squiggle. Click the lightbulk, you will be able to add `includePath` setting automatically.
{: .note}

#### Tasks

To handle build, clean, and flash tasks in VS Code, we need to configure `tasks.json` file. Enter ```Ctrl+Shift+P``` to open Command Palette, then choose Tasks: Configuration Task to generate a new `tasks.json` file.

TODO add image

Modify the file as below, then you can use customized tasks in VS Code toolbar.

```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build app",
            "group": "build",
            "command": "make",
            "type": "shell",
            "args": [
                "app"
            ],
            "presentation": {
                "reveal": "always",
            },
            "problemMatcher": {
                "owner": "cpp",
                "fileLocation": "absolute",
                "pattern": {
                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        },
        {
            "label": "clean app",
            "command": "make",
            "type": "shell",
            "args": [
                "app-clean"
            ],
            "presentation": {
                "reveal": "always",
            },
        },
        {
            "label": "flash app",
            "command": "make",
            "type": "shell",
            "args": [
                "app-flash"
            ],
            "presentation": {
                "reveal": "always",
            },
        },
        {
            "label": "monitor",
            "type":"process",
            "windows": {
                "command": "c:/msys32/mingw32.exe",
                "args": [
                    "make",
                    "monitor"
                ],
            },
            "presentation": {
                "reveal": "always",
            },
            "problemMatcher": []
        },
        {
            "label": "menuconfig",
            "type":"process",
            "windows": {
                "command": "C:/msys32/mingw32.exe",
                "args": [
                    "make",
                    "menuconfig"
                ]
            },
            "presentation": {
                "reveal": "always",
            },
            "problemMatcher": []
        }
    ]
}
```

>Note: Please modify command property to match with your own case.
{: .note}

#### Integrated Terminal
To set the default integrated terminal as MSYS2, we need to configure `User Settings`. Enter ```Ctrl+Shift+P``` to open Command Palette, then choose `Preference: open settings (JSON)` to generate a new `settings.json` file.

TODO add image

```json
{
    "git.enableSmartCommit": true,
    "terminal.integrated.shell.windows": "C:/msys32/usr/bin/bash.exe",
    "terminal.integrated.shellArgs.windows": [
        "--login",
    ],
    "terminal.integrated.env.windows": {
        "CHERE_INVOKING": "1",
        "MSYSTEM": "MINGW32",
    },
    "C_Cpp.default.cppStandard": "c++17",
    "C_Cpp.updateChannel": "Insiders",
    "window.zoomLevel": 0,
}
```


## Optional Step: JTAG Debugging

TODO Check if this works and how to do handle this.