Build Debian packages for various EPICS components
==================================================

This Vagrant environment can be used to build Debian packages for various EPICS components for Debian 10 "buster". This is a quick 'n' dirty solution for users who don't have a full-fledged continuous integration system available that is able to build packages in a "clean-room" environment.

Required software
-----------------

 * Git
 * Vagrant
 * Virtual Box (or similar)

Steps to build
--------------
```
git clone https://github.com/mark0n/build-epicsdeb-packages.git
cd build-epicsdeb-packages/
vagrant up
```
Wait for the build to complete and log in by running
```
vagrant ssh
```
You will find the Debian packages in the home folder.

Known Issues
------------
I noticed that the latest Vagrant box file is still a pre-release version that now that the official repo has been updated fails to run "apt-get update" in non-interactive mode. I was able to work around this by running:
```
git clone https://github.com/mark0n/build-epicsdeb-packages.git
cd build-epicsdeb-packages/
vagrant up
```
Wait for the build to complete and log in by running
```
vagrant ssh
```
You will find the Debian packages in the home folder.