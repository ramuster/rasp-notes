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

A really good book to get started, especially for children.

login default is pi
password default is raspberry

`startx`
	start X windows and desktop environment

`raspi-config`
	Config screen (use sudo)

To use another OS on NOOBS, hold shift when booting

`sudo shutdown -h now` Shuts down now

`sudo shutdown -r now` Restarts now

`sudo reboot` Reboots

`clear` Clears terminal screen

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

```
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

```
___________

Sonic Pi
========

Developed by Sam Aaron, Cambridge, uses Ruby

`sudo apt-get install sonic-pi`

Twinkle twinkle example:

```
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

```
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

As an aside, package managers are apt-get on Debian, yum on Fedora, pacman on Arch.

Find packages with apt-file
---------------------------

`apt-file` searches for all packages containing a file. Useful if you hae a single file or library missing from software you're installing. Need to install it, then `sudo apt-file update`

To search for packages related to `evince`:

    apt-file -l search evince

Can use apt-file to list contents of a package:

    apt-file list evince


Update firmware/kernel
----------------------

Check which versions of kernel and firmware installed:

    uname -a
    
    /opt/vc/bin/vcgencmd version
    
GitHub has latest versions. Download to SD card. Replace files in /boot

Alternatively, 'rpi-update' automates the process. To install and run:

    sudo apt-get install ca-certificates git-core
    sudo wget http://goo.gl/1BOfj -O /usr/bin/rpi-update
    sudo chmod +x /usr/bin/rpi-update
    sudo rpi-update
    

Adjust memory split between GPU and CPU
---------------------------------------

Use rasps-config or:

