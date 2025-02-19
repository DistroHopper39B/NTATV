# NTATV
The NTATV Project: Bringing Windows NT (Windows XP, Windows 2003, ReactOS) to the original Apple TV. Created by [DistroHopper39B](https://youtube.com/@DistrosProjects) with help from several ReactOS devs.

![NTATV Logo](NTATV_Logo_256.png)
## Status
Windows XP and 2003 are officially bootable on the original Apple TV! After 2 years of work, enough drivers are working to get both OSes to the desktop. However, due to HAL issues, ReactOS is not usable yet. You can get to the desktop, but there is 
| Operating System | Kernel | PCI | USB | Basic Video | Accelerated Video | Ethernet | WiFi | Audio | Remote |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Windows XP | Working | Working | Working | Working | Broken | Working | Working | Partially Working** | Broken |
| Windows Server 2003 | Working | Working | Working | Working | Broken | Working | Untested | Untested | Untested |
| ReactOS | Working | Broken | Broken* | Working | Broken* | Broken* | Broken* | Broken* | Broken* |

*\* Non-working PCI prevents all of these from working.*

*\*\* Audio plays, but at an extremely low volume.*


## Background
Ever since I saw The 8-Bit Guy's video ["Hacking the Apple TV 1st Generation"](https://youtu.be/Q9Acyy9lGSM) back in 2018 or 2019, I have been fascinated with the original Apple TV. I always wondered if it was possible for it to run Windows XP, but my efforts to actually get it working were kickstarted by [this Michael MJD video](https://youtu.be/3rBFkwtaQbU). Pretty quickly afterwards, I got started on hacking my Apple TV, and after over 700 days of on-and-off work, Windows XP finally runs!
### Why this was so complicated
While the Apple TV uses a standard x86 CPU and even an IDE hard drive, its firmware is not compatible with standard Windows XP. Windows XP requires legacy BIOS firmware, while the Apple TV is EFI-only. Not only that, the Apple TV's EFI implementation is *weird* - it can only boot one EFI executable, that being the Apple-official boot.efi. However, hackers very quickly realized that the Apple TV does zero verification on the next stage up in the boot process, that being the Mac OS X kernel file. Within three weeks of the Apple TV shipping, Linux was booted through a custom loader that embeds a Linux kernel into a statically linked Mach-O executable, the same type used by the Linux kernel. Using this concept, we can boot, well, anything on the hardware!

However, Windows is much harder to get running on non-standard hardware than Linux. For one, it's proprietary - when the first Linux support for the Apple TV was developed in 2007, installing Linux used to require numerous kernel patches due to Linux's at-the-time minimal EFI support. Booting Windows is also much more complicated than booting Windows; while Linux boot loaders can comprise of just a few files totalling less than 5000 lines of code, booting Windows XP involves parsing the registry and loading dozens of drivers individually. Thankfully, I don't have to do that. By creating an Apple TV version of ReactOS' extremely portable bootloader, [FreeLoader](https://reactos.org/wiki/FreeLoader), I was able to get the kernels of ReactOS and Windows to start successfully.

Moving any further than that involved getting video drivers to work. Thanks to some alpha-stage UEFI video drivers for ReactOS, I was able to get to the desktop on that OS; Windows took quite a bit more effort, but I detail that in my [write-up](Docs/Write-Up.md). 

A guide on how to create your own Windows XP install for the Apple TV is coming soon, but for now, just [download my install from Archive.org](https://archive.org/details/apple-tv-windows-xp-full.img)
## Credits
* [Justin Miller (The_DarkFire_)](https://github.com/DarkFire01) and [Hermès Bélusca-Maïto](https://github.com/hbelusca) for ReactOS UEFI video and boot loader support (and being immensely helpful with this project)
* Edgar (gimli) Hucek, James McKenzie of MythicBeasts, [Scott Davilla](https://github.com/davilla), and [Dmitri (loop333)](https://github.com/loop333) for work on Apple TV Linux.

If I used code or ideas from you and you want credit please open an issue.