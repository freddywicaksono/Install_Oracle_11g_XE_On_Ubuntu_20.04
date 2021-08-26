# Install_Oracle_11g_XE_On_Ubuntu_20.04

## Download Oracle 11g XE R2
```
$ mkdir ~/Downloads
$ cd Downloads
$ wget http://download.xskernel.org/soft/linux-rpm/oracle-xe-11.2.0-1.0.x86_64.rpm.zip
```

## Install Unzip
```
sudo apt install unzip
```

## Unzip Oracle 11g XE
```
unzip oracle-xe-11.2.0-1.0.x86_64.rpm.zip
```
## Install RPM to Deb Converter
```
sudo apt install alien
```
## Install Additional library
```
sudo apt-get install libaio1 unixodbc
```
## Activate Oracle 11g XE location
```
cd Disk1
```
## Convert Oracle 11g XE rpm to deb
```
sudo alien --scripts -d oracle-xe-11.2.0-1.0.x86_64.rpm
```
Wait the process until ...
```
oracle-xe_11.2.0-2_amd64.deb generated
```
## Create a special chkconfig script
```
sudo nano /sbin/chkconfig
```
Copy-Paste this script:
```
#!/bin/bash
# Oracle 11gR2 XE installer chkconfig hack for Ubuntu
file=/etc/init.d/oracle-xe
if [[ ! `tail -n1 $file | grep INIT` ]]; then
echo >> $file
echo '### BEGIN INIT INFO' >> $file
echo '# Provides: OracleXE' >> $file
echo '# Required-Start: $remote_fs $syslog' >> $file
echo '# Required-Stop: $remote_fs $syslog' >> $file
echo '# Default-Start: 2 3 4 5' >> $file
echo '# Default-Stop: 0 1 6' >> $file
echo '# Short-Description: Oracle 11g Express Edition' >> $file
echo '### END INIT INFO' >> $file
fi
update-rc.d oracle-xe defaults 80 01
```
save the file...

Give execute privilege to the script
```
sudo chmod 755 /sbin/chkconfig
```
## Set the Kernel parameters :
Oracle 11gR2 XE requires to set the following additional kernel parameters:
```
sudo vim /etc/sysctl.d/60-oracle.conf
```
Copy-Paste this script:
```
# Oracle 11g XE kernel parameters  
fs.file-max=6815744  
net.ipv4.ip_local_port_range=9000 65000  
kernel.sem=250 32000 100 128 
kernel.shmmax=536870912
```
save the file

Verify the changes
```
sudo cat /etc/sysctl.d/60-oracle.conf 
```
## Load kernel parameters
```
sudo service procps restart 
```
Verify:
```
sudo sysctl -q fs.file-max
```
## Install net-tools
```
sudo apt install net-tools
```
## Remove Current AWK
```
sudo apt-get remove --auto-remove gawk
```
## Install Original AWK
```
sudo apt-get install original-awk  
```
## Create symlink
```
sudo ln -s -f /usr/bin/awk /bin/awk
```
## Create Listener
Set user as root
```
sudo su
touch /var/lock/subsys/listener 
```
Return as Sudo user
```
exit
```
## Ready to Install Oracle 11g XE
Should be on directory Disk1
```
sudo dpkg --install oracle-xe_11.2.0-2_amd64.deb
```
## Proceed Oracle 11g XE configuration
Set User as root
```
sudo /etc/init.d/oracle-xe configure
```
please do remember the password you fill on this process
the password is for user: sys
## Setup environment variables
```
nano ~/.bashrc
```
Add this script at the end of the file
```
export ORACLE_HOME=/u01/app/oracle/product/11.2.0/xe
export ORACLE_SID=XE
export NLS_LANG=`$ORACLE_HOME/bin/nls_lang.sh`
export ORACLE_BASE=/u01/app/oracle
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH
export PATH=$ORACLE_HOME/bin:$PATH
```
## Load the changes by executing .bashrc file
```
. ~/.bashrc
```
or
```
source ~/.bashrc
```
## Start Oracle 11g XE service
```
sudo service oracle-xe start
```
## Test login to Oracle Console via SqlPlus
```
sqlplus sys as sysdba
```
use password as you set in configure process above