You can change memory configuration using different GPU firmware. Raspbian comes with a few preconfigured firmware files in /boot

    ls -l /boot/*.elf
    
Files starting with arm contain firmware images, with number indicating memory allocated to CPU, e.g. `arm128_start.elf` allocates 128MB for CPU. To activate a new memory split, copy relevant file to `start.elf` then reboot:

    sudo cp /boot/arm224_start/elf /boot/start.elf
    sudo reboot
    

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

`ps` to list processes running:

*  Get more info using `-f` option
*  List all processes with `-e`
*  See all info with `-ef`

Pressing `Ctrl-C` terminates running process by sending `SIGINT` signal to process.

To stop background process use:

 -  `kill 111`
 -  where 111 is process ID (PID)
 -  sends SIGTERM command

Moving around man pages or less/more:

	`q`          quit
	`spc` or `PgDwn`   down a page
	`b`   `^b` `PgUpup` back a page
	`Down` `Rtn`    down a line
	`Up`         up a line

To determine pi's IP address:

    ip addr | grep 'inet .* eth0'


To share Pi desktop
-------------------

Install VNC server on Pi:

    sudo apt-get install tightvncserver
    tightvncserver

You will require a password to access your desktops.

You can optionally enter a view-only password to allow read-only access.

VNC allows you to create as many virual screens as you need. Do not have to correspond to physical screens.

To access virtual screen need IP address of Pi and port address of screen:

VNCs base port is 5900 so to access screen number 1 use port 5901. e.g. `192.168.2.109:5901`

Install VNC client on Windows or Linux (like TightVNC).

On Mac use browser, location:

    vnc://192.168.2.109:5901


Controlling desktop of Mac or PC from Pi
----------------------------------------

Install VNC server on Windows or Linux. e.g. TightVNC.

Mac has integrated VNC server that you only have to enable in system preferences - sharing - enable screen sharing

Install VNC client like `xtightvncviewer` on Pi

    sudo apt-get install xtightvncviewer

Open a terminal on Pi and start client, passing it PC IP address and VNC port number:

    xtightvncviewer 192.168.2.100:5900


Turn Pi into Web Server
-----------------------

Lighttpd good lightweight choice:

    sudo apt-get install lighttpd

Point browser at Pi's IP address to see default webpage:

    http://192.168.2.1

To create own webpages add to lighttpd's document root, which by default is `/var/www/html`

Only members of group `www-data` have permission to write to it. Add pi user to www-data group and set permissions:

    sudo adduser pi www-data
    sudo chown -R www-data:www-data /var/www
    sudo chmod -R 775 /var/www
    logout

Lighttpd configuration file: `/etc/lighttpd/lighttpd.conf`


To create dynamic web content...
-----------------------------

Install PHP interpreter and enable FastCGI module in lighttpd server.

    sudo apt-get update
    sudo apt-get install php-cgi
    sudo lighty-enable-mod fastcgi
    sudo /etc/init.d/lighttpd force-reload

Have to add these lines to end of lighttpd configuration file:

```
fastcgi.server = (".php" => ((
    "bin-path" => "/usr/bin/php-cgi",
    "socket"   => "/tmp/php.socket"
)))
```

Then restart lighttpd server:

    sudo service lighttpd restart

To test, create file `/var/www/html/index.php`:

```
<?php
    phpinfo();
?>
```

Then point browswer to the server

Add wi-fi to Pi with wireless dongle
------------------------------------

Plug wi-fi dongle into USB port.

Run `lsusb`

Can look at boot message with:

    sudo dmesg | less

Get current status of wireless network with `iwconfig`

This searches for wireless network:

    sudo iwlist scan | grep ESSID

To connect to one of them you have to edit configuration file:

    /etc/network/interfaces

To connect to mywifi add lines:

    auto wlan0
    iface wlan0 inet dhcp
    wpa-ssid mywifi
    wpa-psk pa55w0rd

Either reboot or run: `sudo ifup wlan0`


Install XBMC (Raspbmc)
----------------------

Follow along using NOOBs (otherwise you have to use an installer program)

Linux primer
------------

In case of a directory, execute means enter the directory

Manage users
------------

Raspbian comes with user pi. Powerful, full admin rights.

Add new user using `adduser newuser`. Name should be lowercase only.

If you are impatient use `su` to switch to new user.

To give new user sudo rights, add to sudoers file, using visudo to invoke default text editor. To use different editor:

    sudo EDITOR=nano visudo

add line:

    peter ALL=(ALL) ALL

To remove user but not their files: `sudo userdel peter`

To remove user and their files:  `sudo userdel -r peter`

To lock an account:

    sudo usermod -L peter

To unlock an account:

    sudo usermod -U peter


**********************************

Learn to program your Raspberry Pi
==================================

Kevin Partner (kindle sample)
-----------------------------

Premier Farnell and RS Electronics are official RaPi suppliers.

Synaptic graphical package manager can search/find available packages.

	sudo apt-get install synaptic

Already installed on RaPi3

________

Raspberry Pi Server Essentials (Need to finish book in Adobe)
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

Raspberry Pi Cookbook - Simon Monk (go through again)
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

Raspberry Pi Essentials
=======================

Jack Creasey 2015
-----------------

Keep pi on insulated static-free surface if no case.

Desktop environment called lightweight X11 desktop environment (LXDE). 
Installed on top of window manager, which in this case is Openbox.

No automated updates or bug fixes. Instead use:
-----------------------------------------------

	sudo apt-get update
	sudo apt-get upgrade
	sudo apt-get autoremove

Building talking clock with script - text-to-speech bit not working...
======================================================================

**********

Raspotify
=========

From (https://github.com/dtcooper/raspotify)

_**Spotify Connect client for the Raspberry Pi that Just Works™.**_

## tl;dr

Install the Spotify Connect client on your Raspberry Pi,

```
curl -sL https://dtcooper.github.io/raspotify/install.sh | sh
```

## Introduction

Raspotify is a [Spotify Connect](https://www.spotify.com/connect/) client for
[Raspbian](https://www.raspberrypi.org/downloads/raspbian/) on the Raspberry Pi
that Just Works™. Raspotify is a
[Debian package and associated repository](https://en.wikipedia.org/wiki/Deb_\(file_format\))
which thinly wraps the awesome
[librespot](https://github.com/plietar/librespot) library by
[Paul Lietar](https://github.com/plietar). It works out of the box on all three
revisions of the Pi, immediately after installation.

## Download Latest Version

Head on over to the [releases](https://github.com/dtcooper/raspotify/releases/latest)
page to download themost recent version and install the Debian package. Or follow
the [directions below](#easy-installation).

### Requirements

Raspotify works on a Raspberry Pi running [Raspbian](https://www.raspberrypi.org/downloads/raspbian/).
You'll need a [Spotify Premium](https://www.spotify.com/premium/) account in order
to use Connect.

Raspotify should work on _any_ Pi but it has been tested on,

* Raspberry Pi (v1) model B
* Raspberry Pi 2 model B
* Raspberry Pi 3 model B

### Easy Installation

This command downloads and installs the Debian package and adds its apt repository,
which ensures you'll always be up to date with upstream changes.

```
curl -sL https://dtcooper.github.io/raspotify/install.sh | sh
```

That's it! Plug a speaker into your Pi on your local network, select the device
in Spotify et voilà!

### Hard installation

Essentially, here's what the easy installer does,

```
# Install curl and https apt transport
sudo apt-get -y install curl apt-transport-https

# Add repo and its GPG key
curl -sSL https://dtcooper.github.io/raspotify/key.asc | sudo apt-key add -v -
echo 'deb https://dtcooper.github.io/raspotify jessie main' | sudo tee /etc/apt/sources.list.d/raspotify.list

# Install package
sudo apt-get update
sudo apt-get -y install raspotify
```

Or just download the latest .deb package and install it manually:

 * [`raspotify-latest.deb`](https://dtcooper.github.io/raspotify/raspotify-latest.deb)

### Uninstalling

To uninstall, remove the package,

```
sudo apt-get remove -y raspotify
```

To completely remove Raspotify and its Debian repository from your system try,
```
sudo apt-get remove -y --purge raspotify
sudo rm -v /etc/apt/sources.list.d/raspotify.list
```

## Configuration

Raspotify works out of the box and should be discoverable by Spotify Connect on
your local network, however you can configure it by editing `/etc/default/raspotify`
which passes arguments to [librespot](https://github.com/plietar/librespot).

```
# /etc/default/raspotify -- Arguments for librespot

# Device name on Spotify Connect
#DEVICE_NAME="raspotify"

# Bitrate, one of 96 (low quality), 160 (default quality), or 320 (high quality)
#BITRATE="160"

# Additional command line arguments for librespot can be set below.
# See `librespot -h` for more info.
#
# To make your device visible on Spotify Connect across the Internet add your
# username and password which can be set via "Set device password", on your
# account settings, use `--username` and `--password`.
#
# To choose a different output device (ie a USB audio dongle or HDMI audio out),
# use `--device` with something like `--device hw:0,1`. Your mileage may vary.
#
#OPTIONS="--username <USERNAME> --password <PASSWORD>"

# Uncomment to use a cache for downloaded audio files. It's best to leave this
# as-is since permissions are properly set on directory `/var/cache/raspotify'.
#CACHE_ARGS="--cache /var/cache/raspotify"
```

After editing restart the daemon by running: `sudo systemctl restart raspotify`

## Building the Package Yourself

All that's required is [Docker](https://www.docker.com/) on a \*nix system with
[git](https://git-scm.com/) and [Make](https://www.gnu.org/software/make/). It
can be built on any amd64 platform that runs docker using Raspberry Pi's
cross-compiler (tested on Ubuntu 16.04 LTS and macOS El Capitan).

```
git clone https://github.com/dtcooper/raspotify
cd raspotify
make
```

There should be a built Debian package (a `.deb` file) in your project directory.

## License

This project is licensed under the MIT License - see the [`LICENSE`](LICENSE)
file for details.

## Acknowledgments

Special thanks to [Paul Lietar](https://github.com/plietar) for
[librespot](https://github.com/plietar/librespot), which Raspotify packages.
Without [librespot](https://github.com/plietar/librespot), Raspotify would simply
not exist.

*********

Guide to minimal Debian install on VirtualBox to emulate Raspberry Desktop Lite
===============================================================================

<https://www.raspberrypi.org/forums/viewtopic.php?p=1109518#p1109518>

Virtual Machine Playground
--------------------------

When trying to figure out what desktop environment works best for your Raspberry Pi, you would most likely reformat your SD / microSD card several times since there is no option of going back in time. You installed LXDE, but you didn't like it, so you reformatted and installed XFCE. Maybe you didn't like XFCE and reformatted again and tried MATE. Maybe you didn't like MATE and you just decided that you want to build your own desktop environment. In general, its a hassle.

This is where a virtual machine comes into play. The virtual machine itself runs on top of a standard computer running Windows, macOS, or Linux. The operating system on your standard computer is known as the host operating system. The virtual machine running on the host operating system is known as the guest operating system.

Since your Raspberry Pi is running Raspbian Lite, in reality, Rasbpian Lite itself is acutally a form of Debian Linux. Debian runs on a variety of hardware. The difference is that Raspian Lite is a customized distribution of Debian so that it can only run on the Raspberry Pi. The repository used in Raspbian Lite only works there as well.

So what does this all mean? The idea is that you can "simulate" an installation of a desktop environment on a virtual machine rather than installing it on Raspbian Lite directly. It's basically a playground where no damage can me made and allows you to gain ideas on what your desktop environment should look like. All you need to do is write down what changes you made and when ready, repeat them when you are ready to implement it on Raspbian Lite.

Requirements:

1. A normal computer with Linux, macOS, or Windows
2. Internet connection
3. A virtual machine virtualizer (VMware, Virtualbox)
4. A copy of Debian Minimal ISO 
You will basically be creating a Debian Linux minimal virtual machine. As you read along, you will notice how its very similar to Raspbian Lite.

Installation:

1. Install a virtual machine virtualizer on you computer. I will briefly go over the steps so make sure you have a general idea on how your virtual machine virtualizer works. For this guide, I will be using VMware Fusion since I am running this on a Mac. 
2. Download the Debian Minimal ISO image from the official website. Simply go to this link below:

<https://www.debian.org/CD/netinst/>

You can either obtain the ISO image directly or by downloading it using a BitTorrent client. For 64-bit computers, you would click on amd64. For 32-bit computers, you would click on i386. In reality, it doesn't matter which one to download since it would be running on a virtual machine anyway. The general rule is that a 64-bit computer should run a 64-bit virtual machine. 

2. Once you have the ISO image downloaded, you are now ready to create a virtual machine of Debian Linux. Open your virtual machine virtualizer and create a new virtual machine.

You will be creating a virtual machine using an ISO image.

You should be asked to locate the ISO image.

At one point, the virtualizer will recommend default settings. The default settings are fine for this tutorial but you can customize them if you wish.

Once you have created your Debian virtual machine, you are now ready to run it on your computer.

3. Start the Debian virtual machine.

Using your keyboard, select "Install" and press Enter. We like to do things using the command line interface! ;)

Select a language to use and press Enter

Select your location and press Enter.

Select your preferred keyboard keymap and press Enter.

It will ask you to enter a hostname. It doesn't matter what it is. Once you entered a name select Continue and press Enter.

It will ask you to enter a domain name. Again, it doesn't matter. Once you entered a name select Continue and press Enter.


You will be asked to create a root password for the root user account. You will need to remember this password since you will use it later. Once you entered a password select Continue and press Enter. You will be asked to verify the password.


You will now be asked to create a user account. It will first ask you to enter the name of the user. Once you typed a name select Continue and press Enter. 


You will then be asked to enter the login name of the user. Once you typed a login name select Continue and press Enter.


You will be now be asked to create a password for the user account. Once you entered a password, select Continue and press Enter. You will be asked to verify the password.


Select your time zone and press Enter.


Select "Guided - Use Entire Disk" and press Enter.


Since we only created one virtual hard drive disk for the virtual machine, only one disk will appear. Press Enter.


Select "All files in one partition" and press Enter.


All of the changes to the virtual hard drive will appear. Select "Finish partitioning and write changes to disk" and press Enter.


You will be asked to verify the changes. Select "Yes" and press Enter. Debian will now install on the virtual hard drive.


Select your location and press Enter. This will help in finding the closest package mirror in your location.


Select your package mirror and press Enter.


There is no need to enter any HTTP proxy information. Press Enter.


This asks if you want to share information on what packages are installed. Select either "Yes" or "No" and press Enter.



We only want the core of Debian in order to replicate Raspbian Lite. Unselect "Debian Desktop Environment" and "Print Server" by highlighting the option and pressing the Space Bar. Once you made your changes, press Enter. Debian will now only install the necessary packages to get it up and running.


The Grub bootloader is required to boot up Debian. Select "Yes" and press Enter.


Select the option "/dev/sda" since that is the location where Debian is installed. The Grub bootloader will use this location at each startup to find Debian. Press Enter.


The installation is now complete. On some virtualizers, you may need to unmount the Debian ISO image or else it will keep booting to it. Regardless, select "Continue" and press Enter to reboot the virtual machine.


4. After the virtual machine reboots, you should see the Grub bootloader. To boot Debian, select "Debian GNU/Linux" and press Enter.


Once Debian has booted, you will be asked to log in. If you noticed, the command line interface (CLI) looks exactly like Raspbian Lite which means it will feel very familiar. 

5. You will log in as root since we need to add a very important package known as Sudo. The Debian core does not include Sudo by default. Sudo allows a regular user to perform administrative commands like "sudo apt-get update" or "sudo apt-get install somepackage".

To log in as root, type in "root" as the login name, and press Enter. Enter the root password.


You are now logged in as root.

To install Sudo type in:

    apt-get install sudo
    
and press Enter. The Sudo package will automatically install. 

6. Now, you need to add your regular user account to the sudo group so that it can have access to the "sudo" command. To do this, type in:

    sudo adduser YOURUSERNAME sudo
    
and press Enter. Replace YOURUSERNAME in the command to your username you created earlier.

7. After you have successfully added your user account to the sudo group, restart the virtual machine. Type in:

    reboot

and press Enter.

8. Boot Debian by selecting it in the Grub Bootloader menu. Once booted, you should see the login screen. All that is left to complete the Debian virtual machine installation is to create a "snapshot" of the virtual machine. A snapshot basically stores the state of the virtual machine. For example, if you take a screenshot now, no display server, desktop environment, window manager, login manager, or any other packages are installed. Now, let's suppose that you installed the XFCE4 desktop environment and you decide that you want LXDE instead. If you "restore" the snapshot, you are basically going back in time to where you haven't installed anything! 

So before doing anything else at this point, create a snapshot of your Debian virtual machine. This will be your starting point. Refer to the documentation of your virtualizer if you do not know how to do this.


As you can see, a snapshot has been saved and I can restore to it at any time. Remember, you can create snapshots whenever you want. That's it for the installation. Now it's time to play with the Debian virtual machine!

Let's Play:

At this point, you don't have to do any steps I talk about here. You can just read along. This is just to demonstrate what you can do with the Debian virtual machine.

Now that we have created a snapshot, let's play around with the virtual machine. For this demonstration, let's install the XFCE Desktop Environment. To make things interesting, I will copy the exact same steps from the guide as if I'm running Raspbian Lite.

First, we need to install a display server which is Xorg. The command for that is:

    sudo apt-get install --no-install-recommends xserver-xorg


Next we need to install the XFCE GUI. The command for that is:

    sudo apt-get install xfce4 xfce4-terminal

The last thing we need is a login manager which is LightDM. The command for that is:

    sudo apt-get install lightdm

According to the guide, we need to restart. After restarting the Debian virtual machine:


It looks like we have the exact same thing as if we did this on Raspbian Lite! In general, the whole point of this section is for you to explore how desktop environments work. You can delete packages, customize the GUI, and so on without having to worry about reformatting your SD / microSD card or having to leave the commodity of your standard computer. If you decide that you want to start all over, simply restore the snapshot you created. That simple.

After you have created a perfect GUI setup on the Debian virtual machine, simply copy those steps you did and implement them on Raspbian Lite. The Debian virtual machine is your test bench.

**************

Raspbian Lite Guide - GUI
=========================

[GUIDE] Raspbian Lite with RPD/LXDE/XFCE/MATE/i3/Openbox/X11 GUI - Raspberry Pi Forums

By GhostRaider:

<https://www.raspberrypi.org/forums/viewtopic.php?f=66&t=133691#p890408>


RasPi GUI Table of Contents
---------------------------

1. Introduction
2. Memory Usage
3. Part 1 - Build the Foundation
4. Part 2 - Bring in the Furniture
5. Sample Screenshots
6. What Do I Use?
7. Virtual Machine Playground
8. Advanced - X11 Forwarding (Remote Applications)
9. Advanced - Custom Desktop Environment using i3 WM
10. Advanced - Custom Desktop Environment using Openbox WM
11. Extras

Requirements
------------

1. Any Raspberry Pi microcomputer
2. Raspbian Lite image
3. SD / microSD card (At least 4GB or higher, but it is possible to use smaller
storage space depending on your configuration)
4. Keyboard and Mouse (For using the GUI, but can vary depending on how the
Raspberry Pi will be used)
5. TV / Monitor (For seeing the GUI) (NOTE: For those wanting to use a
touchscreen, I do not cover this in this guide. You need to research this.)
6. A normal computer with Linux, macOS, or Windows (For burning Rasbian Lite
image to SD / microSD)
7. Internet connection

Introduction
------------

There are two official Linux distributions for the Raspberry Pi which are
Raspbian and Raspbian Lite. Rasbian is a full Linux distribution for the
Raspberry Pi which uses Raspberry Pi Desktop (RPD) desktop environment. The
desktop environment is the GUI (Graphical User Interface) of the operating
system. Raspbian includes preinstalled applications for word processing, games,
programming, and so on. This is great for beginners and people who just want to
start using their Raspberry Pi immediately.

But, some of us don't like that. We want the ability to work with a GUI, but
with our own preferences. In other words, we want to start with a clean
install, and then install whatever packages we need on top. Packages can
consist of desktop environments, drivers, compilers, applications, utilities,
and so on.

As a reward, there would be more storage space, less usage on memory, and GUI
customization! This is where Raspbian Lite comes into play.

Raspbian Lite is similar to that of a core. A core basically contains all the
essential packages needed to make the hardware on the Raspberry Pi work
correctly. Raspbian Lite was made so that the Pi can run as a headless system
where the Pi is controlled by commands sent from an external source. Raspbian
Lite does not contain a GUI but has a command line interface (CLI) which is
shown automatically if it is connected to an external display. Configuration of
Raspbian Lite can also be done via SSH (Secure Shell) from a computer connected
to the same network as the Raspberry Pi. More information on SSH in the
official Raspberry Pi documentation.

If you have ever heard of Arch Linux, Raspbian Lite is similar to that. Since
Raspbian Lite is supported by the Raspberry Pi Foundation, it is the preferred
operating system for most Raspberry Pi microcomputers.

To summarize, this guide talks about how to run Raspbian Lite with a GUI, in
this case you choose your desktop environment, RPD, LXDE, XFCE, or MATE. There
is an advanced section in this guide that talks about how to create your own
desktop environment if you are interested. The official Rasbian distribution
uses RPD as its default desktop environment, but reality, it is actually a fork
(or a branch) of LXDE. Other distributions such as Xubuntu uses XFCE as its
default desktop environment, and Ubuntu MATE uses MATE as its default desktop
environment. If you are not familiar with Linux desktop environments, be sure
to watch videos or research on the types of GUIs available. That way, you will
have and idea of what GUI to install, if any.

For those that are really consciousness about memory usage, a desktop
environment based on LXDE would be a recommended choice. For those that prefer
a prettier or modern look, then XFCE or MATE would be a recommended choice.
However, both do the exact same job which is to make your Raspberry Pi a simple
desktop computer that is easy to use. This is assuming that you want to use a
prebuilt desktop environment. Otherwise you are free to create your own desktop
environment.

So why do this? Well, you decide how your desktop looks like, you decide what
applications to install, and finally, you decide what do to next!

Let's begin!

Memory Usage
------------

Before beginning to install Raspbian Lite with a GUI, let's explore memory
usage. In a nutshell, the less memory your Raspberry Pi consumes, the more
applications it can run. Raspbian Lite itself consumes very little memory since
it is a core. As discussed earlier, a core only has the essential packages that
make the hardware on the Raspberry Pi work.

NOTE: The memory used shown in the screenshots may be different than what your
installation may actually use. Use this information as a reference to determine
what desktop environment is right for you.

So how much memory does Raspbian Lite itself use?

    free -m

If we take a look at the screenshot, the memory is displayed in megabytes. This
Raspberry Pi has 925MB of total memory. Some of the memory is internally
allocated to the GPU by default. This means that the operating system and
applications can use up to 925MB of memory.

Currently, Raspbian Lite is using 30MB of memory. Very impressive. This means
that the available memory to use is now 895MB.

How does this compare to Raspbian with RPD?


On a clean installation, Raspbian with RPD is using about 90MB of memory.
That's pretty good. Now, let's see what the memory usage is with Raspbian Lite
running various GUIs.

If Raspbian Lite is running RPD Desktop Environment:


Here we see that Raspbian Lite with RPD is using about 76MB of Memory.

If Raspbian Lite is running LXDE Desktop Environment:


Here we see that Raspbian Lite with LXDE is using about 97MB of Memory.

If Raspbian Lite is running the XFCE Desktop Environment:


Here we see that Raspbian Lite with XFCE is using about 107MB of Memory.

If Raspbian Lite is running the MATE Desktop Environment:


Here we see that Raspbian Lite with MATE is using about 101MB of Memory.

Running a desktop environment with Raspbian Lite can consume quite a bit of
memory. Now, we have to remember that Linux operating systems are flexible. Not
every package required for a desktop environment is needed to be installed.
This means that memory usage (as well as storage space) can be lowered even
further, but you would have to be very familiar with how a package as well as
its dependencies work. Not installing a required package or dependency may
bring unwanted behavior. However, the good news is that it won't break your
Raspberry Pi so long it is software related!

Part 1 - Build the Foundation
-----------------------------

In this part, we will focus on preparing Raspbian Lite.

1. Download the latest Raspbian Lite image.
2. Format the SD / microSD card with Raspbian Lite (Plenty of guides out there
on how to do this. For macOS, Linux, and Windows users, Etcher is an easy to
use application that can help you do this.)
3. Insert the SD / microSD card into the Pi.
4. Connect the Pi to the Internet using an Ethernet cable. If you want to use
Wi-Fi instead, you will have to read on how to configure your wireless receiver
using the command line after your Pi has finished booting.
5. Connect your TV / Monitor and keyboard. (Mouse is optional at this time.)
Turn on the Pi. The Pi should boot up successfully and a prompt to log in will
appear.
6. Log into Raspbian. The username is pi and the password is raspberry.

7. We need to expand the file system so that Raspbian takes full use of the SD/ microSD space. To do this, we need to use raspi-config. Type in:

    `sudo raspi-config`

and press Enter.

8. The Raspberry Pi Software Configuration Tool (raspi-config) main menu will
appear. The option we are interested is option #7 (Advanced Options). Select
that option using the arrow keys on your keyboard and press Enter. Then select
option #A1 (Expand Filesystem) and press Enter. A message will appear saying
that the boot partition has been resized. Select OK using arrow keys on your
keyboard and press Enter. The main menu will reappear. Select Finish at the
bottom of the menu and press Enter. A popup message will ask you to reboot your
Raspberry Pi. Reboot the Pi.

9. Log into Raspbian again. We want to make sure we currently have the latest
files and packages so type in:

    `sudo apt-get update`

and press Enter. If there are updates available, install them. To install the
updates, you would type in the letter "y" when asked "Do you want to continue?"
and then press Enter. When finished, the message "pi@raspberrypi:~ $" will
appear signifying that the Pi is ready to receive a command. Now, type in:

    sudo apt-get upgrade

and press Enter. If there are updates available, install them. Now, type in:

    sudo apt-get dist-upgrade

and press Enter. If there are any updates available, install them.

If packages were updated and installed, then these packages were stored
somewhere in the SD / microSD card. We need to delete them so that they don't
take up valuable space. To clean up leftover packages, type in:

    sudo apt-get clean

and press Enter.

10. At this time, you may want to configure your localization settings which
include language, keyboard layout, and regional settings. To change this, we
need to go back to raspi-config. Type in:

    `sudo raspi-config`

and press Enter.

The option we are interested is option #4 (Localization Options). Select that
option and press Enter. You will be presented with 4 different options.

Begin by selecting option #I1 (Change Locale) and press Enter. Find your locale
by scrolling through the list using the up and down arrow keys on your
keyboard. By default, en_GB.UTF-8 UTF8 will contain an asterisk, meaning that
Raspbian Lite is using this locale. However, this may be incorrect if you live
in another country, like the US. You can deselect this locale by highlighting
it and pressing the Space bar on your keyboard. For example, if you live in the
US, then the locale used should be en.US.UTF-8 UTF8. You would find this locale
on the list and then press the Spacebar to select it. An asterisk will appear
meaning that this locale will be used. Once you are ready, press Enter. A popup
will appear asking you to select the default locale used for the entire system.
Select the same locale you selected previously by highlighting it using the up
and down arrow keys and then press Enter. Raspbian Lite will configure your
system automatically and return to the main menu.

NOTE: You may notice that after you have changed your locale, if you change
other internationalization settings, you may get some text randomly popping up
at the bottom of the screen saying that setting the locale has failed and that
LC_CTYPE, LC_Message, LC_ALL complain that there is no such file or directory.
No problem. Exit out of raspi-config and type in:

    sudo reboot

and press Enter. This will reboot your Pi. Now you can reopen raspi-config and
you will no longer see that weird message. Don't ask me why that hasn't been
fixed yet.

Return to the Localization Options menu by selecting option #4 and press Enter.

Now configure your timezone by selecting option #I2 (Change Timezone) and press Enter.

Select your geological area using the arrow keys and press Enter. Select
your region or city and press Enter. Raspbian Lite will configure your system automatically and return to the main menu.

Return to the Localization Options menu by selecting option #4 and press Enter.

Now configure your keyboard layout by selecting option #I3 (Change Keyboard Layout) and press Enter. Select your keyboard model using the arrow keys and press Enter (In a case where you don't know what keyboard model to select, the Generic 105-key (Intl) PC keyboard model would be good choice). Now, you will select the keyboard layout. Select the appropriate keyboard layout and press Enter (If you don't see your keyboard layout, select Other and press Enter.

Select the keyboard language and press Enter. Now you will be presented with
various keyboard layouts corresponding to your language. Select the appropriate
layout and press Enter). The next few prompts may ask you about configuring the
AltGr and Compose key. This is up for you to decide. Select the appropriate
options and press Enter. You will then return to the main menu.

If you are using a Raspberry Pi 3, this microcomputer come equipped with a
built in Wi-Fi/Bluetooth wireless receiver. You may want to change the Wi-Fi country settings. Return to the Internationalization Options menu by selecting option #4 and press Enter. Now configure your Wi-Fi country settings by selecting option #I4 (Change Wi-Fi Country) and press Enter. Select your
country using the arrow keys and press Enter. A confirmation message will
appear confirming your selection. Select OK. You will return to the main menu.

12. Select Finish and press Enter. If you are asked to reboot, then reboot the Pi by selecting Yes and pressing Enter. If you are not asked to reboot, reboot anyways by typing in:

    `sudo reboot`

13. That's it! The foundation has been built! The Pi is ready to be used now, well obviously without the GUI. We have built the house but there's no furniture inside.

Part 2 - Bring in the Furniture
-------------------------------

This next part focuses on installing a GUI on top of Raspbian Lite. In order to
have a GUI, we need these 4 things:

1. Display Server
2. Desktop Environment
3. Window Manager
4. Login Manager

Since we need 4 things, to make life easier, these 4 things are:

1. Xorg Display Server
2. Raspberry Pi Desktop (RPD) or Lightweight X11 Desktop Environment (LXDE) or
XFCE Desktop Environment (XFCE) or MATE Desktop Environment (MATE)
3. Openbox Window Manager (RPD/LXDE) or XFWM Window Manager (XFCE) or Marco
Window Manager (MATE)
4. LightDM Login Manager

For those that know about Linux, you may be wondering why the login manager
chosen here is LightDM. For the most part, it is lightweight and it looks nice.
But one feature that I believe stands out from other login managers is the
ability to run Synergy client without errors. Synergy is a utility that allows
you to use a computer's mouse and keyboard (Windows, Mac, or Linux) and share
it with another computer, in this case, a Raspberry Pi. Of course you can
install another login manager if you don't want LightDM.

Some users may not want a login manager. This is perfectly fine depending on
how you will use your Raspberry Pi. For example, we may want the Pi to boot
into the command line always and if there is a need to launch a desktop
environment, a simple command will let you launch it. Continue to read on for
more information.

Since we are focusing on Raspbian Lite, then the GUI installed will also be
"lite". I understand that "lite" can have different meanings, but beginners are
the main focus here. The important thing here is for users to personalize their
Pi, without relying on prebuilt Raspbian. I believe these are the best GUI
options. As always, you are free to use whatever you want. Moving forward, we
will be installing the core of RPD, LXDE, XFCE, or MATE. This will give us only
the GUI. There won't be any applications installed other than the required
PIXEL, LXDE, XFCE, or MATE components such as a file manager, terminal, and
settings.

1. Turn on your Pi and log in. We will install Xorg. To do this type in:

    `sudo apt-get install --no-install-recommends xserver-xorg`

and press Enter. There will be a lot of dependent packages to install but these
must be installed for the GUI to work. Install the packages.

If you only install xserver-xorg, you will not have the ability to launch the
Xorg Display Server from the command line. This would be a problem if you are
not planning on installing a login manager. Otherwise, you do not need to do
this. If this is the case, you may want to also install xinit by typing in:

    sudo apt-get install --no-install-recommends xinit

and press Enter. There will be some more dependent packages to install but
these must be installed so that you can have the ability to start the Xorg
Display Server from the command line if no login manager is installed. Install
the packages.

-----

2. Now, choose your path:

Raspberry Pi Desktop (RPD) GUI
------------------------------

1 (RPD). You're reading this part because you want to install RPD right? Let's
continue. For this desktop environment, you have two choices. You can either
install the basic RPD desktop environment or a stripped version of it. The
basic RPD desktop environment is the same as the one included in the regular
Raspbian distribution, but without preinstalled applications. Essentials such
as settings, task manager, terminal and file manager are included. To install
the basic RPD desktop environment, type in:

    sudo apt-get install raspberrypi-ui-mods

and press Enter. There will be a lot of dependent packages to install but these
must be installed for the GUI to work. Install the packages.

The stripped version of the RPD desktop environment only contains the file
manager and settings for appearance, audio, network, and bluetooth. There is no
trash support, no mounting of drives, or terminal included since the required
components are not installed by default. No other applications are included
either. However, you can add these components later if you wish. If you want to
install the stripped version of the RPD desktop environment with LXTerminal
(optional) as well as trash and drive mounting (optional), type in:

    sudo apt-get install --no-install-recommends raspberrypi-ui-mods lxterminal gvfs

and press Enter. There will be a lot of dependent packages to install but these
must be installed for the GUI to work. Install the packages.

2 (RPD). Openbox Window Manager is installed by default when you install RPD.
You do not need to do anything here.

LXDE GUI
--------

1 (LXDE). You're reading this part because you want to install LXDE right?
Let's continue. We will be installing the LXDE core. When you install LXDE,
some essentials such as settings, terminal and file manager are included.
LXAppearance is used to change the look of applications such as panels, icons,
progress bars, cursors, and so on. This is optional to install but I recommend
installing it in order to give yourself more customization abilities. To
install LXDE with LXAppearance type in:

    sudo apt-get install lxde-core lxappearance

and press Enter. There will be a lot of dependent packages to install but these
must be installed for the GUI to work. Install the packages.

2 (LXDE). Openbox Window Manager is actually installed by default when you
install lxde-core. You do not need to do anything here. You can customize the
look of the titlebar using the Openbox settings which is also installed by
default. By using LXAppearance and Openbox settings together, you chose what
LXDE looks like!

Now, go to STEP 3.

XFCE GUI
--------

1 (XFCE). You're reading this part because you want to install XFCE right?
Let's continue. We will be installing the XFCE core. When you install XFCE,
some essentials such as settings and file manager are included. By default,
XFCE uses XFCE4 Terminal. This is optional to install, however if you choose
not to install it, then XTerm will be the default Terminal app.. To install
XFCE with XFCE4 Terminal, type in:

    sudo apt-get install xfce4 xfce4-terminal

and press Enter. There will be a lot of dependent packages to install but these
must be installed for the GUI to work. Install the packages.

2 (XFCE). XFWM Window Manager is actually installed by default when you install
xfce4. You do not need to do anything here!

Now, go to STEP 3.

MATE GUI
--------

1 (MATE). You're reading this part because you want to install MATE right?
Let's continue. We will be installing the MATE core. When you install MATE,
some essentials such as settings, terminal, and file manager are included. To
install MATE, type in:

    sudo apt-get install mate-desktop-environment-core

and press Enter. There will be a lot of dependent packages to install but these
must be installed for the GUI to work. Install the packages.

2 (MATE). Marco Window Manager is actually installed by default when you
install MATE. You do not need to do anything here!

Now, go to STEP 3.

-------------

3 (STEP 3). Finally, we need to install LightDM login manager. If you have
installed the basic or stripped version of the RPD desktop environment, then
LightDM package is installed automatically so you can skip this step. As of the
release of Raspbian Stretch, if you installed the XFCE desktop environment,
LightDM is also installed automatically so you do not need to do this step.
Otherwise, to install LightDM, type in:

    sudo apt-get install lightdm

and press Enter. Install the packages.

If you choose not to install a login manager but you did install xinit earlier,
then this means that everytime your Pi boots, you will always boot into the
command line. However, the desktop environment is already set up for you and is
ready to be launched at any time.

4. Everything we need to have Raspbian Lite with a GUI is ready! Fortunately,
we don't have to do anything else but reboot! Reboot your Pi. When it finishes
booting, you will see the LightDM login screen. From here, you will need use
both a keyboard and a mouse. Log in and you should now see either RPD, LXDE,
XFCE, or MATE desktop!

Otherwise, if no login manager was installed, then just login via the command
line! At anytime, you can launch the Xorg Display Server by typing in:

    startx

and press Enter. You should now see either RPD, LXDE, XFCE, or MATE desktop!
From here, you will need use both a keyboard and a mouse.

5. So what now? This is where you decide what you want to do with your custom
Rasbian Lite installation with a GUI. You can change the look, install
applications, start programming, do what is necessary to make it work the way
you want it to!

What Do I Use?
--------------

So the question is, what desktop environment does the author of this thread use? I actually use my own custom desktop environment. Let's take a look at my Raspbian Lite desktop:

This a custom desktop environment using Openbox as the foundation. First
impression; it looks clean, simple, and beautiful (to me of course!). The main reason I don't use a prebuilt desktop environment is because I want control over how the desktop environment looks. However, I will say that XFCE would be my preferred choice if I were to use a prebuilt desktop environment. This is how my desktop environment is laid out:

The top and bottom panels are Tint2 panels. I customized the Tint2 panels to my liking to achieve this look. The notifications displayed on the desktop are from xfce4-notifyd. I want to be notified of things such as disconnection from the Internet, or Raspberry Pi is getting hot, or other notifications thrown by Raspbian Lite. Let's see the memory usage of my custom desktop environment:

The desktop environment itself is using around ~146 MB which is very good.
There is plenty of memory left for applications. Finally, here is a look of how the desktop looks when there is a lot of activities going on:

And that's my brief tour of the desktop environment I use on Raspbian Lite!

That's the reason why I wrote this guide. For you to learn how to become
independent from regular Raspbian and personalize Raspbian Lite to your own liking. Personalization is of the greatest things about Linux in general.

Virtual Machine Playground
--------------------------

Installing a GUI on Raspbian Lite can either be easy or hard. If you want a particular desktop environment, you just follow the steps to install that environment. For the majority of Raspberry Pi users, that's more than enough.

But what if we wanted to get our hands dirty? In other words, what if we want
the desktop environment to be focused solely on a particular application. For
example, the desktop environment should just be focused on a web browser, or it
should just be focused on a music player. Is it really necessary for a file
manager to be in an operating system that its primary focus is to display web
pages? Is it really necessary for an operating system to be running blown
desktop environment just to play music? This is where you explore ideas for
what kind of GUI Raspian Lite should have.

Can you explore GUI ideas directly on Raspbian Lite? Yes, but the idea of a
virtual desktop is for you to explore those GUI ideas in the comfort of your
own computer. It is basically a playground. You don't need to worry about
reformatting SD / microSD cards, and you can go back in time using a feature
called "snapshots" included in most virtual machine virtualizers in case if you
made a mistake or you broke your installation. There is no risk. Not only that,
but you also learn more about the inner workings of Linux.

Once you build your desktop environment to your liking in the virtual machine,
you simply follow the steps you did on the virtual machine and apply them to
your Raspbian Lite installation. If you are interested in reading more on this
topic, simply click on the link below to see the full tutorial:

<https://www.raspberrypi.org/forums/viewtopic.php?p=1109518#p1109518>

Advanced - X11 Forwarding (Remote Applications)
-----------------------------------------------

X11 Forwarding is an SSH remote tunneling system where you can run applications
installed on a Linux system remotely from another system running Windows,
macOS, or Linux.

For example, let's say that you have a clean Raspbian Lite installation on your
Raspberry Pi. Now, if you physically want use your Raspberry Pi like a normal
computer (with monitor, keyboard, mouse), then most likely you want to install
a GUI on Raspbian Lite. However, if you only care about running specific
applications on Rasbian Lite and don't have a need to use it as a normal
computer (no monitor/keyboard/mouse/GUI), then X11 Forwarding may be something
you'd like to use.

Here's how it works. You would connect to your Raspberry Pi via SSH with X11
Forwarding option enabled from another system. When it is connected, if you
type in an application name, lets say "leafpad" and press Enter, the
application will open on your desktop. That's it! So in other words, your
system will show you the application's GUI while the Raspberry Pi handles the
workload for that application. Pretty neat right?

If you want to use X11 Forwarding, it's very simple. Follow the instructions
below:

1. Follow the steps on Part 1 - Build the Foundation to have a clean
installation of Raspbian Lite. If you already installed a desktop environment
and still want to enable X11 Forwarding, continue to step 2.

2. You need to enable SSH on Raspbian Lite. Using the command line (or Terminal
window), type in:

    sudo raspi-config

and press Enter. Select option #5 (Interfacing Options) and press Enter. Then
select option #P2 (SSH) and press Enter. You will be asked if you want to
enable the SSH server. Select "Yes" and press enter. A popup will open saying
the SSH server has been enabled. Select "Ok" and you will be returned to the
main menu. Select Finish and press Enter to exit raspi-config.

3. Obtain the IP address of your Raspberry Pi. Using the command line (or
Terminal window), type in:

    hostname -I

and press Enter. Take note of that IP address since you need it to connect to
the Raspberry Pi via SSH.

4. Reboot the Raspberry Pi by typing in:

    sudo reboot

and press Enter.

5. Once the Raspberry Pi has been rebooted, you no longer need to physically
use the Raspberry Pi since you can now remotely log onto the Raspberry Pi via
SSH.

6 (Windows). You will need to install an SSH client with X11 Forwarding
capabilities on the computer you wish to run the Raspberry Pi applications on.
In order for the applications to appear on the computer, you also need to
install Xorg Server on the computer as well. For Windows, there is an
application called MobaXterm which is free and it is an SSH client that
integrates Xorg Server. No need to install Xorg Server separately.

Create a session by clicking on the "Session" icon on the toolbar.

Image

Enter the IP address of the Raspberry Pi as well as the Raspberry Pi username.
Make sure that X11 Forwarding is enabled by click on the Advanced SSH Settings
tab. When ready, click OK. You will be asked to enter the password.

Image

Once you are logged in, you are ready to launch Raspberry Pi applications
remotely! To launch applications remotely, type in:

    nameOfApp &

and press Enter. The "&" symbol allows you to continue to use the MobaXterm
window and open multiple Raspberry Pi applications without freezing it.

Image

6 (macOS). You will need to install an SSH client with X11 Forwarding
capabilities on the computer you wish to run the Raspberry Pi applications on.
In order for the applications to appear on the computer, you also need to
install Xorg Server on the computer as well. On macOS, you will need to install
XQuartz since no application comes with Xorg Server integrated. Once XQuartz
has been installed, you can use Terminal to connect to your Raspberry Pi. To
start an SSH session with X11 forwarding, type in:

    ssh -Y username@raspberrypiaddress

where "username" is your Raspberry Pi username and "raspberrypiadrress" is your
Raspberry Pi's IP address. Then press Enter. You may be asked if you are sure
if you want to connect to the host. Type in "yes". Enter the Raspberry Pi
password when asked.

Image

Once you are logged in, you are ready to launch Raspberry Pi applications
remotely! To launch applications remotely, type in:

    nameOfApp &

and press Enter. The "&" symbol allows you to continue to use the MobaXterm
window and open multiple Raspberry Pi applications without freezing it.

Image

For those wondering about memory usage, the memory used on Raspbian Lite is
only the application as well as essential processes. The usage is very small.
No Xorg, no desktop environment, no login manager memory consumption. More
memory, more storage space!
Image
Advanced - Custom Desktop Environment using i3 WM

Let's get serious now. The real reason to use Raspbian Lite is to make the
Raspberry Pi microcomputer work for a specific application purpose. The
operating system should be customized to that specific application. What kind
of applications?

Anything really. Some people use the Raspberry Pi just for:

 * Clock and Weather
 * Internet Radio
 * Web Browser
 * Music Player
 * Surveillance
 * Retro Game Console

and the list goes on and on. What will you be building? To understand the idea
of a custom desktop environment, I will go over some examples and maybe it can
give you an idea of how to approach and implement your idea. If you are
interested in reading more on this topic, simply click on the link below to see
the full tutorial:

<https://www.raspberrypi.org/forums/viewtopic.php?p=1109520#p1109520>

Advanced - Custom Desktop Environment using Openbox WM
------------------------------------------------------

Openbox is a window manager that can run as a standalone desktop environment,
or with another desktop environment. Window managers normally handle
application windows as well as their window decorations and effects. If you run
Openbox as a standale desktop environment, you would have control over how your
desktop environment looks. Openbox does not have any panels, desktop icons,
wallpapers, or other UI elements since that is not the job of Openbox. You
would have to provide that yourself.

There are some benefits of going this route. The main benefit is resource
usage. Since you would only have Openbox running, most of the memory used will
be used for applications that you run. The second benefit is simplicity. There
are many users who only want to run a single application and don't need a full
desktop environment. Third benefit is customization. You can build your own
desktop environment and use Openbox as its window manager.

If you think Openbox window manager sounds like something you want to use on
Raspbian Lite, let's continue!

1) In order to use Openbox, you need to have Xorg Display Server installed. To
install Xorg, type in:

    sudo apt-get install --no-install-recommends xserver-xorg

and press Enter.

If you are planning on not using a login manager, then you will also need to
install Xinit. This will allow you to start Openbox manually. To install Xinit,
type in:

    sudo apt-get install --no-install-recommends xinit

and press Enter.

2) Now you need to install Openbox. Remember that Openbox does not include any
applications other than Openbox Configuration Manager. If you need to use
Terminal in Openbox, you have to install one yourself. In the command below, I
included LXTerminal. Otherwise, install your own Terminal if needed. To install
Openbox with LXTerminal, type in:

    `sudo apt-get install openbox lxterminal`

and press Enter.

3) If you are planning on installing a login manager, to install LightDM login
manager, type in:

    `sudo apt-get install lightdm`

and press Enter.

However, if you plan on starting Openbox manually, then you need to do some
more work. First, we need to generate an .xinitrc file. This file will have all
the commands to start your custom desktop environment. For this case, we only
need to implement the Openbox command to the file.

First, copy a sample xinitrc file and paste it to your home directory. To do
this type in:

    cp /etc/X11/xinit/xinitrc ~/.xinitrc

and press Enter. Now, edit the xinitrc file by typing in:

    nano ~/.xinitrc

and press Enter.

Image

Delete everything inside this file. After that, copy the command below onto
your xinitrc file:

    exec openbox-session

Image

Save the xinitrc file.

4) Now, restart your Raspberry Pi. For those that installed LightDM login
manager, you should see LightDM appear. Login with your username and password
and you should now see the Openbox desktop! Well actually, you would see
nothing. If you right-click, you will see the Openbox menu.

For those that did not install a login manager, simply log onto the Raspberry
Pi. To start Xorg with Openbox, type in:

    startx

and press Enter. Similarly, you should see nothing but a blank screen. If you
right-click, you will see the Openbox menu.

That's it! After this, you decide what to do next with Openbox!

For those wondering about memory usage, Openbox uses very little memory.

Raspberry Pi Configuration Tool
-------------------------------

If you have used the regular Rasbian distribution, you probably noticed that
there was a tool for configuring the Raspberry Pi. No problem, you can bring it
back in Raspbian Lite.

In Terminal, type in:

    sudo apt-get install rc-gui

and press Enter. Install the necessary packages. You may have to reboot your
Raspberry Pi to see the configuration tool in your Applications menu or
Preferences menu.


***************************************

Raspberry Pi Introduction/Documentation
=======================================

__Greg Loyse 2017__


System specs
------------

Explore these commands:

```
uname -a
head -n /etc/issue
cat /proc/partitions
grep MemTotal /proc/meminfo
grep "model name" /proc/cpuinfo
hdparm -i /dev/sda
hwinfo
lshw
```

Modules & Devices
-----------------

List the current modules:

    lsmod
    
List the current USB devices:

    lsusb
    
Exercise
--------

Determine the device that is used as a keyboard.

How can you do this in a way that is guaranteed to work even if naming is ambiguous?

Even if you disconnect all of these and run lsusb (you’d have to be logged in remotely to do this of course) there will still be some usb devices listed. Why? Where are these devices?

The list of modules returned by lsmod is long and confusing. Google some of them and try to identify their purpose. Make sure to know what 8192cu does.

Knowing what you know now, how would you problem solve a usb wireless device not working?

Identify processes
------------------

Use top or stop (needs installing)

Get ASCII documentation
-----------------------

    man ascii
    
`hexdump` displays files in hexadecimal


***********************************

Raspberry Pi for complete beginners
===================================

__Antun Peicevic 2015 Geek University Press__

<http://geek-university.com>


DSI display connector used to attach LCD panel

`ip addr` displays network settings
 
Raspbian repository at <http://archive.raspbian.org>


raspi-config
------------

1. Expand filesystem:

    - raspbian root file system is 2GB by default
    - expand to use whole SD card
    - already done if used NOOBs
    - reboot

2. Change keyboard layout

    - can choose which key to function as AltGr if your keyboard doesn't have one
    - can also choose compose key
    - can choose to use Ctrl-Alt-Backspace to terminate X-server

3. Overclock

    - if problems, hold shift after rebooting to disable overclocking

4. Change hostname

    - set to raspberrypi by default
    - only letters, numbers and hyphen allowed
    - reboot
    - can also change manually by editing `/etc/hostname`. Then edit `/etc/hosts` to change all instances of old hostname to new. `reboot`


omxplayer
---------

Video/audio player installed by default. Can be used from console without GUI.

To see included Big Buck Bunny video:

    omxplayer /opt/vc/src/hello_pi/hello_video/test.h264
    
To enable sound output to HDMI port use `-o hdmi` option

Commands while video playing:

```
q           Exit
Space or p  Pause/Resume
-           Decrease Volume
+           Increase Volume
Left        Seek -30
Right       Seek +30
Down        Seek -600
Up          Seek +600
```

`sort -c` checks if lines already sorted. Reports first unsorted line

/var/log/messages most important log file on Pi

`tail -f` will show updating lines

```
ps -aux     To get full ps options:

    USER    - owner of process
    PID     - process ID
    %CPU
    %MEM    - ratio of process resident set size to physical memory
    VSZ     - virtual memory usage (KiB)
    RSS     - resident set size - non swapped physical memory (KiB)
    TTY     - controlling terminal
    STAT    - multi-character process state
    START   - starting time/date of process
    TIME    - cumulative CPU time
    COMMAND - command used to start process
```

top
---

Advantage over ps is updated every few seconds

```
    PR      - priority
    NI      - nice valul
    VIRT    - total virtual memory
    RES     - non-swapped physical memory (resident)
```

By default, top sorts its entries by CPU usage. Other sort options:

    - memory, press M
    - reverse, press R
    - CPU, press P
    - by other fields, use `<` and `>`

Kill processes in top by pressing `k` and specifying PID


To access Pi desktop remotely on Windows
----------------------------------------

Install xrdp on pi

On Windows computer, open Remote Desktop Connection program:

`start > run > mstsc` Type IP address Pi, then connect. Login at xrdp prompt.

********

