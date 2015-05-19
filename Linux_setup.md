# How to set up Linux for building ProjectX

## Choosing the distro

In order to build ProjectX you will need a Linux OS as no other is supported. Everything is tested on Ubuntu **14.04.2**, other versions or distros may or may not work without any further modifications of the packages.

## In case of VM: Add a shared folder

If you want to get your files out of the VM you might want to set up a shared folder:

* Add folder in host
* Add folder in VM
* Add folder in Linux
* Insert Guest additions  

	sudo apt-get install dkms
	cd /media/USERNAME/
	ls
	cd VBOXADDITIONS_X.X.X_XXXXX
	ls
	sudo sh VBoxLinuxAdditions.run
* reboot  

		sudo nano /etc/rc.local

* remove first #
* enter this after the blue text

		mount -t vboxsf -o rw,uid=1000,gid=1000 NAME IN VM /home/USERNAME/ORDNERNAME
		STRG + X
* reboot

## Install packages

These packages and commands are needed in order to build ProjectX and SaberMod toolchains

### Java

	sudo apt-get install openjdk-7-jdk openjdk-7-jre

	java -version

### Flash Player

	sudo apt-get install flashplugin-installer

### Packages

	sudo apt-get install liblz4-tool libcap-dev texinfo automake autoconf libgmp-dev libexpat-dev python-dev gcc-multilib g++-multilib libncurses5-dev flex gperf schedtool bison build-essential curl git gnupg gperf libesd0-dev libsdl1.2-dev libwxgtk2.8-dev libxml2 libxml2-utils lzop pngcrush squashfs-tools xsltproc zip zlib1g-dev lib32ncurses5-dev lib32readline-gplv2-dev lib32z1-dev libtool

	sudo ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /usr/lib/i386-linux-gnu/libGL.so

	sudo apt-get autoremove

* Download: https://gitlab.com/SaberMod/sabermod-prebuilts/repository/archive.zip
* unzip
	sudo cp -R sabermod-prebuilts/cloog/lib/* -f /usr/lib/x86_64-linux-gnu

### Link header files for multilib

	sudo ln -s /usr/include/asm-generic /usr/include/asm

### extra LIBS to fix ROM compile

* search for "**libisl13**" in Ubunbtu package manager

### Update GLIBCXX to work with prebuilt toolchains

	sudo apt-get install libstdc++6
	sudo add-apt-repository ppa:ubuntu-toolchain-r/test 
	sudo apt-get update
	sudo apt-get upgrade
	sudo apt-get dist-upgrade

## SDK

* https://developer.android.com/sdk/index.html
* download Android Studio 
* unzip
	cd android-studio/bin
	./studio.sh
* install
* download sdk

## bin directory

	mkdir -p ~/android/bin
	export PATH=${PATH}:~/android/bin

## .bashrc

* open .bashrc
* add these lines to the end
		# Android tools
		export PATH=${PATH}:/home/**USER**/android/SDK/tools
		export PATH=${PATH}:/home/**USER**/android/SDK/platform-tools
		export PATH=${PATH}:/home/**USER**/android/android-studio/bin
		export PATH=${PATH}:~/android/bin
		PATH=/home/**USER**/.bin:$PATH 
* save

## Setup git

	git config --global user.name "**Your Name Here**"
	git config --global user.email "**your_email@example.com**"
	git config --global credential.helper cache
	git config --global credential.helper 'cache --timeout=3600'

## ccache

It is **NOT** recommended to use ccache when compiling ProjectX!
