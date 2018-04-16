---
layout: post
title:      "Setting up an Ubuntu Dual Boot"
date:       2018-04-16 18:57:22 +0000
permalink:  setting_up_an_ubuntu_dual_boot
---

Flatiron had recommended that I switch to a local environment once I started Rails.  I tried the virtual machine with Lubuntu. Getting it set up was a lot of googling, help from Dakota, and Luke because my system settings were off. Flatiron does have great help support for setting up systems but I was encountering weird situations and in the end I decided to seek out how to set up a dual boot Windows with Linux on my system. 

There is a lot that goes into setting up a dual boot system. Flatiron has this link that started to help me with the process of setting up Linux, but not actually what goes into everything you need before installing Ubuntu

First you need to go to this [link](https://itsfoss.com/install-ubuntu-1404-dual-boot-mode-windows-8-81-uefi/), which I have summarized below.

1. Back up your computer - if you have concerns.  I had just did a hard reset on my computer so I had nothing on it to back up.
2. Create a live USB/disk of Ubuntu.  Now this was the fun part! I went to Target and purchased a cheapo USB drive for $5.99. I had several USB drives at home but with important stuff on them. When you create the live USB you have to reformat your flash drive which was not ideal for my situation. I quickly found the cheapest one at the store, came home and attempted the next step... MAKE SURE YOU USE FLASH 3 USB !
3. Download Ubuntu on your computer. Use the 16.04 version! **DO NOT use the most recent upgrade 17.10!!!.** I used this version initially because I the most recent would be the best option right? Wrong. There are so many bugs in this version and you cannot use Zoom on this version either. One specific bug 17.10 has is that the screen rotates and flips. When I was trying to set up Ubuntu it kept rotating my screen sideways and back and forth and I had to keep turning my head to be able to read everything. Not to mention that when your screen rotates, so does your mouse! Very confusing for the brain. When you login, there are also bugs that the screen shakes and other weird occurances. 
4. Download Universal USB installer. 
5. Open Universal USB installer and follow the directions. Find your Ubuntu download and start the process fo create your bootable USB drive.
6. You need to figure out how much RAM you have for your computer. You should be able to do a search for this. Write that number down for later reference.
7. You need to partition your harddrive to be able to have space for your new system. To manage your harddrive space you would click on Computer => Manage => Disk Management. If you have Windows 8 and older you can search disk management in the bottom search box of your windows bar and select the option that is "Create and Format hard disk partitions".
8.  Once your there you would right click on your WindowsC: drive (most likely that would be what yours will say, and it will be your largest MB/GB amount.  You will see an option to shrink volume. I shrunk mine by 150GB, but you don't need all of that. I am using my computer solely for development so I didn't care about losing space on my Windows side. You need about 3G for Ubuntu, 2X your harddrive amount, and whatever you want for your system extra space. I had read in many places a minimum of 15, but 20 was probably better. You can see I did much more since I used a total of 150G.
9.  You need to disable secure boot in order and change the order of your drives for your boot order. I recommend going to the site above and looking at their startup screenshots. You need to get to your BIOS settings. I recommend googling your computer and BIOS settings to see what f key is going to get you there. Some sources say f10, f11, I think mine was f9. [Here's a link about boot order and boot menus](https://www.winhelp.us/computer-boot-order.html) The pictures from that link will also help you when you are booting your computer up in the next step. 
10.  Now that your USB drive has a copy of Ubuntu on it and your BIOS settings boot order is taken care of you want to shut down your computer and restart. Make sure the drive is plugged into youru computer this whole time.  When you go to restart, as soon as the screen clicks on and is still black hit the ESC key. It brings up the start screen and you want to select boot order. You should see your USB drive when you do this. Select your USB drive and you will be prompted to go through the Ubuntu install  process.
11. You will continue through the directions from the link above and go through the install screens for Ubuntu. I checked both the first boxes about being connected to the internet, and installing other programs for Ubuntu while it is installing.
12. For installation type you will select "something else"
13. Make sure you remember the amount of the free space you created from deleting volume on your hard disk. On the next screen you will see different drives. One may have the name free space, or it may be named something completely differently, that's why it's importnat you know how much space you had saved for Ubuntu. 
14. Click on the free space and click the plus sign below.
15. First step is to create the root directory on Ubuntu. This should be between 10-20GB. I did 20GB for mine.Then select Type of Partition: primary, Location: beginning of this space, Use as: Ext4 journaling file system, Mount point: / and select ok.
16. Then create a swap area. This acts as space for your RAM if your ram is full. You want to do double your RAM amount. Mine was 6G so I did 12G. Input your size amount in MB, select primary for the partition, beginning of this space, and Use as: "swap area". Hit ok.
17. The remaining free space you would want to use for your /home. Select the size, primary, beginning of this space, Use as: "Ext4 journaling file system", Mount point: /home. Hit ok.
18. You are so close you can almost taste it. Hit "install now".
19. The installation setup will direct you to create a user login and password.  Once you have gone through their setup screens you will want to start the setup of your local environment.

This leads us into the setup found in the Learn-Co curriculum for Linux setup.  See the link [here](https://github.com/learn-co-curriculum/linux-env-setup).  

Do a CTRL + ALT + T to open your terminal and start pushing out the code from the learn.co directions. 

And now you have set up your local environment!!


# The good the bad and the ugly

A lot can go wrong when you are trying to set up the usb drive, ubuntu and your local environment. I'm going to list out all the things that went wrong and the good stuff that came out of it!

1. When I first purchase my USB drive I just purchased the cheapest one I saw.  It didn't have a name on it whether it was a flash 2 or flash 3. For all I knew every USB was created equal. Wrong. I spent 4 days trying to download and install Ubuntu on the drive. It took way longer than the timeframe I was googling and then when I would go to install Ubuntu I would get errors and it would uninstall and I'd have to reboot. **So just make sure you have a FLASH 3 USB DRIVE**
2. I first installed Ubuntu 17.1 which had all the bugs.  Naturally, I thought if you deleted a file that you would fix your problem and then I could install the 16.04 version. So what did I do? I went to my hard drive space and deleted the partitions I made that had Ubuntu installed on it. VERY VERY BAD! DO NOT DO THIS! BUTTTTT IF YOU DO... I can hook you up with potentially how to fix your problems that are about to come on like a bad storm!
3. When you just delete the space that has Ubuntu, you don't delete EVERYTHING from Ubuntu, the grub remains.  It pretty much is going to ruin your world as soon as you turn your computer on the next time. You will see the black boot screen of death AKA the grub screen. You do not want to be booting your computer up from the backend every time right? So how do you fix this???? It's a good thing I stayed up until 4:30 (am) on a Saturday night/Sunday morning trying to figure this one out! Here are some sources I used for these steps:

**You need to get to the windows admin terminal for these steps:**
* [This may work for you but did not work for me](https://askubuntu.com/questions/610535/i-deleted-ubuntu-and-now-grub-doesnt-boot-into-windows-anymore?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)
* [Skip to mid page the response with 23 votes this worked for me!](https://askubuntu.com/questions/429610/uninstall-grub-and-use-windows-bootloader?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)
* I had many other sources, YouTube videos I watched before I got to the two sources above. If you google "I deleted Ubuntu harddrive space before uninstalling" or "grub screen at windows start up" you can see TONS of sources. Apparently, I'm not the only newbie that has made that mistake. 

4.  When you are doing all the installing command line items from the learn.co directions you may run into some problems because it was written for a previous Ubuntu version. One thing I had issues with was that I wanted to use the latest Ruby and RVM download. When I did this though and went to use my environment on Flatiron labs, the versions were not the same.  I uninstalled the latest version and added installed a new RVM and Ruby that was the version that Flatiron had in the curriculum. 
5.  Since I knew the directions were outdated I also googled the items listed on the learn.co instructions and found the github.repos of some of them to install instead. I have copied the links to all of them below:
[Node Source](https://github.com/nodesource/distributions)
[Directions to install RVM](https://rvm.io/rvm/install)
[How to verify that your RVM installed correctly](https://stackoverflow.com/questions/17257534/how-to-verify-if-rvm-was-installed-successfully?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)
[How to install Ruby on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-with-rvm-on-ubuntu-16-04)
[Upgrading RVM](https://rvm.io/rvm/upgrading)
[Check at this link for the most recent Ruby stable releases.](https://www.ruby-lang.org/en/downloads/) Ideally you don't want to be using one that is in beta testing or has bugs.
[The directions after rvm install are helpful if you have any rvm or ruby issues with the version you have installed on your system](https://rvm.io/rvm/basics)

Although this was a week long process for me, literally all day and night, trying to work through the issues with my USB not working, and then issues with the grub screen, I learned A LOT. I learned more about computers in one week than I have ever. At times I was scared to enter commands because I was playing around with screens that potentially could be huge catastrophes on my computer.  But when I finally set everything up and Ubuntu loaded, I felt a sense of accomplishment that I can't even put into words. Although it took an entire week of my time and took away from me working on curriculum, it was a huge learning exprience.

If you are thinking of doing a dual boot instead of a virtual box, shoot me a message on Slack. I'm happy to help!











