Building ProjectX
===========

To get started with ProjectX, you'll need to get
familiar with [Git and Repo](http://source.android.com/source/version-control.html).

Create the Directories
------------------

You will need to set up some directories in your build environment.

To create them run:

    mkdir -p ~/bin
    mkdir -p ~/px

Add ~/bin to PATH
------------------

    echo "PATH=${PATH}:/root/bin" >> ~/.bashrc
    source ~/.bashrc

Downloading Repo
------------------

    curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
    chmod a+x ~/bin/repo

Initialising ProjectX
------------------

    cd ~/px
    repo init -u git://github.com/ProjectX-Android/manifest.git -b lollipop-5.1

Building
------------------

build commands comming soon

