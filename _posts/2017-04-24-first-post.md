---
title: "Linux Commands: Basic"
layout: post
date: 2018-10-17
tags: blog
comments: true
---

#####  Terminal 

Open terminal: Ctrl+Alt+T  
Home Sweet Home : username@host: path

#####  Print Working Directory 

Command (write in terminal): pwd

#####  List Files

Normal listing: ls  
Listing with details: ls -l  
Listing with hidden files: ls -a  
List everything: ls -la  

#####  Navigating Through Directory

Forward navigation: cd path  
Backward  navigation: cd ..

#####  Directory

Create directory:  mkdir directory-name  
Delete  directory:  rmdir directory-name

#####  File

Create file: touch file-name  
Write in a file: gedit file-name, echo "hi" > filename, ls >> filename  
Read from a file: cat filename  
Copy from file1 to file2: cp file1 file2  
Move/rename from file1 to file2: mv file1 file2  
Delete file: rm file-name  
Search in a file: grep phrase file-name  
Differences between two files : diff file1 file2  

#####  Command Help

info command  
help command

#####  File Permissions
 
 Notations-1:  file owner/user: u, group: g, other people: o   
 Take write permission away from other: chmod o-w file1   
 Give write permission to other: chmod o+w file1   
 Take write permission away from file1: chmod -w file1   
 Give write permission for file1: chmod +w file1
 
 Notations-2: read:r:4, write:w:2, execute:x:1, no permission:-: 0   
 Give everyone all permissions:  chmod 777 file1   
 u(4+2+1) g(4+1) o(4): chmod 754 file1

#####  Compress and Decompress File
 
 Notations: c: create, v: view on terminal, f: file option, x: extract   
 Compress/Zip: gzip file1   
 Decompress/Unzip: gunzip file1.gz   
 Compress/Tar: tar cvf file.tar file1 file2   
 Decompress/Untar: tar xvf file.tar


#####  Network Connections & Proxies

1. Network Configurations:  
2. Browser Configurations:  
3. Network Proxy Setting:  
    Home > network proxy > manual > host:port_no > apply system wide  
4. Terminal Proxy Setting:  
    sudo gedit /etc/apt/apt.conf      
    Edit the file:      
    Acquire::http::proxy "http://username:password@host:port_no/";      
    Acquire::https::proxy "https://username:password@host:port_no/";      
    Acquire::ftp::proxy "ftp://username:password@host:port_no/";      
    Acquire::socks::proxy "socks://username:password@host:port_no/";
    
#####  Users

Superuser is  ROOT  
Set root password: sudo passwd  
Login as root: su  
Exit from root: exit  
Add user: sudo useradd user-name   
Add password for user: sudo passwd user-name  
Switch user: su user-name  
Identify user: whoami  
Modify username: sudo usermod -l new-u-n old-u-n  
List all user: getent passwd  
Delete user: sudo userdel user-name
 
#####  Groups

Add group: sudo groupadd group-name  
Add user to group: sudo gpasswd -a user group-name  
Remove user from group: sudo gpasswd -d user group-name  
Rename a group: sudo groupmod -n new-g-n old-g-n  
List all groups: sudo cat /etc/group  
Group membership: sudo groups user-name  
Delete group: sudo groupdel group-name

#####  Install Software 

1. Ubuntu Software Centre  
2. Synaptic Package Manager  
3. Install .deb(debian applications for Linux) File:  
    1. 1st Way:      
        1. Download the file.          
        2. Double click > opens in ubuntu software centre.          
        3. Click install.          
    2. 2nd Way:      
        1. Navigate to the directory where .deb file is.          
        2. Extract .deb file: sudo dpkg -i package.deb          
        3. Boom, its installed.          
4. Advance Package Tool: apt: command-line  
     Download and compile and install: sudo apt-get install package-name      
     Update: sudo apt-get update       
     Upgrade: sudo apt-get upgrade       
     Uninstall: sudo apt-get remove package-name       
     Uninstall and Remove configuration files: sudo apt-get purge package-name       
     Install .tar File:  
    1. Unpack the tar file: tar xvfz 7z.tar.gz      
    2. Navigate to the file: cd file-path      
    3. Read INSTALL or INSTALL.txt or README for compiling process.      
    Classical Steps:       
     1. Ready the tool for compilation: ./configure       
     2. Compile & Build the tool: make       
     3. Load the program: make install  
