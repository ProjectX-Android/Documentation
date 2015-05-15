# Building SaberMod toolchains

[Source](https://gitlab.com/SaberMod/sabermod-manifest/blob/master/README.md)

In order to build ProjectX, you need to build the needed toolchains yourself, as they cannot be uploaded to github due file size limits!

Or you can download prebuilt toolchains from [here](http://sabermod.net)

* **First make sure you have the needed packages from the [Linux_setup.md](https://github.com/ProjectX-Android/Documentation/blob/master/Linux_setup.md)**

## Building

* Create the Directories - One time step
	mkdir -p ~/sm-tc && cd ~/sm-tc;

* Sync the repo
	repo init -u https://gitlab.com/SaberMod/sabermod-manifest.git -b master
	repo sync

* Building toolchains
	cd ~/sm-tc/smbuild/

* View all available arch directories and build all arch scripts.
	ls

* So for example:

	cd arm

* or stay in current directory to use the all script

* So for example:

	bash all-arm

* To execute a build using a script
	bash "insert name of script"

* So for example

	bash arm-eabi-4.9

### Checking for updates

	cd ~/sm-tc && repo sync;

