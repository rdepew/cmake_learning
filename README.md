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

## How-to: Using dpkg

If you use the CMakeLists.txt file in the first few commits of this repo,
then `make package` creates a .deb file. I think this is similar to a .pkg
file.

To install the .deb file on a ZumLink, copy it to the /data directory and:
```
sudo dpkg -i package-name.deb
```

To list the contents of a .deb file:
```
sudo dpkg --contents package-name.deb
```

To remove the package after it's installed:
```
sudo dpkg -r package-name.deb # This keeps the config files
# or
sudo dpkg -p package-name.deb # This deletes the config files (p for "purge")
```

## How-to: Using apt instead of dpkg

You can use `apt` instead of `dpkg` to install and remove the .deb file.

To install the .deb file on a ZumLink, copy it to the /data directory and:
```
sudo apt install -f package-name
```

Note that, even if the package name is `something_1.0_Linux.deb`, you only
need to type `something` for the package name. Also note the `-f` option, 
which specifies to install from the file rather than from an APT repository.

To list the contents of a .deb file:
```
sudo apt ................. # I don't know!
```

To remove the package after it's installed:
```
sudo apt remove package-name
```


## How-to: Some details

1. If you change CMakeLists.txt, you have to rerun `cmake`.
2. But if you only edit the source files, you only have to rerun 
  `make package`.
3. What if you add or delete a source file? I guess it depends on whether
  you have to edit CMakeLists.txt to account for adding or deleting the file.
