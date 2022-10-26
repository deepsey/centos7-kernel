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
    
    
    
## How to make vagrant shares vbox folders with a new kernel

First there was adding the new kernel 6.0.3-1.el7.elrepo.x86_64:  

    # yum install -y http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
    # yum --enablerepo elrepo-kernel install kernel-ml -y
    # grub2-mkconfig -o /boot/grub2/grub.cfg
    # grub2-set-default 0

After reboot we have 

    # uname -r
       6.0.3-1.el7.elrepo.x86_64
       
But no shared folder because of no VBox Additionals. To install the last ones we need to install kernel-headers for our current kernel. Let's do it:
 
    # yum remove kernel-headers
    # yum --enablerepo elrepo-kernel install kernel-ml-headers.x86_64 -y

And we need to install gcc version 9.3.0 to install headers. Let's do it:

    # mkdir gcc
    # cd gcc/
    # wget http://mirror.linux-ia64.org/gnu/gcc/releases/gcc-9.3.0/gcc-9.3.0.tar.gz
    # tar -xvf gcc-9.3.0.tar.gz 
    # cd gcc-9.3.0/
    # ./configure --enable-languages=c,c++ --disable-multilib
    # make
    # make install
    
After reboot check gcc version:

    # gcc --version
      gcc (GCC) 4.8.5 20150623 (Red Hat 4.8.5-44)
      Copyright (C) 2015 Free Software Foundation, Inc.
      
Now we can build headers:

    # /sbin/rcvboxadd quicksetup all
    
And after *vagrant reload* we can see our mounted shared folders.




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
    
   

