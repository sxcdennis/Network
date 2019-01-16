# Network Sharing

In this section we'll go over several ways to share over a network. We will cover: scp, rsync, Simple HTTP Server, Basic NFS, and Samba

# scp

scp is a simple file sharing tool that will help copy through a network. scp stands for secure copy, it works exactly how cp command does but allows you to copy from one host to another on the same network.

**Copy file from local host to remote host**

```

$ scp file.txt username@to_remotehostip:/remote_host/directory/


```


**Copy file from a remote host to your local host**

```

$ scp username@remotehostip:file.txt /local_host/directory


```


**Copy a directory from local host to remote host**

```

$ scp -r /local/directory/ username@remotehostip:/remote_host/directory


```


**Copy a directory from remote host to local host**

```

$ scp -r username@remotehostip:/remote_host/directory/ /local_host/directory

```


**Copy file from remote host to remote host**

```

$ scp username@remote_hostip1:/remotehost1/directory/file.txt username@remotehostip2:/remote/directory2/

```


# rsync

rsync (remote sync ) is another tool that copies data to different hosts. It is similar to scp in a sense that it copies data over a network, but has some major differences. Rsync uses a way to check in advanced if there are files or directories that are already present.

So for example, lets say you were copying over a bunch of files but the connection was lost. You don't want to use scp because it would just copy over the same files over. rsync will pick up where you left off.

Common used options with rsync:

**-v:** verbose
**-r:** recursive -copies data recursively
**-a:** archive mode- allows copying files recursively and also preserves symbolic links, file permissions user & group ownerships and timestamps.
**-z:** compresses file data
**-h:** human readable - outputs numbers in a human-readable format.


**Copying/Sync Files & Directories locally**

```

$ rsync -zvrh /local/directory/one /local/directory/two

```

**Copying/Syncing Files & Directories from a remote host to local host**

```

$ rsync /local/directory username@remotehost.ip:/remotehost/directory


```

**Copy/Syncing Files & Directories from local host to remote host**


```

$rsync username@remotehost.ip:/remotehost/directory /localhost/directory


```



# Simple HTTP Server


Pyhton has a super useful tool that can share files using HTTP. This sets up a basic webserver that can access via localhost address. You just need to go to the directory you want to share and use the command:

```

$ python -m SimpleHTTPServer

```

You can access the files in a web browser by typing: http://YOUR_localhost_IPADRESS:8000


# Basic NFS

The most standard network file share for Linux is NFS ( Network File System), NFS allows servers to share directories and files with one or more clients over the network.

We wont get into details of NFS, but to read further about it go to
[Installing NFS](http://github.com/sxcdennis/Installing%20NFS.md)


# Samba

Samba is used for sharing files and resources like printers. We will go over some of the basics step for installing and using samba.


**1. Install Samba**
```

yum install -y samba

```

**2. Set up smb.conf**
The config file for samba is found in /etc/samba/smb.conf, the file should tell the system what directories should be shared, the permissions and more options. The default smb.conf comes with lots of comments to help you get started on what you need.

```

sudo vi /etc/samba/smb.conf


```

**3. Set up password and user for Samba**

```

sudo smbpasswd -a [username]

```

**4.Create shared directory**

```

mkdir /name_of_directory/to_share/

```

**5. Restart Samba Service**

```

sudo systemctl restart samba

```

**Accessing Samba share via Windows**

In Windows, just type in the command prompt: ```\\HOST\Sharename```
OR
You can look at network directory, and it should be able to show there as well.

**Accessing a Samba/Windows share via Linux**

```

smbclient //HOSTIP/directory -U user

```

**Attach a Samba share to your system**

Instead of transfering files one by one, you can just mount the entire network share on your system.

```

sudo mount -t cifs servername:/directory_point/ mountpoint -o user=your_sambauser,pass=password

```



[< Back: Table Of Contents](https://github.com/sxcdennis/Network "Table of Contents") || [Next: OSI Model >](https://github.com/sxcdennis/Network/blob/master/OSI.md "OSI Model")
