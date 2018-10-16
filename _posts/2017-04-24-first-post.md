---
title: "Linux Commands: Basic"
layout: post
date: 2018-10-17
tags: blog
comments: true
---

1. TERMINAL(Ctrl+Alt+T) : Home Sweet Home : username@host: path
2. Print Working Directory : pwd
3. LIST FILES : NORMAL LISTING    : ls
   WITH DETAILS      : ls -l
  WITH HIDDEN FILES : ls -a
  EVERYTHING        : ls -la
4. NAVIGATING THROUGH DIRECTORY : FORWARD  : cd path
BACKWARD : cd ..
5. Directory : CREATE :  mkdir directory-name
        REMOVE :  rmdir directory-name
7. FILE : CREATE      : touch file-name
   WRITE       : gedit file-name
   echo "hi" > filename
   ls >> filename
   READ       : cat filename
   COPY        : cp file1 file2
   MOVE/RENAME : mv file1 file2
   REMOVE      : rm file-name
8. SEARCH : grep phrase file-name
9. DIFFERENCES : diff file1 file2
10. COMMAND HELP : info command OR help command
11. PERMISSIONS:
  - / d       # # #           # # #         # # #
 <file / directory  Owner/user : u   Group : g   other people : o>
 chmod o-w file1 : take away write permission from other
 chmod 0+w file1 : give write permission to other
 chmod -w file1  : take away write permission of file1
 chmod +w file1  : give write permission for file1
 <read    : r : 4, write    : w : 2, execute   : x : 1, No permission   : - : 0 >
 chmod 777 file1: everyone get all permission
 chmod 754 file1 : u(4+2+1) g(4+1) o(4)
12. COMPRESS AND DECOMPRESS:
 ZIP   : gzip file1
 UNZIP : gunzip file1.gz
 tar cvf file.tar file1 file2
 tar xvf file.tar
  <c : create, v : view on terminal, f:file option, x:extract>
13. NETWORK CONNECTIONS & PROXIES
NETWORK CONFIGURATION :
BROWSER CONFIGURATION : 
NETWORK PROXY SETTING : 
  Home > network proxy > manual > host:port_no > apply system wide
TERMINAL PROXY SETTING : sudo gedit /etc/apt/apt.conf
  Acquire::http::proxy "http://username:password@host:port_no/";
  Acquire::https::proxy "https://username:password@host:port_no/";
  Acquire::ftp::proxy "ftp://username:password@host:port_no/";
  Acquire::socks::proxy "socks://username:password@host:port_no/";
14. USERS 
SUPERUSER : ROOT 
SET ROOT PASSWORD     : sudo passwd
 LOGIN AS ROOT         : su
 EXIT FROM ROOT        : exit
 NORMAL USER :
 ADD USER        : sudo useradd user-name
 ADD PASSWORD FOR USER : sudo passwd user-name
 SWITCH USER       : su user-name
 IDENTIFYING USER      : whoami
 MODIFY USER NAME      : sudo usermod -l new-u-n old-u-n
 LIST ALL USERS       : getent passwd 
 DELETE USER        : sudo userdel user-name
 GROUP :
 ADD GROUP             : sudo groupadd group-name
 ADD USER TO GROUP     : sudo gpasswd -a user group-name
 REMOVE USER FROM GROUP: sudo gpasswd -d user group-name
 RENAME A GROUP        : sudo groupmod -n new-g-n old-g-n
 LIST ALL GROUPS       : sudo cat /etc/group
 GROUP MEMBERSHIP      : sudo groups user-name 
 DELETE GROUP          : sudo groupdel group-name
15.  INSTALLING SOFTWARE  
UBUNTU SOFTWARE CENTER
SYNAPTIC PACKAGE MANAGER
INSTALL .deb FILE : .deb : Debian applications for Linux
1st Way : 
     1. Download the File.  
     2. Double Click > Opens in Ubuntu Soft. Centre.
    3. Click Install.
2nd Way :  
    1. Navigate to the directory where .deb file is.
    2. Extract .deb file : sudo dpkg -i package.deb
    3. Boom, its installed.
ADVANCE PACKAGE TOOL : apt : command-line
downld+comp.+inst.      : sudo apt-get install package-name
 Updates       : sudo apt-get update
 Upgrade       : sudo apt-get upgrade
 Uninstall       : sudo apt-get remove package-name
 Uninst. & Remv. conf-files  : sudo apt-get purge package-name
INSTALL .tar FILE :
1. Unpack the tar file    : tar xvfz 7z.tar.gz
 2. Navigate to the file      : cd file-path
3. Read INSTALL or INSTALL.txt or README for compiling process.
Classical Steps : 
 i. Ready the tool for compilation  : ./configure 
 ii. Compile & Build the tool  : make
 iii. Load the program   : make install 