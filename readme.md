## Installing linux kernel 6.0.5 from source code 

### Preinstall 
**1. Install some needed packages**

    sudo yum install epel-release  
    sudo yum install -y wget gcc flex bison elfutils-libelf-devel openssl-devel perl
    
**2. Install gcc 9.3.0 version**
    
    mkdir gcc
    cd gcc/
    wget http://mirror.linux-ia64.org/gnu/gcc/releases/gcc-9.3.0/gcc-9.3.0.tar.gz
    tar -xvf gcc-9.3.0.tar.gz
    cd gcc-9.3.0/
    sudo yum -y install bzip2 wget gcc gcc-c++ gmp-devel mpfr-devel libmpc-devel make
    ./configure --enable-languages=c,c++ --disable-multilib
    make -j12
    sudo make install
    gcc --version
      gcc (GCC) 9.3.0

   17  sudo gcc --version

    yum install gcc  
    yum install flex  
    yum install bison   
    yum install elfutils-libelf-devel  
    yum install openssl-devel  
    yum install epel-release  
    yum update
    yum install -y wget gcc flex bison elfutils-libelf-devel openssl-devel perl  
    
sudo yum install epel-release  
    2  sudo yum update
    3  yum install -y wget gcc flex bison elfutils-libelf-devel openssl-devel perl  
    4  sudo yum install -y wget gcc flex bison elfutils-libelf-devel openssl-devel perl  
    5  mkdir gcc
    6  cd gcc/
    7  wget http://mirror.linux-ia64.org/gnu/gcc/releases/gcc-9.3.0/gcc-9.3.0.tar.gz
    8  tar -xvf gcc-9.3.0.tar.gz
    9  cd gcc-9.3.0/
   10  ./configure --enable-languages=c,c++ --disable-multilib
   11  sudo yum -y install bzip2 wget gcc gcc-c++ gmp-devel mpfr-devel libmpc-devel make
   12  ./configure --enable-languages=c,c++ --disable-multilib
   13  make -j12
   14  make install
   15  sudo make install
   16  gcc --version
   17  sudo gcc --version
   18  wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.0.5.tar.xz
   19  ls
   20  mv linux-6.0.5.tar.xz ~/
   21  cd
   22  tar -xf linux-6.0.5.tar.xz 
   23  cp /vagrant/kernel_5.4/.config ~/linux-6.0.5
   24  cd linux-6.0.5/
   25  make oldconfig
   26  cp /vagrant/.config ~/linux-6.0.5
   27  make oldconfig
   28  make -j12
   29  sudo make modules_install
   30  sudo halt -p
   31  cd linux-6.0.5/
   32  sudo make install
   33  ls /boot
   34  grubby --info=all
   35  sudo grub2-mkconfig -o /boot/grub2/grub.cfg
   36  sudo grubby --info=all
   37  sudo grubby --info=ALL
   38  sudo grub2-set-default 0
   39  exit
   40  uname -r


    
  
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

    $ gcc --version
      gcc (GCC) 9.3.0
      Copyright (C) 2019 Free Software Foundation, Inc.

      
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
    
   

