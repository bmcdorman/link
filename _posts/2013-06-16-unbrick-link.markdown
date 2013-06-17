---
layout: post
title:  "Manually Un-bricking a Link"
---

***These steps will void your warranty.***

If the Link fails to boot to standard mode or recovery mode, these steps can be used to manually flash the internal micro-SD card. The following steps require a Torx screwdriver, a micro-SD card reader (or SD card reader and adapter), and an Operating System supporting `dd` (nix or Mac OS X).

 - Remove the warranty sticker from the Link's case.
 - Remove the four bottom screws using a Torx screwdriver.
 - Locate the micro-SD card hinge (by the power switch).
 - Push the hinge towards the inside of the case and lift up.
 - Place the recovered micro-SD card in card reader.
 - The OS will probably auto-mount the contents of the drive and
	possibly display some error messages. Ignore these error messages and
	unmount the SD card if auto-mounted.
 - Determine the appropriate device file to write to in \texttt{/dev}.
	This can easily be determined by removing the card,
	running `ls /dev > 1`, inserting the card again, 
	and running `ls /dev > 2 && diff 1 2`. The correct
	device file will not have any numerical suffix.
 - Download the KIPR Link firmware file to install.
 - Extract the KIPR Link firmware file using `gunzip`.

***Triple check that the determined device file is indeed the micro-SD card.
Choosing the wrong device file could overwrite your hard drive disk!***

Finally, 
	`sudo dd if=image.img of=/dev/determined_device_file bs=1M`
(the M might be lowercase on your platform).