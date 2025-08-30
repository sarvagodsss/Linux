SSH (Secure Shell)

SSH, also known as Secure Shell or Secure Socket Shell, is a network protocol that provides users, particularly system administrators, with a secure way to access a computer over an unsecured network. It also refers to the suite of utilities that implement the SSH protocol.

SSH provides strong authentication and encrypted data communications between two computers connecting over an open network such as the internet. It is widely used by network administrators for managing systems and applications remotely, allowing them to:

Log into another computer over a network

Execute commands remotely

Move files between systems

Key Features

Secure remote access to SSH-enabled network systems or devices

Secure and interactive file transfer sessions

Automated and secured file transfers

Secure issuance of commands on remote devices or systems

Secure management of network infrastructure components

SSH Basics

Default Port: 22

Configuration file: /etc/ssh/sshd_config

Required Packages: openssh-server, openssh-client, openssh

Daemon Service: sshd

SSH Authentication Types

There are two types of SSH authentication:

Password Based Authentication

Key Based Authentication

1. Password Based Authentication
This is the simplest method of authenticating an SSH connection to another machine. The user provides the password for the account at the time of connection.

Syntax:

ssh user@server_ip
Example:

[root@server0 ~]# ssh root@172.31.19.233

root@172.31.19.233's password:

To enable/disable password-based authentication, edit /etc/ssh/sshd_config:

PasswordAuthentication yes   # enable

PasswordAuthentication no    # disable

2. Key Based Authentication
   
SSH key pairs consist of a public key and a private key.

Private key: Kept secret by the client.

Public key: Shared with the server and stored in ~/.ssh/authorized_keys.

If the client can prove it has the private key, the server grants access without requiring a password.

Steps:

Generate key pair:

ssh-keygen

View keys:

ls ~/.ssh/

# authorized_keys id_rsa id_rsa.pub

Add public key to authorized_keys:

cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

chmod 600 ~/.ssh/id_rsa

chmod 600 ~/.ssh/authorized_keys

Transfer private key to client:

scp ~/.ssh/id_rsa root@172.25.0.10:/root

Login using private key:

ssh -i /root/id_rsa root@172.25.0.11

Additional SSH Examples

Execute Single Remote Command

ssh -i /root/id_rsa root@172.25.0.11 "mkdir /dir_name2"

Run Graphical Applications (X11 Forwarding)

ssh -X root@172.25.0.11

firefox &

Use Custom Port

Edit /etc/ssh/sshd_config:

Port 2020

Allow new port in SELinux:

semanage port -a -t ssh_port_t -p tcp 2020

Restart SSH service:

systemctl restart sshd

Open port in firewall:

firewall-cmd --add-port=2020/tcp

Connect using custom port:

ssh root@172.25.0.11 -p 2020

