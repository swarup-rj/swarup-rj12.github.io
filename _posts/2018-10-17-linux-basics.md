---
title: "Linux Commands"
layout: post
date: 2018-10-17
tags: blog
comments: true
---

#####  Terminal (username@host:path)
*Open terminal:*
{% highlight unix %}
Ctrl+Alt+T
{% endhighlight %} 

#####  Directory Operations

| Operation | Command |
|-------|--------|
Print working directory | pwd |
Create directory | mkdir directoryname |
Remove/Delete  directory | rmdir directoryname | 
Forward navigation | cd path |
Backward navigation | cd .. |
| List files in a directory | ls |
| List files with details | ls -l |
| List files and hidden files | ls -a |  
| List everything with all details | ls  -la | 
|-------|--------|
  
 

#####  File Operations

 Notations: 
 c: create, v: view on terminal, f: file option, x: extract, f: allows to specify the filename of the archive

| Operation | Command |
|-------|--------|
| Create file | touch filename | 
| Delete file | rm filename |
| Write in a file | vim filename, gedit file-name | 
| Read from a file | cat filename | 
| Copy from file1 to file2 | cp file1 file2 | 
| Move/rename from file1 to file2 | mv file1 file2 |  
| Search in a file | grep phrase filename |    
| Differences between two files | diff file1 file2 | 
| Compress/Zip a file|  gzip filename |
| Decompress/Unzip | gunzip filename.gz |  
| Compress/Tar | tar cvf filename.tar file1 file2 |  
| Decompress/Untar | tar xvf filename.tar |
|Create a archive and compress it|tar -czvf archive.tar.gz directoryname|  
|-------|--------|




#####  Users

| Operation | Command |
|-------|--------|
|Set root (superuser) password | sudo passwd |
|Login as root | su |  
|Exit from root | exit |  
|Add user | sudo useradd username |
|Add password for user | sudo passwd username | 
|Switch user | su username |  
|Identify user | whoami | 
|Modify username | sudo usermod -l newusername oldusername |
|List all user | getent passwd | 
|Delete user | sudo userdel username |
|-------|--------| 

#####  Groups

| Operation | Command |
|-------|--------|
|Add group | sudo groupadd groupname|
|Add user to group | sudo gpasswd -a user groupname|
|Remove user from group | sudo gpasswd -d user groupname|
|Rename a group | sudo groupmod -n newgroupname oldgroupname|
|List all groups | sudo cat /etc/group|
|Group membership | sudo groups username|
|Delete group | sudo groupdel groupname|
|-------|--------| 

#####  File Permissions

Notations-1 (file owner/user: u, group: g, other people: o)

Notations-2 (read(r): 4, write(w): 2, execute(x):1, no permission(-): 0)
  
| Operation | Command |
|-------|--------| 
| Take write permission away from other | chmod o-w file1 |
| Give write permission to other | chmod o+w file1 |
| Take write permission away from file1 | chmod -w file1 |
| Give write permission for file1 | chmod +w file1 |
| Give everyone all permissions | chmod 777 file1 |   
| u(4+2+1) g(4+1) o(4) | chmod 754 file1 |
|-------|--------|  

#####  Network Connections & Proxies

1. Network Configurations:  
2. Browser Configurations:  
3. Network Proxy Setting: 

    Home > network proxy > manual > host:port_no > apply system wide  

4. Terminal Proxy Setting: 

    *Open the file:* 

        sudo gedit /etc/apt/apt.conf 

    *Include the folowings in the above file:*  

        Acquire::http::proxy "http://username:password@host:port_no/";      
        Acquire::https::proxy "https://username:password@host:port_no/";      
        Acquire::ftp::proxy "ftp://username:password@host:port_no/";      
        Acquire::socks::proxy "socks://username:password@host:port_no/";
 

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
     Download and compile and install: 

        sudo apt-get install packagename  

     Update: 

        sudo apt-get update   

     Upgrade: 

        sudo apt-get upgrade  

     Uninstall: 

        sudo apt-get remove packagename 

     Uninstall and Remove configuration files: 

        sudo apt-get purge packagename  

5. Install .tar File:  
    1. Unpack the tar file: 

        tar xvfz 7z.tar.gz  

    2. Navigate to the file: 

        cd filepath   

    3. Read INSTALL.txt or README for compiling process.      
        
        Classical Steps:       
         1. Ready the tool for compilation: 

            ./configure  

         2. Compile & Build the tool: 

            make

         3. Load the program: 

            make install   

#####  Working with Remote Server: Secure SHell(SSH)

| Operation | Command |
|-------|--------| 
|ssh connect | ssh remote_username@remote_host|
|ssh disconnect | exit|
|-------|--------| 

#####  Working with Remote Server: Secure File Transfer(SFTP)

| Operation | Command |
|-------|--------| 
|sftp connect | sftp remote_username@remote_host|
|sftp disconnect | exit|
|Commands on Remote host | ls, mkdir, pwd, cd ...|
|Commands on Local host | lls, lmkdir, lpwd, lcd ...|
|Download File from Remote Host | get filename.txt|
|Download Multiple Files from Remote Host | mget \*.txt|
|Download Directory from Remote Host | get -r directoryname|
|Upload File to Remote Host | put filename.txt|
|Upload Multiple Files to Remote Host | mput \*.txt|
|Upload Directory to Remote Host | put -r directoryname|
|-------|--------|


#### Working with Remote Server: Secure Copy (SCP)) :
    
*Secure Copy a File from Local host to a Remote host:*
    {% highlight unix %}
    scp filename.txt username@remotehost:path
    {% endhighlight %}

*Secure Copy a File from Local host to Home Directory on Remote Host:* 
    {% highlight unix %}
    scp filename.txt username@remotehost:~
    {% endhighlight %}

*Secure Copy Multiple Files from Local host to a Remote host:*
{% highlight unix %}
scp file1.txt file2.txt your_un@rh.edu:~ 
{% endhighlight %}

*Secure Copy a Directory from Local host to a Remote host:*
{% highlight unix %}
scp -r directoryname username@remotehost:path/directoryname
{% endhighlight %}

*Secure Copy Using port 2264 from Local host to a Remote host:*
{% highlight unix %}
scp -P 2264 filename.txt username@remotehost:~
{% endhighlight %}

*Secure Copy a File from Remote host to a Local host:*
{% highlight unix %}   
scp username@remotehost:filename.txt path
{% endhighlight %}

*Secure Copy Multiple Files from Remote host to a Local host:*
{% highlight unix %}
scp username@remotehost:~/\{file1.txt,file2.txt\}
{% endhighlight %}

*Secure Copy from Remote Host "rh1" to "rh2":*
{% highlight unix %}
scp username@rh1:path/filename.txt \username@rh2:path/
{% endhighlight %}

#####  Command Help
{% highlight unix %}
info command 

help command
{% endhighlight %} 