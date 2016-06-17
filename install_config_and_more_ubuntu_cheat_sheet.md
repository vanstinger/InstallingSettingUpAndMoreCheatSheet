Brightness control fix
	sudo touch /usr/share/X11/xorg.conf.d/20-intel.conf
	sudo gedit /usr/share/X11/xorg.conf.d/20-intel.conf

Section	"Device"
	Identifier "card0"
	Driver	   "intel"
	Option
"Backlight" "intel_backlight"
	BusID	"PCI:0:2:0"
EndSection


Disable Bluetooth by Default on Startup
	sudo gedit /etc/rc.local

just before 'exit 0' add
	rfkill block bluetooth

Installing Oracle Java
	-Ubuntu
		using webupd8team ppa
			sudo apt-add-repository ppa:webupd8team/java
			sudo apt-get install oracle-java6-installer
			sudo apt-get install oracle-java7-installer
			sudo apt-get install oracle-java8-installer
Smart way to setup Java alternatives // Got it from .deb package oracle-java7-set-default
	sudo update-java-alternatives -s java-7-oracle > /dev/null 2>&1

	-Fedora
		install Oracle Java by downloading rpm from official website
			sudo dnf install jdk-8u92-linux-x64.rpm

			su -
			alternatives --install /usr/bin/java java /usr/java/default/jre/bin/java 200000
			alternatives --install /usr/bin/javaws javaws /usr/java/default/jre/bin/javaws 200000
			alternatives --install /usr/lib64/mozilla/plugins/libjavaplugin.so libjavaplugin.so.x86_64 /usr/java/default/jre/lib/amd64/libnpjp2.so 200000
			alternatives --install /usr/bin/javac javac /usr/java/default/bin/javac 200000
			alternatives --install /usr/bin/jar jar /usr/java/default/bin/jar 200000
			alternatives --install /usr/bin/java java /usr/java/jdk1.8.0_92/jre/bin/java 200000

			su -
			alternatives --config java
			alternatives --config javaws
			alternatives --config libjavaplugin.so.x86_64
			alternatives --config javac
			alternatives --config jar

