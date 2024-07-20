# Wireless Wiitar w/ Tilt function on Linux.

I have only tested this on batocera, but if it can be done inside this closed environment, it should be easy to accomplish on any other linux platform!

This project is designed for the small percentage of people who have been stressing themselves out trying to get wireless wiimotes + wiitar to work with tilt on multiple controllers with Clone Hero!

First of all, big shout out to the people that actually helped in making this possible through hours of google searching:

https://cohost.org/ticky/post/3622903-well-i-finally-sat   <---Took the time to map out the template for the separate wiimote inputs so they can be mapped to the virtual input using evsieve!

https://retropie.org.uk/forum/topic/21251/static-dev-input-entry-for-bluetooth-controllers   <---amazing little piece of code that does all the work of assigning wii inputs into static addressable inputs!

https://github.com/Oblomov/wiimote-pad/blob/master/70-wiimote.rules   <---This was the final piece of the puzzle that helped me really understand what can be done with UDEV rules!

The folder above has the following contents:

1) The UDEV rule that can be copied to /etc/udev/rules.d folder (You will have to change your paths from what I have in order to make this work). Be sure to type "udevadm control --reload-rules && udevadm trigger" in order to reload the rules and trigger them. **Also if running batocera, you'll want to make sure you type "batocera-save-overlay" if you want this rule to be persistent after a reboot (since batocera clears out any changes to certain file systems after a reboot otherwise)!

2) The wiitar-namer file that will be called from the UDEV rule that was added, in order to create symlinks of the different wiimote inputs linux likes to split up and assign to a random /input/event*. I also added a wiitar-cleanup file that should remove any leftover wiimote* symlinks after the controllers have been disconnected (This will also have to be edited if you choose a different naming scheme for your /dev/input names.

3) The wiitar1-4 executables that use evsieve to assign the appropriately named wiimote devices to a virtual device called wiitar w/ tilt (1-4). This allows for the tilt function to be programmed to the select key for use in clone hero, and activated by tilting past a certain threshold.

For the record, I am not a programmer by any means, and a lot of this was trial and error (as well as chatgpt helping immensely). I hope that it helps someone else along the way, and please feel free to give feedback or tips for how this could be better! 

****important note: I recently found that when connecting a third wiitar was causing batocera to reload emulationstation over and over. This was due to having too many usb devices plugged into my mini pc. If this happens to you, just try unplugging any unnecessary devices from your usb ports to see if that fixes the issue!
