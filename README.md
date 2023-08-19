# Multiboot Config

Create a Multi bootable USB flash drive

# Format USB dirve

https://wiki.networksecuritytoolkit.org/nstwiki/index.php?title=HowTo_Create_A_GPT_Disk_With_EFI_System_And_exFAT_Partitions_Using_Parted


# Install GRUB

https://wiki.archlinux.org/title/Multiboot_USB_drive#Installing_GRUB


# Install Autoiso

```
git clone https://github.com/jim945/autoiso-multiboot.git
cd autoiso-multiboot
sudo rsync --recursive --times --progress --verbose --delete --exclude=.git --exclude='*.md' . /mnt/boot/grub/autoiso
```

# Install Memtest86+

Download [memtest86](https://www.memtest86.com/download.htm)

```
cd ~/Downloads

mkdir memtest86
unzip -d memtest86 memtest86-usb.zip

cd memtest86
mkdir ./tmp
sudo mount -o loop,offset=$(( $(fdisk -lu memtest86-usb.img | awk '/EFI System/ {print $2}') * 512 )) ./memtest86-usb.img ~/Downloads/memtest86/tmp
rsync --times --progress --verbose ./tmp/EFI/BOOT/ /mnt/boot/memtest86+
```

# Copy grub.cfg

```
cp grub.cfg /mnt/boot/grub
```

# Test

## Virtualbox

```
sudo usermod -aG vboxusers $USER
```

Settings -> USB -> USB Device Filters -> Adds new USB filter

Start the machine


# References

https://wiki.networksecuritytoolkit.org/nstwiki/index.php?title=HowTo_Create_A_GPT_Disk_With_EFI_System_And_exFAT_Partitions_Using_Parted

https://wiki.archlinux.org/title/Multiboot_USB_drive

https://www.memtest86.com/tech_configuring-grub.html

https://lists.gnu.org/archive/html/help-grub/2016-01/msg00067.html

https://www.supergrubdisk.org/wiki/Loopback.cfg

https://www.gnu.org/software/grub/manual/grub/html_node/index.html#SEC_Contents

https://github.com/thias/glim

https://github.com/jim945/autoiso-multiboot