Referrence:-(http://www.if-not-true-then-false.com/2014/install-oracle-java-8-on-fedora-centos-rhel/)

Installing kvm for Android Studio (source:http://tinyurl.com/os95xme)

(documentation page:https://help.ubuntu.com/community/KVM/Installation)
	sudo apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils
	sudo adduser your_user_name kvm
	sudo adduser your_user_name libvirtd

Under Fedora
	sudo useradd maez -D -G dialout,kvm,libvirtd
	or try,
	sudo usermod meaz -a -G dialout,kvm,libvirtd

Solving Android device unauthorised in adb devices list

	gedit android.rules

SUBSYSTEM=="usb" ATTR{idVendor}=="0bb4", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0e79", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0502", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0b05", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="413c", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0489", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="091e", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="18d1", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="12d1", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="24e3", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="2116", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0482", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="17ef", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="1004", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="22b8", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0409", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="2080", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0955", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="2257", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="10a9", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="1d4d", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0471", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="04da", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="05c6", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="1f53", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="04e8", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="04dd", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0fce", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="0930", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="19d2", MODE="0666"
SUBSYSTEM=="usb" ATTR{idVendor}=="1782", MODE="0666"

	sudo cp android.rules /etc/udev/rules.d/51-android.rules
	sudo chmod og+r /etc/udev/rules.d/51-android.rules

Uninstall Libreoffice and install Openoffice
	aptitude search '~i' | grep libreoffice
	sudo apt-get install -s remove libreoffice-core
	sudo apt-get install remove libreoffice-core
Download OpenOffice from it's official website, *.tar.gz, extract and
	sudo dpkg -i *.deb

Alternative to libreoffice and openoffice is WPS Kingsoft Office suite


Install redshift
	sudo apt-get install redshift*
	sudo gedit /usr/share/applications/redshift-gtk.desktop
add  '-l 18.98:72.83' next to 'Exec=redshift-gtk'
start redshift and select autostart in its options menu
Open Startup Applications app select RedShift and press edit button
and add '-l 18.98:72.83' next to 'redshift-gtk' Command field

To fix unmet dependencies of the packages installed on the system
	sudo apt-get install -f
To remove packages not needed anymore
	sudo apt-get install autoremove
clean using
	sudo apt-get install clean
	sudo apt-get install autoclean

Check for broken packages fix and clean
	sudo apt-get install --fix-broken 
	sudo apt-get install --fix-missing 

Enable Hibernate
	sudo nano /etc/polkit-1/localauthority/50-local.d/com.ubuntu.enable-hibernate.pkla

[Re-enable hibernate by default in upower]
Identity=unix-user:*
Action=org.freedesktop.upower.hibernate
ResultActive=yes

[Re-enable hibernate by default in logind]
Identity=unix-user:*
Action=org.freedesktop.login1.hibernate
ResultActive=yes

killall unity-panel-service

Installing Sublime-text-3
	-Ubuntu/Debian
		sudo add-apt-repository ppa:webupd8team/sublime-text-3
		sudo apt-get update
		sudo apt-get install sublime-text-installer

	-Fedora/(other linux distros)
		$  curl -L git.io/sublimetext | sh

Install subversion and git
	sudo apt-get install subversion
	sudo apt-get install git

Setup git global properties using
	git config --global user.email "name@example.com"
	git config --global user.name "Your Name"

In Terminal, enter the following:

	git config --global credential.helper cache
	# Set git to use the credential memory cache
To change the defau
lt password cache timeout, enter the following:

	git config --global credential.helper 'cache --timeout=3600'
	# Set the cache to timeout after 1 hour (setting is in seconds)

Doing Git Stuff
	echo "# exploring_java_src" >> README.md
	git init
	git add README.md
	git commit -m "first commit"
	git remote add origin https://github.com/Sairaj4522/exploring_java_src.git
	git checkout -b "master"
	git push -u origin master

Enable color output from git log or whatever
	git config --global color.ui auto
and some additional global configs
	git config --global core.editor "subl -n -w"
	git config --global push.default upstream
	git config --global merg.conflictstyle diff3

Configuring Git prompt
add following to the end of ~/.bashrc for this you need git-prompt.sh and git-completion.bash



# Enable tab completion
#source ~/git-completion.bash
source /etc/bash_completion.d/git-prompt

# colors!
green="\[\033[0;32m\]"
blue="\[\033[0;34m\]"
purple="\[\033[0;35m\]"
reset="\[\033[0m\]"

# Change command prompt
source ~/git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1
# '\u' adds the name of the current user to the prompt
# '\$(__git_ps1)' adds git-related stuff
# '\W' adds the name of the current directory
export PS1="$purple\u$green\$(__git_ps1)$blue \W $ $reset"

#Adding some of the commands here.
	git diff commit1 commit2
	#Compare file changes between commit1 and commit2
	
	git diff 
	#Compare file changes between working directory and staging area
	
	git diff --staged
	#Compare file change between staging area and latest commit in the repository
	
	git log
	#Log all the reachable commits in the current checked out branch
	
	git log --graph --oneline master coins
	#Show all logs in form of graph to see the branching in current repo,
	#its useful to see when a some other branch in this case coins was created to
	#see which code base from master(or to find the tip of the master at that branch
	#creation) it is derived from, here --oneline tag specifies to git log to print 
	#in more concise/compact format
	
	git log -n 1
	#Log only one latest commit, here -n 1 specifies git log to show only one output
	
	git status
	#Check status of your local repo, whether a file is yet to be staged, commited or
	#pushed(in case of remote repo)
	
	git checkout some-branch
	#Switch between various branches in your repo, also can put commit git hash in place
	#of 'some-branch' name to checkout that particular commit
	
	git merge master some-other-branch
	#Combine two branches together if there a conflict solve them and then use git commit
	#to do final steps of this command
	
	git branch
	#View all branches in current repo
	
	git branch coins
	#Create a branch named 'coins'
	
	git branch -d coins 
	#Delete a branch named 'coins'
	
	git pull
	#Get all the repo info/files from some other repo, also acts as update as in subversion,
	#which updates the local repo by pulling data/info from remote
	
					git fetch origin
						|
	git pull origin master = {		|
						V
					git merge master origin/master
	git fetch
	#This updates your local origin/master, while keeping the master intact(this is only in
	#case of a conflict in commits between local and remote repo)
	#
	#Think of this command as if it's made for GitHub, if there's a situation when you make
	#a commit to your local repo but u did not push it to remote, and in remote repo(i.e at GitHub)
	#someone or you have changed some file which will result in a new commit on remote repo. Now you
	#want to push changes from local repo but git wont let that happen due to unmatching commit on
	#both local and remote side. this is where git fetch comes in u fetch, merge, resolve the conflicts
	#if any, and finally merge them as single commit in master and origin/master branch, and finally 
	#push to be in sync
	

#TO DO
#Download How to Use Git and GitHub Udacity Videos and add
#all git commands here.

Installing Linux, Apache, MySQL, PHP (LAMP) stack on Ubuntu 14.04


Setting up ClamAV and Running Virus scans:
	sudo apt-get install clamav clamav-daemon -y
update the clamav pattern file:
	sudo freshclam
Check files in the all users home deirectories:
	sudo clamscan -r /home
Scan and remove virus files:
	sudo clamscan --infected --remove --recursive /home
Start clamav-daemon(clamd):
	sudo /etc/init.d/clamav-daemon start
Check clamd status :
	sudo /etc/init.d/clamav-daemon status

Changing brightness at Startup to lower value as compare to max_brightness
Add this line to '/etc/rc.local' before 'exit 0'
	echo 900 > /sys/class/backlight/intel_backlight/brightness

Adding AVR support in eclipse on Ubuntu
	sudo apt-get install avr-libc avrdude binutils-avr
Open eclipse
go to Help-->Install New Software...
and add http://avr-eclipse.sourceforge.net/updatesite/
in Text input and press Add Site button

Adding support for the varous USB AVR devices
Create a file avrisp.rules

	gedit ~/avrisp.rules

SUBSYTEM!="usb_device", ACTION!="add", GOTO="avrisp_end"
# Atmel Corp. JTAG ICE mkII
ATTR{idVendor}=="03eb", SYSFS{idProduct}=="2103", MODE="660", GROUP="dialout"
# Atmel Corp. AVRISP mkII
ATTR{idVendor}=="03eb", SYSFS{idProduct}=="2104", MODE="660", GROUP="dialout"
# Atmel Corp. Dragon
ATTR{idVendor}=="03eb", SYSFS{idProduct}=="2107", MODE="660", GROUP="dialout" LABEL="avrisp_end"

	sudo cp ~/avrisp.rules /etc/udev/60-avrisp.rules
In order to access these devices the user must also belong to dialout group
	sudo adduser your-user-name dialout
At last uploading hex file
	sudo avrdude -p m128 -c avrispmkII -P usb -U test.hex
	sudo avrdude -p m32 -c usbasp -P usb -U ~/test.hex
Go to http://www.fischl.de/avrusbboot/ and download the avrusbboot.2006-06-25.tar.gz and extract
	tar -xvfz avrusbboot.2006-06-25.tar.gz 
for custom avr usb bootloader  and folow instructions on the same website to make
the bootloader and the program to upload the hex file on the micro-controller
another dependency for compiling above programs
	sudo apt-get install libusb
	cd avrusbboot.2006-06-25
	cd firmware
	make
	sudo avrdude -p m8 -c usbasp -P usb -U lock:w:0x3F:m
	sudo avrdude -p m8 -c usbasp -P usb -U hfuse:w:0xD8:m -U lfuse:w:0xDF:m -U flash:w:main.hex
	cd ../software
	make
	sudo ./avrusbboot ~/test.hex

Setting up Genymotion
	-Ubuntu
		sudo apt-get install virtualbox
	-Fedora23
		Add yum repository for virtualbox
			cd /etc/yum.repos.d/
			wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo
			dnf update

		check that the system is running latest installed kernel version
		Output of foll. commands version numbers should match:
			rpm -qa kernel |sort -V |tail -n 1
			uname -r

		Install dependencies
			dnf install binutils gcc make patch libgomp glibc-headers glibc-devel kernel-headers kernel-devel dkms

		Install VirtualBox latest version 5.0
			dnf install VirtualBox-5.0
		Add VirtualBox User to vboxusers Group
			usermod -a -G vboxusers user_name
		Start VirtualBox and proceed to installing Genymotion
			VirtualBox
Refference:
http://www.if-not-true-then-false.com/2010/install-virtualbox-with-yum-on-fedora-centos-red-hat-rhel/

Download Genymotion
	chmod +x genymotion-x.x.x_x64.bin
	./genymotion-x.x.x_x64.bin

Cool Java stuff
	//Diagonosing java code to find out if a method is not good to run as a inline method
	java -XX:+UnlockDiagnosticVMOptions -XX:+PrintInlining jcookb.SubStringDemo
	//Running JUnit Tests
	java -cp $CLASSPATH org.junit.runner.JUnitCore testing.SuiteTest

Use strings command line to scan for strings in the binary file
	strings some_binary_file

flaunt with the monkey
	adb shell monkey -p com.example.android.app -v 10000

Add alias to a common action
add this to your ~/.bashrc
	alias name='value'
where name is the short form of the action(value) that you choose for example
	alias ogc='google-chrome'

Customize theme specifics in Ubuntu, such as highlight color, menu background color,etc.
	sudo apt-get install dconf-editor 
	sudo apt-get install gtk-theme-config 
Press Alt+F2 and open Theme configuration and change color for the Highlight background and click on toggle button to enable it

Create Bootable Ubuntu USB 
	Either use Ubuntu default Startup Disk Creator or right click on the ISO file
	and open with Disk Image Writer select the USB drive, start the restore 
	procedure and after when its done you have your bootable USB drive.
Refference:
(http://askubuntu.com/questions/485357/unknown-error-from-startup-disk-creator)

Create Windows Bootable USB on Ubuntu
1. Format USB
	Open GParted, first unmount the USB drive, recreate the partition table by going
	to the Device menu then select Create Partition Table. Choose 'msdos' and click
	Apply.

	Right click on the unallocated space and select New, Make a primary NTFS or FAT32
	partition and give it a label, this label will be required later.

	Apply all pending operations, now Right click the partition and add the 'boot' flag
	by selecting Manage Flags and tick the checkbox next to 'boot'

2. Copy Windows files
	Close GParted and use nautilus to copy all files from Windows ISO to USB stick.
	Mount ISO using Open with - Disk Image Mounter

3. Make it Bootable
	sudo apt-get install grub-pc-bin
	sudo grub-install --target=i386-pc --boot-directory="/media/<username>/<drive_label>/boot" /dev/sdX
		Replace /dev/sdX with the USB drive(eg. /dev/sdb)

	Create grub.cfg file

		default=1  
		timeout=15
		color_normal=light-cyan/dark-gray
		menu_color_normal=black/light-cyan
		menu_color_highlight=white/black
		 
		menuentry "Start Windows Installation" {
		    insmod ntfs
		    insmod search_label
		    search --no-floppy --set=root --label <USB_drive_label> --hint hd0,msdos1
		    ntldr /bootmgr
		}

		menuentry "Boot from the first hard drive" {
		    insmod ntfs
		    insmod chain
		    insmod part_msdos
		    insmod part_gpt
		    set root=(hd1)
		    chainloader +1
		    boot
		}

	Replace <USB_drive_label> with the label from step 1
	Save this file and put in boot/grub folder on USB drive.

Refference:
(http://onetransistor.blogspot.in/2014/09/make-bootable-windows-usb-from-ubuntu.html)


List of softwares for Ubuntu
vlc browser-plugin-vlc
chrome
gstreamer 1.0 and 0.10 full(good, bad and ugly) 


Unlocking Bootloader on Moto e
first get unlock data which will be fed to OEM to get secret code
	fastboot oem get_unlock_data

	fastboot oem unlock {secret-code-from-OEM}

#TODO Add extracting .img files and cwm flashable zip creation steps
in adb shell issue these commands to get mount information
	cat /proc/dumchar_info
	cat /proc/mtd

Flashing Devices with Fastboot mode
install Android SDK which provides almost all the tools to do this.
issue this command to check if the device is detected
	fastboot devices
now fetch your recovery.img, boot.img, etc.
	fastboot flash recovery recovery.img
	fastboot flash boot boot.img
	fastboot flash logo logo.bin


Flashing MTK based mobile devices

first install libusb-dev
	sudo apt-get install libusb-dev

Get latest SP Flash tool Linux version from http://spflashtool.com/
unzip the file and cd into the directory

In order to avoid running the flash_tool as root user, you need to add a standard user to the usergroup "dialout"
	sudo adduser username dialout
and activate the membership immediately
	newgrp - dialout

Open the tool
	./flash_tool

You can try at this stage if the flash tool connects to your phone:
In the user interface, choose tab „Download“. Hit "scatter-loading", navigate to a directory with a valid firmware
for your device and choose the scatter-file.

For testing purposes uncheck "name" and check one of the smaller files in the list below (for example "logo")

Switch off your device. Hit the "Download" button in SP_Flash_Tool and connect your phone to the computer.

Some devices require you to take off the battery for about 10 seconds, with others you need to press Vol+ or Vol-
while plugging the cable into the phone.

Please look up device-specific threads and try out different options.

If nothing happens at all, open a second terminal, run
	dmesg | grep usb
and look out for a MediaTek entry. If there is none -> did you install libusb-dev

If the answer is yes, then you might need to create a persistent udev rule for the MTK Preloader:
	sudo gedit /etc/udev/rules.d/80-persistent-usb.rules

and add the following line to the file:
	SUBSYSTEM=="usb", ACTION=="add", ATTR{idVendor}=="0e8d", ATTR{idProduct}=="*"

save the file and exit.

Reload the usb-rules:
	sudo service udev restart

Disconnect the usb cable, close the tool window.

Now try repeating the procedure to get your phone in fastboot mode, in case of MTK devices MTK preloader mode,
which means just connect phone to pc without battery, and later add the battery after you open the tool and
press Download button.

If the tool connects, within a few seconds a red progress bar will appear. In case an error message like:
S_BROM_CMD_JUMP_DA_FAIL (2035)
shows up, then there is a connection, but have to do some thing to solve it.

From Sergio Riveros tutorial on mibqyyo, he mentions:
	Quote:
		"This is because the 'modemmanager` package integrated by default within Linux Ubuntu 14.04 and later
		is not compatible with the MTK Flash Tool."

To put it in other words: The modem manager controls port /dev/ttyACM0 and disables the Flash Tool. So we
blacklist it for the two MTK vendor IDs the flash tool uses:
	sudo gedit /etc/udev/rules.d/20-mm-blacklist-mtk.rules
with the following contents:
	ATTRS{idVendor}=="0e8d", ENV{ID_MM_DEVICE_IGNORE}="1"
	ATTRS{idVendor}=="6000", ENV{ID_MM_DEVICE_IGNORE}="1"

Restart udev for the changes to take effect:
	sudo service udev restart

Switch your phone on (fastboot mode will suffice) and off again
	./flash_tool

Now everything should run smoothly. In case you encounter
	BROM ERROR : S_SECURITY_SF_CODE_FORMAT_FORBIDDEN (6012) , MSP ERROE CODE : 0x00
change the download agent to MTK_AllInOne_DA.bin 

If you run into more errors, you could get a hint about what is wrong from here:
Flashtools errors and their solutions! - MIUI(http://en.miui.com/thread-78047-1-1.html)

References:
	http://android.stackexchange.com/questions/119068/how-to-root-mtk-based-mobile-devices-using-a-linux-pc
	http://forum.xda-developers.com/general/rooting-roms/tutorial-how-to-setup-spflashtoollinux-t3160802
	http://en.miui.com/thread-78047-1-1.html

Configure hotkeys on Fedora
https://www.howtoforge.com/manage-your-laptop-hotkeys-on-fedora
Open Settings->Keyboard, switch to Shortcuts tab
Then configure Audio control and volume control keys by assigning new accelerator
Now select Custom Shortcuts in left pane, here you can add new shortcuts by clicking on + button ;
for adding hotkeys for brightness control install xbacklight
	sudo dnf install xbacklight
then press that + button and add name and command in the fields in the dialog window
for increasing brightness, xbacklight -inc 10%
and for decreasing it, xbacklight -dec 10%
these commands increases or decreases brightness by 10 percent

Add terminal shortcut using any name for the title and add command as
gnome-terminal

#TODO Add how to disable some of the system hotkeys which interfere with Android studio default keys


Mount drives on boot in Fedora 23
To do this we have to edit /etc/fstab file, so 
	sudo gedit /etc/fstab
and add following to the end of the file:
	/dev/sda4 /run/media/my_user_name/Data ntfs defaults 1 2

where: /dev/sda4 is the partition name
       /run/media/my_user_name/Data is the mount point
       ntfs is the partition type you have to choose options as defaults and latter part is the order to check

Fix Native Window Placement extention to display the title on top or bottom
	Tweak the stylesheet.css to modify the window title placement. open "/home/$USER/.local/share/gnome-shell/extensions/native-window-placement@gnome-shell-extensions.gcampax.github.com/stylesheet.css", change "-shell-caption-spacing" as you like. 0px (on top) or 26px (below) would do. Restart the extension with toggling on/off switch in this page or tweak tool.

###Add API keys to Android Studio for your apps the right way
First open gradle.properties file, then add API key in the form
MyApiKey="{Your API Key}"

then open app/build.gradle
and add following

	android {
	    buildTypes {
	        buildTypes.each {
	            it.buildConfigField 'String', 'MY_API_KEY', MyApiKey
	        }
	    }
	}

thats it now use your API keys in Java code by refering BuildConfig constants like,
String api_key = BuildConfig.MY_API_KEY;