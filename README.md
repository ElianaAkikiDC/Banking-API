# Banking-API
user: opc  
password: vncpasswd  
port: 5901  
  
user: oracle  
password: vncpasswd  
port: 5902  

# Attach volume block
Create and Attach volume block to instance.
Display details about block devices
``` lsblk ```

Create file system in the chosen disk
``` sudo mkfs -t ext3 /dev/sdb ```

Create a directory to which you will mount the disk for example:
``` mkdir /mnt/OBA ```

Mount the volume to the directory created
``` sudo mount /dev/sdb /mnt/OBA ```

Update the File System Table
``` sudo nano /etc/fstab ```

Add at the end of the file 
``` /dev/sdb /mnt/OBA ext3 defaults, nofail 0,0 ```

Reboot the instance


# 1- Create a VM oracle linux 8.3   
Create an instance on Oracle Cloud Infrastructure with 4 ocpu and 64 GRAM    

# 2- Download Oracle Database 19.16.0.0.0   
** Download from Oracle software Delivery Cloud ( https://edelivery.oracle.com/osdc/faces/Home.jspx;jsessionid=NYEE-VQioEO6JUCWuIlH51PGuUD0G7-TIyF5_hpk2sruBFBlXXgs!-209191303 ) the wget.sh file.  

Create a new profile "ProfileOpenBanking.tlp" in Bitvise: press on "client key manager" then press on "import" and add the downlooaded private key of the VM created in step 1 and this will save them in a loaction called "profile 1". host > 193.123.66.121, port > 22, username > opc, initial method > publickey, client key > profile 1, elevation > default.   

Press "Add" in Bitvise: Listen interface > loacal host, Destination host > localhost, port > 5901, check > Accept server-configured port forwardings, press on "apply" and "login"  

Press on "new SFTP window" in Bitvise and drag and drop the wget.sh file to the "remote files" section   

Execute the following commands in a terminal in Putty:  
```mkdir software```  
```cd software```  
```ls ```  
```chmod +x wget.sh```  
```ls -ltr```   
```./wget.sh``` **  

# Install VNC on Oracle Linux 8  
Use the following tutorial: https://youtu.be/Z5vhER7K34E  

Install a Graphical Desktop Environment: Install a GNOME desktop environment and all of its dependencies.  
```sudo dnf group install "Server with GUI"```  

Set graphical mode as the default login type for user accounts, then reboot the server.  
```sudo systemctl set-default graphical```  
```sudo reboot```  
  
# Download TigerVNC  
Download it from: https://sourceforge.net/projects/tigervnc/  
(password: vncpasswd and no view once password)  
  
```sudo dnf install -y tigervnc-server```  
```vncpasswd ```  
```sudo vi /etc/tigervnc/vncserver.users```  
```sudo vi /etc/```  
```sudo vi /etc/tigervnc/vncserver-config-defaults```  
```sudo systemctl daemon-reload```  
```sudo systemctl enable --now vncserver@:1.service```  
```sudo systemctl status vncserver@:1.service```  
```vi /etc/systemd/system/multi-user.target.wants/vnc```  
```sudo systemctl daemon-reload```  
```sudo systemctl status vncserver@:1.service```  
```sudo firewall-cmd --add-port=5901/tcp```  
```sudo firewall-cmd --permanent --add-port=5901/tcp```  
```sudo firewall-cmd --reload```  
```sudo firewall-cmd --list-all```  
```sudo systemctl daemon-reload```  
```sudo systemctl status vncserver@:1.service```  

# 3- Download Oracle Java Development Kit 11.0.16 on Oracle software Delivery Cloud

# 4- Download Oracle Weblogic Server 14.1.1.0.0 on Oracle software Delivery Cloud

# 5- Download Python Package: urwid 2.1.2 on Oracle software Delivery Cloud

# 6- Download Gradle 7.5.1 on Oracle software Delivery Cloud

# PS: Repeat  ** ... ** in step 2 for the other steps.
