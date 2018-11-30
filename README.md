
![Screenshot](https://raw.githubusercontent.com/hsab/vscode_oF/master/.readme/image.png)

# ofxVSCode

Quick [openFrameworks](https://openframeworks.cc/) workspace initializer for [Visual Studio Code](https://code.visualstudio.com/).

Fork of [vscode_oF](https://github.com/hiroMTB/vscode_oF) by [@hiroMTB](https://github.com/hiroMTB) modified for Arch systems.

This is not an addon, although the name suggests it is.

This project is intended to quickly initiate a vscode workspace in an existing or empty project or an addon example.

It relies on the use of of **aliases** and command chaining in terminal to circumvent `git clone <repo> .`'s restrictions in a non empty directory.
  

# Example Alias:

After adding the alias to your shell config (in my case zsh) you can run `ofxvsc` in your current existing project.

This is particularly useful for quickly initiating addon examples for testing, without the need to go through the projectGenerator.

```
alias ofxvsc="git clone https://github.com/hsab/ofxVSCode.git && mv ./ofxVSCode/.vscode/ ./ && mv ./ofxVSCode/.gitignore ./ && rm -rf ./ofxVSCode"
```

Running the following will:
1. Clone the `ofxVSCode` repo in current project.
2. Move `.vscode` workspace folder and `.gitignore` from `ofxVSCode` to the current project directory.
3. Remove `ofxVSCode` folder entirely.


  

**Note:** By default the include and libraries are linked such that the project is in the same directory as myApps:

- Correct: `openframeworks/apps/yourProject`
- Incorrect: `openframeworks/apps/myApps/yourProject`

This structure is my personal preference. You can fork the repo and change every instance of `${workspaceRoot}/../../` to `${workspaceRoot}/../../../` in the `c_cpp_properties.json` file.

  

# Addons How-to:
1. Edit addons.make file if you want to add addons/
2. You might need to edit the `c_cpp_properties.json` file.
  
  

# Features
- Auto code completion (Requires [Microsoft C++ extension](https://code.visualstudio.com/docs/languages/cpp)).
- Step by step debugging (requires [gdb](https://www.gnu.org/software/gdb/) or similar debugger).
- Browse source code under `/libs/openFrameworks` and `/addons/*` folders.
- Currently tested on macOS, Ubuntu(by @anselanza), and Arch (Manjaro).

  
## Folder Structure

```
/of
  /apps
    /exampleProject <--
```

## oF version
0.10.0

  
## Known issue (copied from the original repo)

+ Rebuilding does not work properly. As a fix prior to running the task, **only** the binary file(s) is removed:
  - Build Debug: <pre>rm -f <b>./bin/$(basename '$PWD')_debug</b> && make <b>Debug</b> -j$(nproc)</pre>
  - Build Release: <pre>rm -f <b>./bin/$(basename '$PWD')</b> && make <b>Release</b> -j$(nproc)</pre>
+ macOS.sdk path is hard coded
+ `#include error detected` for header files which is not actualy included. For example `GL/gl.h` is for Linux wihch is not included on macOS. This shold be fixed with `limitSymbolsToIncludedHeaders` property in `c_cpp_properties.json`.
