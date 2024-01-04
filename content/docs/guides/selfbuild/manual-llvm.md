---
title: "Manual LLVM build"
weight: 3
description: >
  How to build LLVM yourself, or "manually".
---


| You need to build LLVM manually in the following cases |
|---|
|  You would like to use it for the ESP8266 or ESP32 chips |
| You are using Windows. |
| Your Linux distribution (if you use Linux) does not ship the right LLVM version. |


#### Build dependencies

Debian and Ubuntu users can install all required tools this way:

```shell
sudo apt-get install build-essential git cmake ninja-build
```

Fedora users can install all required tools with:

```shell
sudo dnf groupinstall "Development Tools"
sudo dnf install cmake ninja-build
```

On MacOS you can install these tools using [Homebrew](https://brew.sh/):

```shell
brew install cmake ninja
```

On Windows you can install them using [Chocolatey](https://chocolatey.org/). Install Chocolatey first, then run the following in a command prompt or PowerShell with administrative privileges:

```shell
choco install --confirm git golang mingw make cmake ninja python
```

Use *Git Bash* (installed above) to run all the build commands like `make`. The TinyGo build system expects a Unix-like environment that is not normally provided by Windows but is included already in *Git Bash*.

Choco doesn't seem to add CMake automatically to the `$PATH` variable. You can do this manually if needed, in Git bash:

```shell
export PATH="$PATH:/c/Program Files/CMake/bin"
```

#### Building LLVM

The following command takes care of downloading and building LLVM. It places the source code in `llvm-project/` and the build output in `llvm-build/`. It only needs to be done once until the next LLVM release (every half year).

```shell
make llvm-source llvm-build
```

When building on Windows, add CCACHE=OFF.

```shell
make llvm-source llvm-build CCACHE=OFF
```


#### Building TinyGo

Once this is finished, you can build TinyGo against this manually built LLVM:

```shell
make
```

This results in a `tinygo` binary in the `build` directory:

```shell
$ ./build/tinygo version
tinygo version 0.30.0 linux/amd64 (using go version go1.21 and LLVM version 16.0.0)
```

You have successfully built TinyGo from source. Congratulations!

If you have gotten this far, please refer to [Additional requirements](./additional-requirements) to further set up TinyGo.