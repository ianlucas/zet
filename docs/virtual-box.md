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
```

## Removing an existing virtual machine

```bash
VBoxManage unregistervm "YOUR_VM_NAME" --delete
```