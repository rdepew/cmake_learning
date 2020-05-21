# cmake_learning

This repository keeps track of everything I'm learning about CMake. 

## Goal

I want to learn how to create .PKG files which can be dragged-and-dropped 
onto a FreeWave Technologies' ZumLink window in Windows 10 File Explorer,
or scp'ed to the /ptp directory on a ZumLink, and which will then be 
auto-executed or auto-installed by the ZumLink's OS.

## Particulars

CMake is oriented towards C/C++ programs. My application will be 
exclusively Python3 and Bash scripts. 

CPack is the CMake tool that creates installation files. CPack seems to
be a "by the way, you can do this with CMake" sort of application, but
for me, CPack is the focus. Naturally, I will learn CMake along the way
because you can't have CPack without CMake.

## How-to: Prequisites, Dependencies

Before you can start, you need to install some packages.
```
sudo apt install build-essentials g++ cmake
```

I think that's it.

## How-to: Quick version

Basically, it goes like this. For a project called 'hello', you create
this structure:

hello
|-- CMakeLists.txt
|-- License.txt
|-- build
`-- src
    |-- hello.py
    `-- helloConfig.h.in

Don't worry; I'll save these files in "first commit". 

Then you execute the following commands:
```
cd build
rm -rf *
cmake ..
make package
```

CMake and CPack create an install package and put it in the 'build'
directory.

## How-to: Some details

1. If you change CMakeLists.txt, you have to rerun `cmake`.
2. But if you only edit the source files, you only have to rerun 
  `make package`.
3. What if you add or delete a source file? I guess it depends on whether
  you have to edit CMakeLists.txt to account for adding or deleting the file.
