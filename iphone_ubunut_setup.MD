# How to access and mount iPhone 6 in Linux - Tutorial
- https://www.dedoimedo.com/computers/linux-iphone-6.html

### Errors with installing libimobiledevice

You can use it to mount iPhone with the ifuse tool. So after you install libimobiledevice6 as you did, you mount the iPhone with ifuse.

But first you need to install some packages including what you installed. To help others who see this question I'll explain how I do it from scratch:

sudo apt-get install ideviceinstaller python-imobiledevice libimobiledevice-utils libimobiledevice6 libplist3 python-plist ifuse
Then plug in the iPhone to a USB port and pair the iPhone:

idevicepair pair
Note: if you get an error "ERROR: Could not validate with device xxxxxxxxxx because a passcode is set. Please enter the passcode on the device and retry." unlock the iPhone and choose "Trust" in the security popup and repeat the command above.

Next you mount the iPhone with ifuse:

ifuse /media/iPhone/
You can run ifuse command above as root (sudo) or as a regular user, depending if you want to allow users to mount and unmount your iPhone.

To unmount the iPhone, which you should do to avoid problems mounting in future use the following commands one after the other:

fusermount -u /media/iPhone/
idevicepair unpair
More info here: http://www.dedoimedo.com/computers/linux-iphone-6.html
