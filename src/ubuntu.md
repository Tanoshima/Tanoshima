# Ubuntu

## install & download

- Install Ubuntu desktop
  - https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview
- Download Ubuntu Desktop 
  - https://ubuntu.com/download/desktop

## 2022.03.21 Night Light not working

- 「夜間モード」が機能していない

1. 試したこと1

- gnome-control-center を再インストール & 再起動
```
sudo apt-get install --reinstall gnome-control-center
```


## VertualBoxからホストのUSBデバイスにアクセス
vboxusersにユーザーを追加が必要

```
$ sudo gpasswd -a {USERNAME} vboxusers
```

参考
https://qiita.com/yvl/items/de09cd110651f6c25cb3
https://studio3104.hatenablog.com/entry/20121126/1353893999
