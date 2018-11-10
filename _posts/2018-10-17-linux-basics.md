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
Print Working Directory | pwd |
Create Directory | mkdir directoryname |
Remove/Delete  Directory | rmdir directoryname | 
Forward Navigation | cd path |
Backward Navigation | cd .. |
| List files in a directory | ls |
| List files with details | ls -l |
| List files and hidden files | ls -a |  
| List everything with all details | ls  -la | 
|-------|--------|
  
 

#####  File Operations
| Create file | touch filename | 
| Delete file | rm filename |
| Write in a file | vim filename, gedit file-name | 
| Read from a file | cat filename | 
| Copy from file1 to file2 | cp file1 file2 | 
| Move/rename from file1 to file2 | mv file1 file2 |  
| Search in a file | grep phrase filename |    
| Differences between two files | diff file1 file2 |   

#####  Compress and Decompress File
 Notations: c: create, v: view on terminal, f: file option, x: extract

 *Compress/Zip:*
 {% highlight unix %} 
 gzip file1
 {% endhighlight %}

 *Decompress/Unzip:* 
 {% highlight unix %}
 gunzip file1.gz  
 {% endhighlight %}

 *Compress/Tar:* 
 {% highlight unix %}
 tar cvf file.tar file1 file2  
 {% endhighlight %}

 *Decompress/Untar:* 
 {% highlight unix %}
 tar xvf file.tar
 {% endhighlight %}


#####  Users

Superuser is  ROOT 

*Set root password:* 
{% highlight unix %}
sudo passwd 
{% endhighlight %} 

*Login as root:* 
{% highlight unix %}
su  
{% endhighlight %}

*Exit from root:* 
{% highlight unix %}
exit  
{% endhighlight %}

*Add user:* 
{% highlight unix %}
sudo useradd username
{% endhighlight %} 

*Add password for user:* 
{% highlight unix %}
sudo passwd username 
{% endhighlight %} 

*Switch user:* 
{% highlight unix %}
su username  
{% endhighlight %} 

*Identify user:* 
{% highlight unix %}
whoami 
{% endhighlight %} 

*Modify username:* 
{% highlight unix %}
sudo usermod -l newusername oldusername
{% endhighlight %} 

*List all user:* 
{% highlight unix %}
getent passwd 
{% endhighlight %} 

*Delete user:* 
{% highlight unix %}
sudo userdel username
{% endhighlight %} 

#####  Groups

*Add group:* 
{% highlight unix %}
sudo groupadd groupname
{% endhighlight %}

*Add user to group:* 
{% highlight unix %}
sudo gpasswd -a user groupname
{% endhighlight %}

*Remove user from group:* 
{% highlight unix %}
sudo gpasswd -d user groupname
{% endhighlight %}

*Rename a group:* 
{% highlight unix %}
sudo groupmod -n newgroupname oldgroupname
{% endhighlight %}

*List all groups:* 
{% highlight unix %}
sudo cat /etc/group
{% endhighlight %}

*Group membership:* 
{% highlight unix %}
sudo groups username
{% endhighlight %}

*Delete group:* 
{% highlight unix %}
sudo groupdel groupname
{% endhighlight %}


#####  File Permissions
 Notations-1 (file owner/user: u, group: g, other people: o):
  
 *Take write permission away from other:* 
 {% highlight unix %} 
 chmod o-w file1
 {% endhighlight %} 
 *Give write permission to other:* 
 {% highlight unix %} 
 chmod o+w file1
 {% endhighlight %} 
 *Take write permission away from file1:* 
 {% highlight unix %} 
 chmod -w file1
 {% endhighlight %}  
 *Give write permission for file1:* 
 {% highlight unix %} 
 chmod +w file1
 {% endhighlight %} 

 Notations-2 (read(r): 4, write(w): 2, execute(x):1, no permission(-): 0):

 *Give everyone all permissions:* 
 {% highlight unix %} 
 chmod 777 file1   
 {% endhighlight %} 

 *u(4+2+1) g(4+1) o(4):*
 {% highlight unix %} 
 chmod 754 file1
 {% endhighlight %} 
 

#####  Network Connections & Proxies
{% highlight unix %}
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
{% endhighlight %} 
 

#####  Install Software 
{% highlight unix %}
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
         1. Ready the tool for compilation: ./configure       
         2. Compile & Build the tool: make       
         3. Load the program: make install  
{% endhighlight %} 

#####  Working with Remote Server: Secure SHell(SSH)
*ssh connect:*
{% highlight unix %}
ssh remote_username@remote_host
{% endhighlight %} 

*ssh disconnect:* 
{% highlight unix %}      
exit
{% endhighlight %} 

#####  Working with Remote Server: Secure File Transfer(SFTP)
*sftp connect:*
{% highlight unix %} 
sftp remote_username@remote_host
{% endhighlight %} 

*sftp disconnect:*    
{% highlight unix %}
exit
{% endhighlight %} 

*Commands on Remote host:* 
{% highlight unix %}
ls, mkdir, pwd, cd ...
{% endhighlight %} 

*Commands on Local host:* 
{% highlight unix %}
lls, lmkdir, lpwd, lcd ...
{% endhighlight %} 

*Download File from Remote Host:*
{% highlight unix %} 
get filename.txt
{% endhighlight %} 

*Download Multiple Files from Remote Host:* 
{% highlight unix %}
mget \*.txt
{% endhighlight %} 

*Download Directory from Remote Host:* 
{% highlight unix %}
get -r directoryname
{% endhighlight %} 

*Upload File to Remote Host:*
{% highlight unix %}
put filename.txt
{% endhighlight %} 

*Upload Multiple Files to Remote Host:* 
{% highlight unix %}
mput \*.txt
{% endhighlight %} 

*Upload Directory to Remote Host:* 
{% highlight unix %}
put -r directoryname
{% endhighlight %} 

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