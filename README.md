# VS Code Task and Launch Configuration for C/C++ Projects

This README provides instructions on setting up VS Code tasks and launch configurations to compile and run multiple C/C++ source files located in a single directory.

## Prerequisites

- Visual Studio Code
- C/C++ extension for VS Code
- GCC or any other C/C++ compiler

## Directory Structure

Assume your project directory structure is as follows:

```
/e:/Projects/
│
├── src/
│   ├── main.c
│   ├── utils.c
│   └── utils.h
├── .vscode/
│   ├── tasks.json
│   └── launch.json
└── Readme.md
```

## tasks.json

Create a `tasks.json` file in the `.vscode` directory to define the build tasks.

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build C project",
            "type": "shell",
            "command": "gcc", //if your terminal does not recognize this change it to your compiler absolute path
            "args": [
                "-g",
                "${workspaceFolder}/src/*.c",
                "-o",
                "${workspaceFolder}/out/projectExecutable"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": [
                "$gcc"
            ],
            "detail": "Generated task to build all C source files."
        },
        {
            "label": "build C++ project",
            "type": "shell",
            "command": "g++", //if your terminal does not recognize this change it to your compiler absolute path
            "args": [
                "-g",
                "${workspaceFolder}/src/*.cpp",
                "-o",
                "${workspaceFolder}/out/projectExecutable"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": [
                "$gcc"
            ],
            "detail": "Generated task to build all C++ source files."
        }
    ]
}
```

## launch.json

Create a `launch.json` file in the `.vscode` directory to define the debug configurations.

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug C Project",
      "type": "cppdbg",
      "request": "launch",
      "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false, //change this for external consule
      "MIMode": "gdb",
      "setupCommands": [
        {
          "description": "Enable pretty-printing for gdb",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        },
        {
          "description": "Set Disassembly Flavor to Intel",
          "text": "-gdb-set disassembly-flavor intel",
          "ignoreFailures": true
        }
      ],
      "preLaunchTask": "build C project",
      "miDebuggerPath": "C:\\MinGW\\bin\\gdb.exe",
      "logging": {
        "trace": true,
        "traceResponse": true,
        "engineLogging": true
      }
    },
    {
      "name": "Debug C++ Project",
      "type": "cppdbg",
      "request": "launch",
      "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false, //change this for external consule
      "MIMode": "gdb",
      "setupCommands": [
        {
          "description": "Enable pretty-printing for gdb",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        },
        {
          "description": "Set Disassembly Flavor to Intel",
          "text": "-gdb-set disassembly-flavor intel",
          "ignoreFailures": true
        }
      ],
      "preLaunchTask": "build C++ project",
      "miDebuggerPath": "C:\\MinGW\\bin\\gdb.exe",
      "logging": {
        "trace": true,
        "traceResponse": true,
        "engineLogging": true
      }
    }
  ]
}
```

This setup will compile all C/C++ source files in the `src` directory and create an executable in the directory.
