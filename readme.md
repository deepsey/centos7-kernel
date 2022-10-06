#### Preinstall 

    yum install gcc  
    yum install flex  
    yum install bison   
    yum install elfutils-libelf-devel  
    yum install openssl-devel  
    yum install epel-release  
    yum update
    yum install -y wget gcc flex bison elfutils-libelf-devel openssl-devel perl  
  
#### Update GCC:
Often people want the most recent version of gcc, and devtoolset is being kept up-to-date, so maybe you want devtoolset-N where N={4,5,6,7...}, check yum for the latest available on your system). Updated the cmds below for N=7.  

There is a package for gcc-7.2.1 for devtoolset-7 as an example. First you need to enable the Software Collections, then it's available in devtoolset-7:  

    sudo yum install centos-release-scl
    sudo yum install devtoolset-7-gcc*
    scl enable devtoolset-7 bash
    which gcc

And cheking gcc version:  

    gcc --version  
    gcc (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)  
    Copyright (C) 2017 Free Software Foundation, Inc.  
    This is free software; see the source for copying conditions.  There is NO  
    warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  


## Installing a new kernel for Oracle Linux 

#### Preinstall

    yum install epel-release flex bison elfutils-libelf-devel openssl openssl-devel bc
    wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.19.12.tar.xz
    tar -xf linux-5.19.12.tar.xz 
    cp /boot/config-4.18.0-372.26.1.0.1.el8_6.x86_64 .config
    
#### Install

    make oldconfig
    make -j12
    make install    
    make modules_install
    
   

