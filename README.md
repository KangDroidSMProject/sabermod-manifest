SaberMod Toolchains
===================

License
-------

By proceeding, you agree to the terms and conditions of the license.

https://gitlab.com/SaberMod/sabermod-manifest/raw/master/LICENSE

Intro and sources
-----------------

Only supported linux is Ubuntu 14.04-14.10 (Trusty-Utopic).  ROM toolchains will be built on Ubuntu 14.04 Trusty.  If you build on newer ubuntu systems, you may need to use the prebuilt toolchains.
Note: arm-eabi toolchains do not need specific versions of GLIBCXX installed.  They can be used on a variety of linux systems.  These toolchains will most likely not work without modifications to the kernels and the android system.  View all the android source modifications at: https://gitlab.com/SaberMod

Current source components are all from SaberMod gitlab with the exception of upstream merges from gnu and the android open source 
project (aosp)

Toolchain source components separated by branch.  See build scripts to see what versions are being used. https://gitlab.com/SaberMod/sabermod-build-scripts

    * GCC
      https://gitlab.com/SaberMod/GCC

    * binutils
      based on gnu binutils
      https://gitlab.com/SaberMod/BinUtils

    * gdb
      based on gnu gdb
      https://gitlab.com/SaberMod/GDB

    * stock gnu binutils and gdb (used for some targets)
      https://sourceware.org/git/gitweb.cgi?p=binutils-gdb.git

    * build
      based on aosp build repo
      https://gitlab.com/SaberMod/toolchain-build

    * SaberMod build scripts
      https://gitlab.com/SaberMod/sabermod-build-scripts

    * Cloog
      based on gnu cloog
      https://gitlab.com/SaberMod/CLOOG


    * ISL
      based on gnu isl
      https://gitlab.com/SaberMod/ISL

    * OSL
      based on gnu osl
      https://gitlab.com/SaberMod/OSL

    * gmp
      based on gnu gmp
      https://gitlab.com/SaberMod/GMP
    
    * mpc
      based on gnu mpc
      https://gitlab.com/SaberMod/MPC

    * mpfr
      based on gnu mpfr
      https://gitlab.com/SaberMod/MPFR

    * prebuilts
      https://gitlab.com/SaberMod/sabermod-prebuilts

    * sysroot
      https://gitlab.com/SaberMod/sabermod-sysroot

Prerequisites - One time step
-----------------------------

Linux x86_64 - This source only has been tested and works on linux 64bit systems.  Tested on Ubuntu 14.04-14.10 (Trusty-Utopic).

You will need some additional packages to use the included toolchain during compilation.  It is a good idea to make sure you have these packages installed.

Tested on Ubuntu the following packages are available:
    * build-essential
      Essential development packages

    * gcc-multilib g++-multilib

    * flex
      http://flex.sourceforge.net/

    * bison
      http://www.gnu.org/software/bison/

    * libncurses5-dev
      http://download.gna.org/pdbv/demo_html/demo_2.0.10/package/libncurses5-dev_5.4-4.html

    * libtool
      https://www.gnu.org/software/libtool/

    * libcap-dev
      Installs a missing header capability.h file.

    * texinfo
      Program needed to create texi files.

     * automake and autoconf
      Two programs needed to configure the individual build components automatically.

    * libgmp-dev
      Needed for cloog to compile (graphite flags tools)

    * libexpat-dev
      Needed for gdb compilation when it uses -lexpat (and it does use it).

    * python-dev
      Needed to use --with-python

So for example:

    sudo apt-get install libcap-dev texinfo automake autoconf libgmp-dev libexpat-dev python-dev build-essential gcc-multilib g++-multilib libncurses5-dev flex bison libtool gawk;

Installing cloog - Can be installed again
-----------------------------------------

Note that this is required to build the toolchains, NO EXCEPTIONS.  It is also usefull to have these installed for ROM building with SaberMod.  These help a lot for graphite flags, which you should be using (if not no point in using sm).  DO NOT install the package libcloog-isl-dev
There is newer versions available that I have compiled as prebuilts to be used in /usr/lib/x86_64-linux-gnu
download it as a zip file from here:
https://gitlab.com/SaberMod/sabermod-prebuilts/repository/archive.zip

cd to where you have the repository downloaded

Note:  The zip name will change with new commits.  Change the name below accordingly.

    cd ~/Downloads
    unzip sabermod-prebuilts-"commit number".zip
    sudo cp -R sm-prebuilts-master/cloog/lib/* -f /usr/lib/x86_64-linux-gnu

To install future updates, repeat this proccess.

Link header files for multilib - One time step
----------------------------------------------

In order to enable mutilib on ubuntu there's some header files that need to be linked from asm-generic.  asm-generic already has all the files needed but gcc wants it in asm.

    sudo ln -s /usr/include/asm-generic /usr/include/asm;

Create the Directories - One time step
--------------------------------------

    mkdir -p ~/sm-tc && cd ~/sm-tc;

Sync the repo
-------------

    repo init -u https://gitlab.com/SaberMod/sabermod-manifest.git -b master
    repo sync

Building toolchains
-------------------

Build via sabermod scripts for ease.

cd ~/sm-tc/smbuild/

View all available arch directories and build all arch scripts.
---------------------------------------------------------------

    ls

So for example:

    cd arm

or stay in current directory to use the all script

So for example:

    bash all-arm

To execute a build using a script
---------------------------------

    bash "insert name of script"

So for example

    bash arm-eabi-4.9

Checking for updates
--------------------

    cd ~/sm-tc && repo sync;
