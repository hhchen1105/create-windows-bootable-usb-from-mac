# Create a bootable USB disk for Windows installation from MAC

1. Ensure your Mac has ``wimlib``.  If not, install it by

   ```brew install wimlib```

1. Insert USB disk.  Ensure the disk ID by

   ```diskutil list```

   The ID of the USB disk is probably be something like ``/dev/disk2``

1. Format the USB disk by

   ```diskutil eraseDisk MS-DOS "WIN10" GPT /dev/disk2```

1. Download the windows ISO file (e.g., ``~/Downloads/win10-Eng-x86.iso``)
1. Mount the windows ISO
   
   ```hdiutil mount ~/Downloads/win10-Eng-x86.iso```
   
1. Because the file ``install.wim`` is too large to copy over to a FAT-32 formatted USB drive, we need to copy it over separately.

   ```rsync -vha --exclude=sources/install.wim /Volumes/WIN10_EN-US_DV9/* /Volumes/WIN10```

1. Split ``install.wim`` into 2 files and copy them to USB.

   ```wimlib-imagex split /Volumes/WIN10_EN-US_DV9/sources/install.wim /Volumes/WIN10/sources/install.swm 3800```

VIOLA!
