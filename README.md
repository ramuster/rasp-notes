# rasp-notes

Raspberry Pi notes
==================

Starting Raspberry Pi
=====================

Processor is Broadcom BCM2835
System on chip (SoC) multimedia processor.  Beneath memory chip at centre of board.

No external device should draw > 100mA from any USB port

Expand filesystem to fill entire SD card:

`expand_roofs` option on `raspi-config`

2 default user accounts:

 -  pi  (normal user)
 -  root (administrator or superuser)

Configuration files:
--------------------

All important parameters for firmware in text files

Mostly in 3 files in boot:

 -  config.txt
 -  cmdline.txt
 -  start.elf

Restart system to make changes

In case of start error, edit config.txt on separate PC then plug SD back in

If completely lost, delete config.txt and pi will start with defaults

Or copy fresh Raspbian image onto SD card
     
To update kernel and firmware:
------------------------------

Forum says use apt-get upgrade after apt-get update.

Book says:

Check old versions using:

	uname -a
	/opt/vc/bin/vcgencmd version

Download new versions from <https://github.com/raspberrypi>

Replace files on SD.

Or use Rpi-Update (may need to `sudo apt-get install rpi-update`)

Firmware in `start.elf`

Kernel in `kernel.img`

To install Chromium:
--------------------

     sudo apt-get install chromium-browser
     # [Didn't work for me, install iceweasel did]

Virtual Network Computing (VNC)
===============================

Allows you to control Pi desktop from another computer.

Install VNC server on Pi first - e.g. TightVNC:

    sudo apt-get install tightvncserver

Apple Mac comes with VNC client

Adventures in Raspberry Pi
==========================

Carrie Anne Philbin
-------------------

login default is pi
password default is raspberry

`startx`
	start X windows and desktop environment

`raspi-config`
	Config screen (use sudo)

To use another OS on NOOBS, hold shift when booting

`sudo shutdown -h now`
	Shuts down now

`sudo shutdown -r now`
	Restarts now

`sudo reboot`
    Reboots

`clear`
	Clears terminal screen

`ls -1`
	lists one filename per line
`ls -a`
	lists all files (including .hidden)

`Ctr-Alt-F1` to `F6`	virtual terminals:
	`Ctr-Alt-F1`	original
	`Ctr-Alt-F1`	desktop environment

<http://www.wiley.com/go/adventuresinrp>   Videos

`date`

`sudo apt-get install`
	To get and install new programs
`sudo apt-get update`
	To download info about updates
`sudo apt-get upgrade`
	To install updates/upgrades
`sudo apt-get remove`
	To remove programs
`sudo apt-get purge`
	To remove programs and associated junk
`sudo apt-get autoremove`
	General clean-up
`sudo apt-cache`
    Utility for managing cached list of software
`sudo apt-cache search game`
    Searches for game programs
    

Midori (browser)
----------------
Ctr-K	Move to search bar

Linux
-----

`ps`	List processes running for me
`ps -e`	List all processes on system
`ps -f`   Gives detailed info on processes
`&`	At end of line executes command in background
`./`	Before filename to run script not in path

`Alt-F2`	Run box

Text-based browsers
-------------------

w3m is text-based web browser. I couldn't get it.

Lynx is another:

	sudo apt-get install lynx

When opening press 'o' to open options.

Change 'ask user' to 'accept all' (cookies).

Python Turtle Module
--------------------

# Displays pentagon of different colour sides

import turtle

alex = turtle.Turtle()
alex.shape("turtle")	# default is arrow
alex.pensize(5)

for aColor in ["red", "green", "blue", "orange", "purple"]:
    alex.color(aColor)
    alex.stamp()	# leaves imprint of shape at that point
    alex.forward(100)	# move forward 100
    alex.left(72)	# turn left 72 degrees

___________

Sonic Pi
========

Developed by Sam Aaron, Cambridge, uses Ruby

`sudo apt-get install sonic-pi`

    # To play Twinkle Twinkle:
    #  - default sound 'pretty_bell':

    play 60    # play C (MIDI key no.)
    sleep 0.5  # pause 0.5 sec
    play 60
    sleep 0.5
    play 67
    sleep 0.5
    play 67
    sleep 0.5
    play 69
    sleep 0.5
    play 69
    sleep 0.5
    play 67
    sleep 0.5

    # To play as sequence use data structure:
    play_pattern [60,60,67,67,69,69,67]
    # ...plays with delay

    # To play at 150bpm
    use_bpm 150
    play_pattern [60,60,67,67,69,69,67]

    # Use loop to repeat:
    2.times do
      play_pattern [67,67,65,65,64,64,62]
      sleep 0.5
    end

    # Translate into notes using variables:
    C = 60
    D = 62
    E = 64
    F = 65
    G = 67
    A = 69

    use_bpm 150
    play_pattern [C,C,G,G,A,A,G]
    play_pattern [F,F,E,E,D,D,C]
    play_pattern [G,G,F,F,E,E,D]
    play_pattern [G,G,F,F,E,E,D]
    play_pattern [C,C,G,G,A,A,G]
    play_pattern [F,F,E,E,D,D,C]


