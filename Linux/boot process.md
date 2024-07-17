### [[initramfs]]

### boot process:

1. The system powers up. The [[BIOS]] does minimal hardware initialization and hands over control to the [[boot loader]].
2. The boot loader calls the [[kernel]].
3. The kernel loads an initial RAM disk that loads the system drives and then looks for the root file system.
4. Once the kernel is set up, it begins the systemd initialization system.
5. systemd takes over and continues to mount the host's file system and start services.

