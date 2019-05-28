---
layout: post
title: Getting started with Linux Commands
date: '2016-05-09 05:32:00'
previewimg: '/content/images/2017/04/linux.jpg'
tags:
- linux
- cli
---

####How to Install a Package ?
```
sudo tasksel
```
Installs multiple related packages. It shows some popup, where we can select the number of packages. More Info : https://help.ubuntu.com/community/Tasksel 

####Installing Apache server :
Downloads and installs apache2.
```
sudo apt-get install apache2
```
Deletes apache2
``` 
sudo apt-get remove apache2
```
Updates the new versions of packages existing on the machine. 
```
sudo apt-get upgrade
```
Generally in Windows any changes in system configuration or software changes, it needs to restart the entire system or machine. While in Linux OS, we have simple commands to start and restart the services with out restarting the machine. 

Starts the service
```
sudo /etc/init.d/apache2 start
```
Stops the service
```
sudo /etc/init.d/apache2 stop
``` 
Restarts the service
```
sudo /etc/init.d/apache2 restart
``` 
####How to view log files:

Top is something similar to task manager in windows, which gives the table structure including CPU usage, memory usage, and CPU time, process Id etc. 
```
sudo top
```
Displays the table structure about CPU usage, memory usage, CPU time, process Id. 

**Other useful commands**

`K <PID>` - kills the process. <br>
`cd /` - Points to root directory. <br>
`q` - Exit the terminal. <br>

####Using vim Editor 
In Linux, we don’t use extensions for filenames as in Windows. 

`sudo vim <filename>` - Creates file, if file doesn’t exists. Opens file, if file exists.

`a` - Insert some changes in file or Insert mode is ON. <br>
`esc` - Escapes from edit mode. <br>
`:/*max*` - Searches for “max” word from top of the file. <br>
`:/? max`  - Searches for “max” word from bottom of the file. <br>
`n` - Goes to next line while searching. <br>
`:e` <filename> - Opens new file, if user is already in vim editor. <br>
`:q!` - Force quit. <br>
`:wq` - Saves the changes in file and exits vim. <br>
`:w` <newfilename> - Saves the changes as a new file with new name, doesn’t override same file. Similar to **Save As** operation in windows. <br>


`sudo chown <new user> <file name>` - Changes ownership of file to new user (eg: root)). <br>
`sudo adduser <username>` - Adds user with the specified username. <br>
`sudo userdel <username>` - Deletes specified user account. <br>
`sudo passwd <username>` - Changes password for specific user account. <br>

Note: All the configuration files in Linux are stored as text format. 
`sudo vim /etc/passwd` - passwd is the location where information about the accounts and path or home directories are shown.
 
####User Management
`sudo groupadd <groupname>` - Creates group with specified name. <br>
`sudo groupdel <groupname>` - Deletes group with specified name. <br>
`sudo adduser <username> <groupname>` - Adds user to the specified group. <br>
`sudo deluser <username> <groupname>` - Deletes user to the specified group. <br>
`sudo vim /etc/group` - Displays the list of all groups and users present in the different groups. <br>

####Setting Permissions:
754 
`7` indicates (all read write & execute) permissions at user level.<br>
`5` indicates permission (read & write) permissions at group level.<br>
`4` indicates only read permission for all web people. <br>

`4` – allows read permission<br>
`2` - allows write permission<br>
`1` – allows execute permission<br>

`sudo chmod 777 <file name>` - Changes permissions at file level, applies all read, write & execute permission at user, group and others. 

`sudo chmod 777 <folder name>-R` - changes permissions at folder level and applies same permissions at subfolders also. 

####Changing ownership: 
`sudo chown –R <username> <folder name>` - Changes ownership of particular folder recursively to mentioned user or changing owner at user level. 

`sudo chgrp -R <groupname> <folder name>` - Changes ownership of particular folder recursively to mentioned group name or changing owner at group level. 

####Linux Networking:
`sudo ifconfig` - Shows all the network cards attached with the computer. 

`sudo dhclient` - Releases and renews the ip address. 