__________

My backup command:

`rsync -av --exclude=".*" -delete /home/pi/ /media/pi/8\ GB\ TDK/Backup`

Cycle through open apps using `Alt-Tab`


Raspberry Pi: A Quick Start Guide
=================================

Maik Schmidt
------------

Good simple book

Own web page (to download code):

<http://pragprog.com/titles/msraspi>

Extract source code with:

`tar xzf msraspi-code.tgz`

BCM2835 contains ARM1176J-F processor running 700MHz and GPU named VideoCoreIV
Graphics drivers are proprietary.

*  CSI connector for camera
*  DSI connector for display
*  JTAG headers help debug hardware projects.

5 status LEDs:

* OK indicates SD card access
* PWR turns red with power
* FDX shows if LAN running full duplex
* LNK blinks with LAN activity
* 10M on when Ethernet running 100Mbit/s

Bodhi Linux available

Preparing SD Card
-----------------

	Windows
	-------

	Get and run Win32DiskImager.exe
	Download ZIP file of image and unzip
	Install fciv command to check SHA1 checksum:
	(File checksum integrity verifier)
	Write unzipped image to FAT32 formatted SD card

	Mac OSX and Linux
	-----------------

	Read the book or look on raspberrypi.org

Date set from network and not retained

To set date manually:
	`sudo date --set="2016-05-25 13:24:42"`

Possible PDF readers are xpdf and evince. xpdf installed on RaPi3.

`sudo apt-get autoclean` to remove files after upgrade.

Dependency packages no longer needed removed by:
	`sudo apt-get autoremove`

Add new user: `adduser`

If you want to give your new user the same rights as the pi user,
you have to add the user to the sudoers file:
Can't edit sudoers file directly; have to use visudo command;
which invokes vi text editor by default. To use nano:

	sudo EDITOR=nano visudo

[Seems to open by default in nano on my RaPi3]

Add a line in section:
`# User privilege specification`

Like the following, but replace pi with new user name:
`pi ALL=(ALL) ALL`

To delete a user account but not files:
`userdel name`

To delete user account and files:
`userdel -r name`

To change user's attributes such as their home directory:
	`usermod`

To change a password
	`passwd`

List processes running:
	`ps`
	Get more info using `-f` option
	List all processes with `-e`
	See all info with `-ef`

Pressing `Ctrl-C` terminates running process by sending `SIGINT` signal to process.

To stop background process use:
	`kill 111`
	where 111 is process ID (PID)
	sends SIGTERM command

Moving around man pages or less/more:
	`q`          quit
	`spc` or `PgDwn`   down a page
	`b`   `^b` `PgUpup` back a page
	`Down` `Rtn`    down a line
	`Up`         up a line

__________
Need to finish book then complete notes
__________

Learn to program your Raspberry Pi
==================================

Kevin Partner (kindle sample)
-----------------------------

Premier Farnell and RS Electronics are official RaPi suppliers.

Synaptic graphical package manager can search/find available packages.
	sudo apt-get install synaptic
Already installed on RaPi3

________

Raspberry Pi Server Essentials
==============================

Piotr Kula
----------

Extra peripherals
-----------------
  - get driver
  - plug in device
  - use lsub command to see if detected

Some wireless keyboards, such as the Microsoft 3000 series, do not need any configuration as they emulate a wired keyboard and can be used during boot time.

How to install Raspbian on the Raspberry Pi:
--------------------------------------------

For Windows and Macintosh users, it is recommended by the Raspberry Pi foundation to use the SD Formatter from <http://www.sdcard.com>. 
    
For Windows, perform the following steps:
    
 1. Install the SD card formatting tool.
 2. In the Option menu, set the Format size adjustment option to ON.
 3. Make sure that you select the correct SD card.
 4. Click on the Format button.

For Macintosh, perform the following steps:
      
 1. Install the SD card formatting tool.
 2. Select Overwrite Format.
 3. Make sure that you select the correct SD card.
 4. Click on the Format button.

For Linux, perform the following steps:
 
 1. It is recommended to use the GParted or Parted tool in Linux.
 2. Format the entire disk as FAT.

