# SSH
Secure Shell (SSH) is an encrypted protocol used to administer and communicate with other devices. You can log into other devices with the command ssh

#SSH Server Configuration

For Linux, typically OpenSSH is the suite that is provided. If you don't have it installed you can do so by installing ```openssh and openssh-server```
Start the ssh by running

```
systemctl start sshd
systemctl enable sshd

```

**/etc/ssh/sshd_config**

To configure ssh you can check the configuaration file located at /etc/ssh/sshd_config

Some things to take note to:

**Port** - You may want to change the default port number if you want .  

**MaxSessions** - Maybe you only want a certain amount of people on your server at once

**MaxTries**- Max amount of attempts someone can take

**PermitRootLogin** - Some may want to disable root login from remote hosts.

**PasswordAuthentication** - If you want to only use public/private keys to authenticate you can turn this off. (It's on by default)

# Hosts Set-up

Hosts are devices that you want to use to log into your ssh server. By default, you can log in with just a password and a public key. You can log in with various SHH clients like PuTTY which comes with auto generating keys.

With OpenSSH, it comes with ssh-keygen and ssh-copyid tools, which help create public/private keys and add to servers.

# Keys
The following is a guide to setting up ssh-keys from your host to your server.


**1. We first start by creating a key using ssh-keygen on your host.**


```

ssh-keygen

```
After entering the command, you should see the following prompt:

```

Output
Generating public/private rsa key pair.
Enter file in which to save the key (/your_home/.ssh/id_rsa):

```
Press ENTER to save the key pair into the .ssh/ subdirectory in your home directory, or specify an alternate path.

Then you will be prompted again:

```
Enter passphrase (empty for no passphrase):

```

You can add an addiational security measure by entering a passphrase.

Then you should see the following output:

```
Your identification has been saved in /your_home/.ssh/id_rsa.
Your public key has been saved in /your_home/.ssh/id_rsa.pub.
The key fingerprint is:
a9:49:2e:2a:5e:33:3e:a9:de:4e:77:11:58:b6:90:26 username@remote_host
The key's randomart image is:
+--[ RSA 2048]----+
|     ..o         |
|   E o= .        |
|    o. o         |
|        ..       |
|      ..S        |
|     o o.        |
|   =o.+.         |
|. =++..          |
|o=++.            |
+-----------------+

```
You now have a public and private key that you can use to authenticate. The next step is to place the public key on your server so that you can use SSH-key-based authentication to log in.


**2. Copy the Public Key to Server**
To copy the public key to server we use the tool ssh-copy-id


```
ssh-copy-id username@remotehost

OR

ssh-copy-id -i /path/to/file username@remotehost


```

Next, the utility will scan your local account for the id_rsa.pub key that we created earlier. When it finds the key, it will prompt you for the password of the remote user's account.

Once you've finsihed typing in the password, the utility will connect to the account on the remote host using the password you provided. It will then copy the contents of your ~/.ssh/id_rsa.pub key into a file in the remote account's home ~/.ssh directory called authorized_keys.

**3. Authenticate your Server Using SSH Keys**

Once you've successfully completed the whole procedures you can login without the remote hosts password. (if you've disabled it on the server )

To test this :

```

ssh username@remote_host

```


# Summary

This is just the basics of ssh, it gets a bit more deep into security and keys.


[< Back: DNS](https://github.com/sxcdennis/Network/blob/master/DNS.md "DNS") || [Next: SSL & TLS >](https://github.com/sxcdennis/Network/blob/master/SSL%20%26%20TLS.md "SSL & TLS")
