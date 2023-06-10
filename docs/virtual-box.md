# Virtual Box

Install Virtual Box on your system.

```bash
brew install virtualbox
```

## Setting up a virtual machine using `VBoxManage` CLI

```bash
VBoxManage createvm --name "YOUR_VM_NAME" --ostype Ubuntu_64 --register
VBoxManage modifyvm "YOUR_VM_NAME" --memory 2048
VBoxManage modifyvm "YOUR_VM_NAME" --cpus 1
VBoxManage createhd --filename "YOUR_VM_NAME.vdi" --size 34816
VBoxManage storagectl "YOUR_VM_NAME" --name "SATA Controller" --add sata --controller IntelAhci
VBoxManage storageattach "YOUR_VM_NAME" --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium "YOUR_VM_NAME.vdi"
VBoxManage storagectl "YOUR_VM_NAME" --name "IDE Controller" --add ide
VBoxManage storageattach "YOUR_VM_NAME" --storagectl "IDE Controller" --port 0 --device 0 --type dvddrive --medium ubuntu-20.04.3-live-server-amd64.iso
VBoxManage modifyvm "YOUR_VM_NAME" --nic1 nat
VBoxManage modifyvm "YOUR_VM_NAME" --natpf1 "ssh,tcp,,2334,,22"
```

### Starting and stopping a virtual machine

```bash
VBoxHeadless --startvm "YOUR_VM_NAME"         # Headless version
VBoxManage startvm "YOUR_VM_NAME"
VBoxManage controlvm "YOUR_VM_NAME" poweroff
```

### Removing an existing virtual machine

```bash
VBoxManage unregistervm "YOUR_VM_NAME" --delete
```

### Resizing an existing virtual machine

```bash
VBoxManage modifyhd "YOUR_VM_NAME.vdi" --resize <new_size_in_MB>
```

#### Update default partioning

> See https://askubuntu.com/a/1117523

```bash
sudo lvm
lvm> lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
lvm> exit

sudo resize2fs /dev/ubuntu-vg/ubuntu-lv
```

Also may be helpful:

1. First, you need to expand the virtual disk in VirtualBox. You can do this by selecting the virtual machine in the VirtualBox Manager, going to the "Storage" tab, and selecting the virtual disk. Then, click on the "Properties" button, go to the "Capacity" tab, and increase the size of the disk.

2. Once you have increased the size of the disk, you need to boot the virtual machine and use a partitioning tool to expand the partition. One way to do this is to use the `fdisk` command:

   a. Start by running `sudo fdisk /dev/sda`.

   b. Type `p` to print the partition table and make note of the starting sector of the `sda3` partition.

   c. Type `d` to delete the `sda3` partition.

   d. Type `n` to create a new partition. Select the default partition number and starting sector (the same as before).

   e. When prompted for the size, press Enter to use the default value, which is the maximum available.

   f. Type `t` to change the partition type. Select `8e` to set the partition type to Linux LVM.

   g. Type `p` to verify that the partition table looks correct.

   h. Type `w` to write the changes to disk and exit.

3. After you have expanded the partition, you need to expand the LVM volume and file system:

   a. Run `sudo pvresize /dev/sda3` to resize the physical volume.

   b. Run `sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv` to extend the logical volume.

   c. Run `sudo resize2fs /dev/ubuntu-vg/ubuntu-lv` to resize the file system.

4. Finally, you can verify that the file system has been expanded by running `df -h`.