You should download the latest NOOBS archive from <http://www.raspbian.org/>.

Unzip the archive.

Copy the extracted files on to the formatted SD card:

 * For copying image on Mac use Etcher

__________

42 of the Most Useful Raspberry Pi Commands:
============================================

General Commands
----------------

 -  apt-get update: Updates your version of Raspbian.
 -  apt-get upgrade: Upgrades all of the software packages you have installed.
 -  clear: Clears the terminal screen of previously run commands and text.
 -  date: Prints the current date.
 -  find / -name example.txt: Searches the whole system for the file example.txt and outputs a list of all directories that contain the file.
 -  nano example.txt: Opens the file example.txt in “Nano”, the Linux text editor.
 -  poweroff: To shutdown immediately.
 -  raspi-config: Opens the configuration settings menu.
 -  reboot: To reboot immediately.
 -  shutdown -h now: To shutdown immediately.
 -  shutdown -h 01:22: To shutdown at 1:22 AM.
 -  startx: Opens the GUI (Graphical User Interface).

File/Directory Commands
-----------------------

 *  cat example.txt: Displays the contents of the file example.txt.
 *  cd /abc/xyz: Changes the current directory to the /abc/xyz directory.
 *  cp XXX: Copies the file or directory XXX and pastes it to a specified location; i.e. cp examplefile.txt /home/pi/office/ copies examplefile.txt in the current directory and pastes it into the /home/pi/ directory. If the file is not in the current directory, add the path of the file’s location (i.e. cp /home/pi/documents/examplefile.txt /home/pi/office/ copies the file from the documents directory to the office directory).
 *  ls -l: Lists files in the current directory, along with file size, date modified, and permissions.
 *  mkdir example_directory: Creates a new directory named example_directory inside the current directory.
 *  mv XXX: Moves the file or directory named XXX to a specified location. For example, mv examplefile.txt /home/pi/office/ moves examplefile.txt in the current directory to the /home/pi/office directory. If the file is not in the current directory, add the path of the file’s location (i.e. cp /home/pi/documents/examplefile.txt /home/pi/office/ moves the file from the documents directory to the office directory). This command can also be used to rename files (but only within the same directory). For example, mv examplefile.txt newfile.txt renames examplefile.txt to newfile.txt, and keeps it in the same directory.
 *  rm example.txt: Deletes the file example.txt.
 *  rmdir example_directory: Deletes the directory example_directory (only if it is empty).
 *  scp user@10.0.0.32:/some/path/file.txt: Copies a file over SSH. Can be used to download a file from a desktop/laptop to the Raspberry Pi. user@10.0.0.32 is the username and local IP address of the desktop/laptop and /some/path/file.txt is the path and file name of the file on the desktop/laptop.
 *  touch: Creates a new, empty file in the current directory.

Networking/Internet Commands
----------------------------

 *  ifconfig: To check the status of the wireless connection you are using  (to see if wlan0 has acquired an IP address).
 *  iwconfig: To check which network the wireless adapter is using.
 *  iwlist wlan0 scan: Prints a list of the currently available wireless networks.
 *  iwlist wlan0 scan | grep ESSID: Use grep along with the name of a field to list only the fields you need (for example to just list the ESSIDs).
 *  nmap: Scans your network and lists connected devices, port number, protocol, state (open or closed) operating system, MAC addresses, and other information.
 *  ping: Tests connectivity between two devices connected on a network. For example, ping 10.0.0.32 will send a packet to the device at IP 10.0.0.32 and wait for a response. It also works with website addresses.
 *  wget http://www.website.com/example.txt: Downloads the file example.txt from the web and saves it to the current directory.
 
System Information Commands
---------------------------

 *  cat /proc/meminfo: Shows details about your memory.
 *  cat /proc/partitions: Shows the size and number of partitions on your SD card or hard drive.
 *  cat /proc/version: Shows you which version of the Raspberry Pi you are using.
 *  df -h: Shows information about the available disk space.
 *  df /: Shows how much free disk space is available.
 *  dpkg –get-selections | grep XXX: Shows all of the installed packages that are related to XXX.
 *  dpkg –get-selections: Shows all of your installed packages.
 *  free: Shows how much free memory is available.
 *  hostname -I: Shows the IP address of your Raspberry Pi.
 *  lsusb: Lists USB hardware connected to your Raspberry Pi.
 *  UP key: Pressing the UP key will enter the last command entered into the command prompt. This is a quick way to correct commands that were made in error.
 *  vcgencmd measure_temp: Shows the temperature of the CPU.
 *  vcgencmd get_mem arm && vcgencmd get_mem gpu: Shows the memory split between the CPU and GPU.

