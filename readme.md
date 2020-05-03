# Document about syncing direcotries from localhost to remote host in real time.  
# We will use Lsyncd, a light-weight live mirror solution.  
### Install Lsyncd  

`# yum install epel-release`  
`# yum install lsyncd`  

### Setup passwordless login to remote host  

`# ssh-keygen`  
Copy the content of /root/.ssh/id_rsa.pub to remote hosts /home/user/.ssh/authorized_keys.  

### Edit the config file as below  

`vi /etc/lsyncd.conf`  

```
settings {  
logfile = "/var/log/lsyncd/lsyncd.log",  
statusFile = "/var/log/lsyncd/lsyncd.status"  
}  

sync{  
	default.rsyncssh, #implementation method  
	source="/home/vagrant/minio/", #Source directory  
	host="vagrant@192.168.3.18", #Remote host  
	targetdir="/home/vagrant/minio/", #Destination directory  
	delete=false, #Lsyncd will not delete any files on the target. Not on startup nor on normal operation  
	delay=5 #Default 20sec this will run the sync in every 5 seconds.  
	}  
```  

