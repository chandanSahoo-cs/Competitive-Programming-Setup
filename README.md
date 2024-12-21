# Competitive Programming Setup for Linux

This guide explains how to set up a competitive programming environment in Linux using VS Code and Sublime Text.

## For Windows

For the Windows setup, refer to this [link](https://github.com/Nishcurse/CpEnviromentSetup-).

## Steps for Setup in VS Code

### 1. Setting up VS Code

1. Open the folder where you have your executable files in VS Code.
2. Inside this folder, create a `.vscode` folder.
3. Within the `.vscode` folder, create two files: `launch.json` and `tasks.json`.

### 2. Configure `launch.json`

Copy and paste the following content into your `launch.json` file:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Run C++",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/${fileBasenameNoExtension}.out",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "preLaunchTask": "Compile and Run",
            "miDebuggerPath": "/usr/bin/gdb"
        }
    ]
}
```

### 3. Configure `tasks.json`

Copy and paste the following content into your `tasks.json` file:

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Compile and Run",
            "type": "shell",
            "command": "bash",
            "args": [
                "-c",
                "g++ -g -DDEBUG ${relativeFile} -o ${fileBasenameNoExtension}.out && ./${fileBasenameNoExtension}.out < input.txt > output.txt && rm ${fileBasenameNoExtension}.out"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": {
                "owner": "cpp",
                "fileLocation": ["relative", "${workspaceRoot}"],
                "pattern": {
                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        }
    ]
}
```

### 4. Modify Input and Output Files

- Update `input.txt` and `output.txt` in the `tasks.json` file to the names of your input and output files.
- Replace `-DDEBUG` with a custom macro name.

### 5. Running the Code

1. Open your `.cpp` file in VS Code.
2. Press `Ctrl+Shift+B` to build and run the program.
3. The program will execute with the specified input and output files.

## Steps for Setup in Sublime Text

### 1. Create a Custom Build System

1. Create a new build system in Sublime Text (`Tools > Build System > New Build System`).
2. Name the file `your_name.sublime-build` and paste the following content:

```json
{
    "cmd": ["g++", "-Dchandan", "-Wextra", "-Wall", "-std=c++20", "$file", "-o", "$file_base_name.out"],
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
    "working_dir": "$file_path",
    "selector": "source.cpp",
    "variants": [
        {
            "name": "Run",
            "cmd": ["bash", "-c", "g++ -Dchandan -Wextra -Wall -std=c++20 '$file' -o '$file_base_name.out' && './$file_base_name.out' < input.txt > output.txt"]
        }
    ]
}
```

### 2. Modify Input and Output Files

- Update `input.txt` and `output.txt` in the `your_name.sublime-build` file to the names of your input and output files.
- Replace `-Dchandan` with a custom macro name if needed.

### 3. Running the Code

1. Open your `.cpp` file in Sublime Text.
2. Press `Ctrl+B` to build and run the program.
3. The program will execute with the specified input and output files.

## Notes

- `-DDEBUG` is a preprocessor directive. You can change this to any name that suits your preference.
- Ensure the `g++` compiler and `gdb` debugger are installed on your Linux system.

Enjoy your seamless competitive programming setup!