__________

Raspberry Pi Cookbook - Simon Monk
==================================

Writing SD Card Manually on Linux
---------------------------------

Download iso

Use ubuntu ImageWriter tool to transfer to card

`sudo apt-get install usb-imagewriter`

To find IP address of your pi:

	sudo ifconfig OR
	hostname -I

WFi adapters can use a lot of power.

To modify file permissions:

	chmod
	+, -, = for add, remove, set. Then permission type:
	g Group
	u User
	o Other

chown (change owner) to modify ownership of file or directory

Screen capture:

	scrot

Fetching Source Code with git
-----------------------------

To use code in Git repositories, download Git, then use git clone command to fetch files

	sudo apt-get install git
	git clone http://github.com/simonmonk/raspberrypi_cookbook.git

Running program or script at regular intervals
----------------------------------------------

	crontab

Edit schedules events using:

	crontab -e

If the script or program needs superuser, prefix commands with sudo

Finding Things
--------------

Start with a directory specified in `find`. e.g.:

    find /home/pi -name gem gemgem.py
    
Can redirect error messages by adding 2>/dev/null to end of line:

    find / -name gemgem.py 2>/dev/null
    
Some options:

    type -d     # directory
    type -f     # regular file
    -ls         # list file
    -perm 744   # permission 744
    
Using command line history
--------------------------

`history` command piped to `grep` to find older commands

Can run a history item using `!` followed by line number:

    !952
    
Monitoring Processor Activity
-----------------------------

 *  Task Manager (GUI)
 *  top
 *  ps -e ("every process")
 
Then use `kill 3` to kill process ID no. 3

Listing connected USB devices
-----------------------------

    lsusb

Hiding output to the terminal
-----------------------------

    > /dev/null
    
Running processes in the background
-----------------------------------

Use `&` after command.

To bring background process back to foreground, use `fg`

Finding out how much room on SD card
------------------------------------

    df -h
    

__________

Add printer using CUPS
======================

    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install cups
    
Add user to default printing group:

    sudo usermod -a -G lpadmin pi

(lpadmin is the default printing group)

In browser:

    http://localhost:631

Add printer (or choose default options)

May need gutenprint 5.2.11 or newer for canon drivers.

Add wireless printer
====================

    sudo apt-get install samba # not sure if needed
    
In browser: localhost:631

Tick server settings, share printers connected to this system, allow printing from internet, allow remote admin.

Change settings.

Add printer. Should find network printer - add it, tick share this printer, select driver, add printer.

__________

raspberry-pi Documentation
==========================

Greg Loyse 2017
---------------

To show directory and its contents:

    tree
    
System specs:
-------------

    uname -a    #  Kernel version and sys architecture
   
    head -n /etc/issue  #  distro name and version
    
    cat /proc/partitions    #  all partitions

Modules and devices
-------------------

list current modules:

    lsmod

Make test programs
------------------

Test programs in /opt/vc/src

README first

cd into directory, then `make`

__________

Raspberry Pi for beginners
==========================

Everything you need to know to get the most out...

Clydebank Technology
--------------------

To install Apache (which is apache2):

	sudo apt-get install apache2 -y

Default webpage served when you browse http://localhost/ on pi

or from another computer: http://192.168.1.10 or whatever is your IP address.

To change default webpage. Go to:/var/

....need to do and write up more...

__________

Getting started with the raspberry pi
=====================================

Kevin Johnson
-------------

To find something to install:

	apt-cache search something 

apt-get purge removes more than apt-get remove

Most config options in 3 files in /boot:

 -  config.txt
 -  cmdline.txt
 -  start.elf

If you have messed up, edit config.txt on separate PC, revert changes and plug SD card back in. If you are completely lost, delete the config.txt file and pi will start with defaults. You can also copy fresh Raspbian image onto SD.

Update kernel
-------------

Check current kernel and firmware versions using:

	uname -a
	vcgencmd version

To updgrade, download new versions from Github. Copy to SD.

Installing new kernel or firmware involves only replacing few files in /boot

Firmware contained in start.elf

Kernel in kernel.img

Download new kernel and firmware files on PC and copy onto SD. Rpi-Update can automate process for you.

VNC
---

Install VNC server on Pi, e.g. TightVNC

	sudo apt-get install tightvncserver

Apple computers come with inbuilt VNC client

Make web server
---------------

Apache HTTP server and Nginx

Lighttpad better choice for Pi: sudo apt-get install lighttpd

Once installed, test by pointing pi browser to localhost or external browser to your IP address.

