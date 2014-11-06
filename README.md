Tontec-RPi-Screen
=================

How to set up a Tontec screen on a Raspberry Pi. I used [this screen on Amazon](http://www.amazon.com/gp/product/B00LN9MYCO).

All of these commands assume sudo/root. Very basic Linux terminology/usage expected.

# Setup

## System

### Install Packages

    aptitude update
    aptitude install build-essential zip

### Set Screen Resolution

    nano /boot/config.txt

Change:

    #framebuffer_width=1280
    #framebuffer_height=720

To:

    framebuffer_width=480
    framebuffer_height=320

## Screen

### Get Driver

    cd /home/pi
    wget https://s3.amazonaws.com/ttbox/35screen.zip
    unzip 35screen.zip
    unzip mzl350i-pi-ext.zip
    rm 35screen.zip mzl350i-pi-ext.zip

### Edit Driver Config

    cd /home/pi/mzl350i-pi-ext/src
    nano mzl350i.c

Change:

    int xsize=960, ysize=640
  
To:

    int xsize=480, ysize=320

Save the file, and...

    make

### Set to Run on Startup

    chmod +x /home/pi/mzl350i-pi-ext/lcd
    crontab -e
    
Add:

    @reboot /home/pi/mzl350i-pi-ext/lcd

## Terminal

### Set Font Size (Optional)

    nano /etc/default/console-setup

Change:

    FONTSIZE=""
    
To:

    FONTSIZE="20x10"

### Disable Raspberry Logo (Optional)

    nano /boot/cmdline.txt

Set

    logo.nologo


It takes a while for it to turn on with the screen. Apparently the screen takes a bit of resources... But works like a charm for me once on. I boot it to terminal and run console programs on these displays.
