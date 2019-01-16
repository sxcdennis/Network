# Installing NFS


To install we need both NFS server and NFS Client. A NFS Client can read and write files/directories as if it were a local drive. So basically a NFS Server is hosting a share to its directory with read/write permissions.


# On the NFS Server Machine

**1. Install & enable Packages**

```
yum install -y nfs-utils
systemctl enable nfs-server.service
systemctl start nfs-server.service

```

**2. Create Directory that will be shared via NFS***

```

mkdir /var/nfs


```

**3. Change permissions of the directory**

```

chmod -R 755 /var/nfs
chown nfsnobody:nfsnobody /var/nfs

```

Note: make sure you choose a directory that is safe. the /home directory would cause huge security risks, but if you DO decide to share /home directory make sure you do not change the permissions of it.


**4. Share NFS directories over Network**

```

vi /etc/exports


```

add line

```

/home     192.168.101.227(rw,sync,no_root_squash,no_all_squash)
#note that 192.168.101.227 is my current ip for my server machine. You must change to your own.


```

**Step 5. Add firewall public zones**

```

firewall-cmd --permanent --zone=public --add-service=nfs
firewall-cmd --permanent --zone=public --add-service=mountd
firewall-cmd --permanent --zone=public --add-service=rpc-bind
firewall-cmd --reload

```

**Step 6. Restart NFS Service:**

```

systemctl restart nfs-server


```

# On NFS Client Machine


**1. Install Package**

```

yum install nfs-utils

```


**2. Create NFS Directory Mount Points:**

```

mkdir -p /mnt/nfs/var/nfs


```

**3. Mount the NFS shared directory from server to client:**


```

mount -t nfs 192.168.101.227:/var/nfs /mnt/nfs/var/nfs


```

**4. Check connected NFS**

```

df -kh

```

**4.5 If you want to permanently mount to NFS Server**

```

vi /etc/fstab

```

add lines:

```

192.168.101.227:/var/nfs    /mnt/nfs/var/nfs nfs defaults 0 0

```

**5. Test to see if it works**

```

touch /mnt/nfs/var/nfs/test_nfs.txt

```

[< Back: Port Bonding](https://github.com/sxcdennis/Network/blob/master/Port%20Bonding.md "Port Bonding")
