![MINGW PACKAGES PKGBUILD CI](https://github.com/tordona/mingw-packages/actions/workflows/build.yml/badge.svg)

# MINGW-packages
This repository contains modified package scripts for MinGW-w64 targets to build under MSYS2. These are specific to helping build statically linked [FFmpeg](https://www.ffmpeg.org/) binaries under MSYS2. 

## Compiling FFmpeg
Assuming you have a properly installed Windows MSYS2 environment and build tools, configure FFmpeg to your preferences.

```
./configure --extra-libs='-static -lpthread' --pkg-config-flags='--static' --arch=aarch64 --enable-gpl --enable-version3 --enable-static --disable-shared --disable-debug --disable-w32threads --disable-autodetect --enable-libssh
```

See more: [https://github.com/tordona/ffmpeg-win-arm64/blob/main/BUILDING.md](https://github.com/tordona/ffmpeg-win-arm64/blob/main/BUILDING.md)

## Errors
**ERROR: libname_xyz not found using pkg-config**

  * Install possible missing package or dependencies
    * Search using website https://packages.msys2.org/search
    * Search using pacman `pacman -Ss <arch> <library_name>`
  * Investigate `ffbuild\config.log`
  * Try one of the custom PKGBUILD available in this repo

## Using packages
 Assuming you have a properly installed MSYS2 environment and build tools, you can build any package using the following command:
 ```
    cd ${package-name}
    MINGW_ARCH=clangarm64 makepkg-mingw -sLf
 ```
 After that you can install the freshly built package(s) with the following command:
 ```
    pacman -U ${package-name}*.pkg.tar.xz
 ```

## Windows ARM64 FFmpeg Binaries
http://github.com/tordona/ffmpeg-win-arm64
