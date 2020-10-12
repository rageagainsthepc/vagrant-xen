# Vagrant-Xen
This project is used to provision a virtual machine with an installed xen hypervisor to help with the development of virtual machine introspection programs.

## Hyperv Virtual Machine

__Note that for nested virtualization a generation 2 Hyper-V virtual machine is required. The common generic/* boxes however only are generation 1.__

See [the corresponding github issue](https://github.com/lavabit/robox/issues/100).

### Install Vagrant

Install Vagrant in both Windows and the WSL. Note that you need the __same version__ in both.

### Prepare the WSL
1. You need to tell the WSL to mount the Windows folder with metadata. For this edit the `/etc/wsl.conf` or create it if it does not exist. 
```bash
[automount]
enabled = true
root = /mnt/
options = "metadata"
mountFsTab = true
```
2. Enable Hyper-V provider and allow the WSL to use Windows Vagrant by appending the following to `~/.profile`
```bash
export VAGRANT_DEFAULT_PROVIDER="hyperv"
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
```
3. Kill the WSL from Powershell and then restart it as __administrator__.
```powershell
wsl.exe --list
wsl.exe --terminate <WSLNAME>
```

### Provision the VM
1. run `vagrant up` or if Hyper-V is not the default provider `vagrant up --provider="hyperv"`.
2. When prompted for the network switch use your newly created one.

### Troubleshoot

#### If vagrant does not detect the started VM
Add a new external network switch to Hyper-V manager. The default settings should be sufficient.