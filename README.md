# Picotool prebuilt binary on Windows

1. clone [`raspberrypi/pico-sdk`](https://github.com/raspberrypi/pico-sdk)
1. clone [`raspberrypi/picotool`](https://github.com/raspberrypi/picotool)
1. set `PICO_SDK_PATH` to the path of `pico-sdk`
1. Install Visual Studio 2022 or [Build Tools for Visual Studio 2022](https://visualstudio.microsoft.com/visual-cpp-build-tools/), if you haven't already
1. Install [ninja](https://ninja-build.org/) and [cmake](https://cmake.org/) and add them to PATH, if you haven't already
1. use `clang` as the compiler
1. Install [vcpkg](https://github.com/microsoft/vcpkg) and install [libusb](https://vcpkg.link/ports/libusb)

```powershell
mkdir build 
cd build

# Visual Studio Code help me find the compiler path
# You still needs to specify `PICO_SDK_PATH` and `LIBUSB_ROOT` manually
"C:\Program Files\CMake\bin\cmake.EXE" -DCMAKE_BUILD_TYPE:STRING=Release -DCMAKE_EXPORT_COMPILE_COMMANDS:BOOL=TRUE "-DCMAKE_C_COMPILER:FILEPATH=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\Llvm\x64\bin\clang.exe" "-DCMAKE_CXX_COMPILER:FILEPATH=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\Llvm\x64\bin\clang.exe" -DPICO_SDK_PATH=~/pico-sdk -DLIBUSB_ROOT=C:/tools/vcpkg/packages/libusb_x64-windows --no-warn-unused-cli -SC:/Users/cross/Desktop/code/picotool -Bc:/Users/cross/Desktop/code/picotool/build -G Ninja
```

try to compile and fix the errors (there will be two redifinition errors of built-in functions, just comment them out)

and finally, copy `libusb-1.0.dll` from vcpkg to the executable directory,
after the a successful build, you will find `picotool.exe` in the `build` directory