`sudo /etc/init.d/networking restart` - Restarts the networking service once the changes made i.e to update configuration files with the latest changes.
 
`sudo vim /etc/network/interfaces` - Opens the interfaces file where you can add static details like address, netmask, broadcast, network.
 
`sudo vim /etc/resolv.conf` - Updates DNS after running above command or making some static changes or resolve domain name to ip address. 

`sudo /bin/hostname` - Gives the hostname of the computer. 

`sudo /bin/hostname <new hostname>` - changes hostname. 

`ping <some ip address or` [www.google.com](http://www.google.com/) `>` - Pings your computer by address to determine that TCP/IP is functioning. 

####UFW Firewall:
 
Ubuntu comes with built in firewall known as UFW, which is secure, robust & easy to use 

`sudo ufw status` - Gives the status of firewall i.e active or inactive.
 
`sudo ufw default allow` - Allows the all of the network traffic by default.
 
`sudo ufw default deny`- Denies all of the network traffic by default. 

`sudo ufw enable` - Turns on firewall.
 
`sudo ufw disable` - Turns off the firewall. 

`sudo ufw allow <port number>` - Allows particular port. 

`sudo ufw deny 80 or <port number>` - Denies particular port. 

`sudo ufw delete allow 80` - Deletes the rules.
 
`sudo ufw delete deny 80` - Deletes the rules. 

`sudo ufw allow from <ip address>` - Allows that particular ip address to connect to the system. 

`sudo ufw deny from <ip address>` - Denies that particular ip address to connect to the system. 

`sudo ufw allow from <ip address> to <port number>` - Allows only that particular ip address to route to port number. 

`sudo ufw deny from <ip address> to <port number>` - Denies that particular ip address not to route to port number. 

####Steps to Work Remotely using SSH & FTP:
Generally SSH works for port 22, so make sure port is open using ufw firewall. 

`sudo apt-get install ssh` - Downloads & installs ssh on local machine. 

`sudo  ifconfig` - Gives ipaddress, inetaddress. 

`sudo ufw status` - Status must be inactive to open port 22. 

Use terminal emulator putty.exe in windows, gives the pop up with field name called host name where put on ip address and press open.Log in to server which remotely controls server from other computer and run the 

`sudo top` - Which shows other processes running on the server. 

* Initially set vsftpd (very secure ftp daemon on the server side to connect with client) 
sudo apt-get vsftpd 
* Downloads & installs vsftpd. 
sudo vim /etc/vsftpd.conf 
* Make sure these two lines are uncommented `local_enable = YES` (allows local users to log in)
`write_enable = YES` (allows uploads the files from remote) 
* Restart the service to update configuration changes by using below command. 

`sudo service vsftpd restart` 
Open Filezilla (ftp client), log in using ip address, user name and password and then move files from local to remote. 


####Linux Backup using TAR: 
```
sudo tar -cvpzf  backup.tar.gz --exclude=/var/www/video /var/www
```
`c` - creates or overrides<br>
`v` - verbose or shows all operations on terminal & can avoid <br>
`p` - preserves permission<br>
`z` - compresses<br>
`f` - allows to create a filename backup.tar.gz indicates file name which is compressed and <br>
`exclude` - indicates creating backup except those files. 

####Recover using TAR: 
```
mkdir  recover 
sudo tar –xvpzf backup.tar.gz –C /recover
```
`x` indicates execute and recovers the backup file in to the recover directory <br>
`C` indicates create. 

####Cron Jobs:
Cron allows users to run commands or scripts at a given time and date. We can schedule scripts to be executed periodically. It is one of the most important tool in an Linux like operating system. Generally Cron is used for sysadmin jobs such as backups or cleaning /tmp/directories. 

`sudo crontab –e` - Opens editor of your wish and insert the 

m – minutes
h – hours
dom – date of month
mon – months
dow – day of week. 

`m h dom mon dow command`
`0-59 0-23 1-31 1-12 0-6`          

Ex:
```
* * * * * sudo tar –cpzf /backupfolder/minutebackup.tar.gz /var/www/wp-content
```
- Schedules the backup for mentioned period of time.