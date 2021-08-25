Notes:

- Instructions: [mac.getutm.app/gallery/ubuntu](https://mac.getutm.app/gallery/ubuntu-20-04), [medium.com](https://medium.com/@lizrice/linux-vms-on-an-m1-based-mac-with-vscode-and-utm-d73e7cb06133), [eshop.macsales.com](https://eshop.macsales.com/blog/72081-utm-virtual-machine-on-m1-mac/)
- Drag UTM symbol into "Applications" folder to install the program
- Update/upgrade the guest (`sudo apt update && sudo apt upgrade`) before executing tasksel command (`tasksel install ubuntu-desktop`), otherwise it may not work
- [tasksel description](https://wiki.debian.org/tasksel)
- If you are like me and don't like the GNOME desktop (`ubuntu-desktop`), consider an alternative like Xfce or Cinnamon instead ([computingforgeeks.com](https://computingforgeeks.com/how-to-install-cinnamon-desktop-environment-on-debian/))
- Resolution: in case of problems, try 1440x900 ([arstechnica.com](https://arstechnica.com/civis/viewtopic.php?f=19&t=1473419))

UTM is a wrapper for QUEMU, an open-source emulator and virtualizer. If you want to use bare QUEMU instead, see:

- Hacking QUEMU: [gist.github.com](https://gist.github.com/akihikodaki/87df4149e7ca87f18dc56807ec5a1bc5)
