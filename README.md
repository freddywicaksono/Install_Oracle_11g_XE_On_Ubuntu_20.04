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
### Wait the process until ...
```
oracle-xe_11.2.0-2_amd64.deb generated
```