Copy your website to /var/www/html/ making sure the root index file is called index.html

Need to delete the default index.lighttpd.html file

Install LAMP stack on Pi
------------------------

sudo apt-get install apache2 php5 php5-mysql mysql-server

If using Pi solely as webserver, switch allocate more memory to CPU not GPU

Rasbmc...
---------

*****************************

Table of Contents in Markdown
=============================

At top of page insert the title:

	% My title here

To make TOC:

	pandoc --toc --standalone mywebpage.txt -o mywebpage.html

*************************************

How to set up VNC, even over internet
=====================================

<https://www.raspberrypi.org/documentation/remote-access/vnc/>

****************

FTP Server on Pi
================

    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install proftpd # d is daemon
    
Run standalone mode

    sudo service proftpd status
    ps -aux | grep proftpd

Connect on another machine

    ftp 192.x.y.z # whatever your pi's ipaddress is
    
To restart ftpd on Pi:

    sudo service proftpd restart
    
**********

Learning Raspbian
=================

William Harrington 2015
-----------------------

Autofs is a deamon that automatically mounts removable storage devices like USB drives.

After all the daemons have loaded, init launches a shell.

After the shell and daemons are loaded, by default X.Org graphical server is started.

The linux kernel is in the kernel.img file on SD card.

Some directories in root
------------------------

 * /dev		All devices attached, represented as special files, e.g. sda1 and null
 * /etc		Config files for software packages
 * lib		Software libraries contain shared code shared between multiple applications. These files in .so and are stored in this folder.
 * /mnt and /media	Any other filesystems attached
 * /opt		Software not installed by default
 * / proc	Special files allowing access to various statistics and configurations in kernel
 * /var		Contains all logs and other folders changing, including www

Debian Reference opens in web browser

Example of built in calculator is gcalculator

Methods of installing software
------------------------------

All of these methods, with exception of installing from source, use APT and dpkg

dpkg
----

 -  At centre of Raspbian
 -  installs from .deb file
 -  .deb file has 3 parts:
    * Debian binary containing version of dpkg needed
    * control archive with all info needed to install package
    * data archive containing actual software

APT
---

APT is frontend tool that makes using dpkg easier. Preconfigured with several repositories containing every official package available on Pi. Easy to add 3rd party repositories.

### Main Archive

main archive contains all software making up Raspbian

### contrib archive

Any package that requires other packages that aren't part of the main archive is included in contrib archive.

### Non-free archive

Using apt-get
-------------

Some packaged are metapackages - collection of packages. e.g. GUI

Can use * wildcard

For fun try apt-get moo

apt-cache search to search for packages, e.g.

    sudo apt-cache search apache2
    
Synaptic GUI Package Manager
----------------------------

    sudo apt-get install synaptic
    
Installing software from source
-------------------------------

Additional software needed to compile and install software (including make, gcc and g++). Generally this is the `build-essential` metapackage.

    sudo apt-get install build-essential
    
Download source code using browser or wget

Extract software from archive. e.g. to extract from a `.tar.bz2`:

    tarxvf xxx.tar.bz2

To build package:

    ./configure     # generates MakeFile
    make
    make install
    
Installing updates using apt-get
--------------------------------

    sudo apt-get update
    sudo apt-get upgrade
    
Installing updates using Synaptic
---------------------------------

1.  Refresh button
2.  Mark All Upgrages
3.  select Mark then click Apply

Other software you can install
------------------------------

IceDove is Thunderbird email client rebranded by Debian

    sudo apt-get install icedove

Bourne again shell (bash)
-------------------------

If you have configured Raspbian not to start Xfce desktop environment, bash will be automatically started after log in

To see which processing commands are running in background:

    ps -a
    
If you don't have keyboard with ~ key you can press F12.

Human readable `ls -h`

mv
--

Unlike `cp`, `mv` automatically moves whole file or folder and doesn't have -r option.

mv options:

    -f  Overwrites files and folders in destination folder
    -u  Only moves file if it is newer than file in destination folder
    
rm
--

 * be careful using -r and -f flags
 * to delete directory will need -f flag to force deletion of folder
 * -i prompts before deleting each file
 * -r recursively deletes files and folders

mkdir
-----

  *  -p creates any parent directories, e.g. `mkdir new/dir/with/parents -p`
  *  -v displays message for every directory created
  

Command line parameters for `chmod`
-----------------------------------

`-R`  changes all permissions for all the directories and files

`-v`  displays a message for every file that is processed

`-c`  only displays files that have their permissions changed


Kali
----

<www.kali.org> linux distribution designed for digital forensics and penetration testing.


**********


