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

#####  Print Working Directory 
*Command (write in terminal):*
{% highlight unix %}
pwd
{% endhighlight %} 

#####  Create and Remove Directory

*Create directory:*
{% highlight unix %}
mkdir directory-name
{% endhighlight %}  

*Remove/Delete  directory:*
{% highlight unix %}
rmdir directory-name
{% endhighlight %}

#####  Navigating Through Directory
*Forward navigation:*
{% highlight unix %}
cd path
{% endhighlight %}

*Backward navigation:*
{% highlight unix %}
cd ..
{% endhighlight %} 

#####  List Files in a Directory
*List files in a directory:*
{% highlight unix %}
ls
{% endhighlight %}
*List files in a directory with details:*
{% highlight unix %}
ls -l
{% endhighlight %}
*List files and hidden files in a directory:*
{% highlight unix %}
ls -a  
{% endhighlight %}
*List everything with all details:*
{% highlight unix %}
ls  -la 
{% endhighlight %}    
 

#####  File Operations
*Create file:* 
{% highlight unix %}
touch filename
{% endhighlight %} 

*Write in a file:* 
{% highlight unix %}
vi filename
gedit file-name 
echo "hi" > filename
ls >> filename
{% endhighlight %} 

*Read from a file:* 
{% highlight unix %}
cat filename
{% endhighlight %} 

*Copy from file1 to file2:* 
{% highlight unix %}
cp file1 file2
{% endhighlight %} 

*Move/rename from file1 to file2:* 
{% highlight unix %}
mv file1 file2  
{% endhighlight %} 

*Delete file:* 
{% highlight unix %}
rm filename  
{% endhighlight %} 

*Search in a file:* 
{% highlight unix %}
grep phrase filename  
{% endhighlight %} 

*Differences between two files:* 
{% highlight unix %}
diff file1 file2  
{% endhighlight %} 

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

#####  Command Help
{% highlight unix %}
info command 

help command
{% endhighlight %} 