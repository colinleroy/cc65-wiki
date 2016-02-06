# Android

## Compile

The cc65 suite has been successfully compiled for Android using the standalone toolchain from the NDK on Linux (Debian Jessie). There is no need to install Android Studio or the Android SDK. Here are the steps:

1) Compile cc65 as usual and install it somewhere, so you can save the platform-independent parts:

	cd __cc65_sources__
	make clean
	make
	prefix=__somewhere__/cc65 make install

2) Generate a NDK standalone toolchain (where `$NDK` is set to the location where you have uncompressed the NDK):

	$NDK/build/tools/make-standalone-toolchain.sh \
	--arch=arm --platform=android-16 --install-dir=__somewhere__/toolchain

3) Cross-compile the Android executables:

	cd __cc65_sources__
	export PATH="$PATH:__somewhere__/toolchain/bin"
	export CROSS_COMPILE=arm-linux-androideabi-
	export USER_CFLAGS=-fPIE
	export LDFLAGS="-fPIE -pie"
	make clean
	make bin

The executables can be found in the directory `bin` and have a `.exe` extension. To reduce their size, you can strip them:

	cd __cc65_sources__/bin
	for i in *.exe ; do arm-linux-androideabi-strip $i ; done

## Precompiled Archives

Unofficial precompiled archives are available here: https://github.com/efornara/cc65/releases

From the user's point of view, the main difference compared to an official cc65 branch is that the default target is *not* c64. All the official targets are still available, but, when compiling for the c64 target, the option `-t c64`
must be explicitly selected.

You need two files:

- The `cc65-android-share.zip` file, which contains the platform-independent parts.

- One of the `cc65-android-bin-*-*.zip` files, which contain the executables for specific Android versions.

The file `cc65-android-bin-arm-pie.zip` is the one to use in the vast majority of cases. Here is a table to help you choose:

          pie    nopie   static  
    arm   4.1+  1.5-4.0   1.5+   
    x86   4.1+  2.3-4.0   2.3+   
    mips  4.1+  2.3-4.0   2.3+   

While the static versions are the most compatible, they are not recommended, as they are bigger and they have compiled-in outdated runtime libraries.

## Installation

### Planning

As a review, in Android there is:

- **Internal Memory**: Partition in the internal flash memory where applications are installed by default, and where native code *must* be located to be allowed to run.  Files can be made executable, but cannot be (?) shared among applications. On cheap phones, the available space in this partition can be very limited.

- **External Memory**: Partition in the internal flash memory where applications can store additional data. File permissions are quite liberal, but making files executable is not allowed.

- **External Storage**: External SD cards. Most application resources can often be moved there, but this excludes their native code. Starting from KitKat, there are permissions issues that make difficult to share files among different applications; somehow fixed starting from Lollipop.

The space used by cc65 is approximately:

    binaries                   1M

    share (1 target)           2M
    share (1 target + doc)     4M
    share (all targets + doc) 32M

The best strategy is probably to install the shared files in the external memory or storage (possibly removing libs of targets that are not needed) and the binaries in each application invoking cc65.  Usually this is just one application (e.g. a terminal), but in theory one could imagine using an editor like Vim Touch and invoking the compilation from there.

### Example

Here is the procedure that has been used to test cc65 on an old version of Android (1.5) running on the emulator (you have to enable the obsolete packages to see it). It uses an old version of Jack Palevich's Terminal.

It can serve as a template, but it shouldn't be used blindly, as the installation can vary a lot from device to device.

We create a new directory and download into it:

- `cc65-android-share.zip` from https://github.com/efornara/cc65/releases
- `cc65-android-bin-arm-nopie.zip` from https://github.com/efornara/cc65/releases
- `busybox-armv5l` from https://busybox.net/downloads/binaries/
- `Term-1.0.65.apk` from http://jackpal.github.io/Android-Terminal-Emulator/

We need three pieces of information about the target environment:

1. Where downloaded files go.

2. Where we can make file executables.

3. Where we can store the cc65 shared resources.

In this environment:

1. `/data/local/tmp` is a good place where we can upload files.

2. `/data/data/jackpal.androidterm/app_HOME` is the place reserved for user's files by the terminal we are using. It can be accessed directly by typing `cd` without arguments.

3. `/sdcard` is the location of the external memory, so `/sdcard/share` looks fine.

With this information, we can write a throwaway script for the installation. On a real phone, this could be written using an editor app, in this case we write it on the host and upload it. While we are still working on the host, we might as well write a convenience script to setup the environment and a test program.

	# env.txt
	PATH="/data/data/jackpal.androidterm/app_HOME/bin:$PATH"
	CC65_HOME=/sdcard/share/cc65
	export PATH CC65_HOME

	/* hello.c */
	#include <stdio.h>
	void main() {
	  printf("Hello, World!\n");
	}

	# install.txt
	d=/data/local/tmp
	h=/data/data/jackpal.androidterm/app_HOME
	s=/sdcard/share
	cd $h
	cat $d/busybox-armv5l >busybox
	chmod 755 busybox
	./busybox unzip $d/cc65-android-bin-arm-nopie.zip
	cd bin
	chmod 755 *
	mv ../busybox .
	ln -s busybox cp
	ln -s busybox vi
	mkdir $s
	cd $s
	$h/bin/busybox unzip $d/cc65-android-share.zip
	cd $h
	mkdir etc
	cat $d/env.txt >etc/vars
	mkdir prgs
	cat $d/hello.c >prgs/hello.c

Note that on most Android systems, the command `cp` is missing, and therefore `cat` must be used.

We install the terminal and "download" everything we need:

	linux$ export ANDROID_SERIAL=emulator-5554
	linux$ adb install Term-1.0.65.apk
	linux$ adb push busybox-armv5l /data/local/tmp
	linux$ adb push cc65-android-share.zip /data/local/tmp
	linux$ adb push cc65-android-bin-arm-nopie.zip /data/local/tmp
	linux$ adb push install.txt /data/local/tmp
	linux$ adb push env.txt /data/local/tmp
	linux$ adb push hello.c /data/local/tmp

From the emulator, we start the terminal and run the installation script:

	android$ . /data/local/tmp/install.txt
	...
	android$ exit

From the emulator, we can now restart the terminal and check that everything works:

	android$ cd
	android$ . etc/vars
	android$ cd prgs
	android$ cl65 -t sim6502 hello.c
	android$ sim65 hello
	Hello, World!
