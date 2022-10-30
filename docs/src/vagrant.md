# Ubuntu

## install & download

- Install Ubuntu desktop
  - https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview

## vagrant up でエラー その1
2022.04.10

- ```$ vagrant up```を実行すると以下のエラー

```
There are errors in the configuration of this machine. Please fix
the following errors and try again:

Vagrant:
* Unknown configuration section 'disksize'.
* Unknown configuration section 'env'.
* Unknown configuration section 'mutagen'.
```

- プラグインを追加する
```
vagrant plugin install vagrant-disksize
vagrant plugin install vagrant-env
vagrant plugin install vagrant-mutagen
```

## vagrant up でエラー その2
2022.04.10

- ```$ vagrant up```を実行すると以下のエラー

```
A customization command failed:

["modifyvm", :id, "--cpus", 0]

The following error was experienced:

#<Vagrant::Errors::VBoxManageError: There was an error while executing `VBoxManage`, a CLI used by Vagrant
for controlling VirtualBox. The command and stderr is shown below.

Command: ["modifyvm", "abe0dc3f-7ea0-4fb5-90fe-3e41f529ee41", "--cpus", "0"]

Stderr: VBoxManage: error: Invalid virtual CPU count: 0 (must be in range [1, 32])
VBoxManage: error: Details: code NS_ERROR_INVALID_ARG (0x80070057), component SessionMachine, interface IMachine, callee nsISupports
VBoxManage: error: Context: "COMSETTER(CPUCount)(ValueUnion.u32)" at line 856 of file VBoxManageModifyVM.cpp
>

Please fix this customization and try again.
```