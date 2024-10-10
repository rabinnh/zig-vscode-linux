
# Setting up VSCode to debug Zig on Linux
This document will describe how to setup and configure VSCode for IDE debugging with Zig.

This document was accurate as of Zig 0.13.0

It is assumed that you already have Zig installed.

## Prerequisites

Install VSCode (https://code.visualstudio.com/docs/setup/linux)

Install the *lldb* debugger. This should be available via your package manager, ex. *sudo apt-get install lldb* on Debian/Ubuntu based systems.

## Set up VSCode

1. Open VSCode
2. Open the *Extensions* page either by clicking on the left panel icon or the menu View|Extensions
3. Install the *Zig Language* extnesion. This should ask you if you want to install the Zig Language Server. Answer 'Y'.
4. NOTE: This will also install the Zig Language Server but best to answer 'Y' when installing the Zig Language. Install the *Zig Language Extras* extension.
5. Create a Zig test project (a workspace with *zig init*) 
6. Make sure that the project builds.
7. Create a *.vscode* folder in the root folder of your project.  IOW it should be a peer to *src*.
8. Copy the following 2 files into *.vscode*:

**launch.json**

NOTE: Change *first_proj* in the following to the name of your workspace.

    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "(lldb) Launch",
                "type": "lldb",
                "request": "launch",
                "program": "${workspaceFolder}/zig-out/bin/first_proj",
                "args": [],
                "stopAtEntry": false,
                "cwd": "${workspaceFolder}",
                "environment": [],
                "externalConsole": false,
                "internalConsoleOptions": "openOnSessionStart",
                "MIMode": "lldb",
                "preLaunchTask": "build",
            }
        ]
    }

**tasks.json**

    {
        "version": "2.0.0",
        "tasks": [
            {
                "label": "build",
                "type": "shell",
                "command": "zig build",
                "problemMatcher": [],
                "group": {
                    "kind": "build",
                    "isDefault": true
                }
            }
        ]
    }

## Test

1. Open your project in VSCode and navigate to *src/main.zig*
2. Set a breakdpoint on one of the lines in the file.
3. Now try to debug with the menu item *Run|Start Debugging*.
