# Linux Settings
system settings and tricks for ubuntu 16.04

## nvidia driver for gtx 1070
1. install ubuntu 16.04 without GPU
2. sudo apt-get update 
3. download [367.27](http://www.nvidia.com/download/driverResults.aspx/104284/en-us)
4. shut down and plug in GPU
5. start and press "esc" to grub2 window
6. hightlight "Ubuntu" and press "e" to edit: add "nomodeset" after "ro" (with space) in the "linux" line, then press f10 to start
7. (screen flickering) right click mouse and open terminal: type "sudo chvt 1" and login
8. sudo service lightdm stop and 
9. install 367.27
10. sudo service lightdm start

## blank screen
1. sudo /usr/bin/
2. gnome-terminal
3. ccsm
4. "Enable Unity Desktop" - For any conflict, just diable the settings in "General"


## fish
set fish env var:

set -U fish_user_paths $fish_user_paths my_path

for example: set -U fisher_user_paths $fish_user_paths ~/anaconda2/bin/

## disable "system program problem detected" dialog
1. sudo rm /var/crash/*
2. vim /etc/default/apport
3. change "enable=1" to "enable=0"
4. sudo service apport stop
5. restart
