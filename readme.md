#### Preinstall 

    yum install gcc  
    yum install flex  
    yum install bison   
    yum install elfutils-libelf-devel  
    yum install openssl-devel  
  
#### Update GCC:
Often people want the most recent version of gcc, and devtoolset is being kept up-to-date, so maybe you want devtoolset-N where N={4,5,6,7...}, check yum for the latest available on your system). Updated the cmds below for N=7.  

There is a package for gcc-7.2.1 for devtoolset-7 as an example. First you need to enable the Software Collections, then it's available in devtoolset-7:  

    sudo yum install centos-release-scl
    sudo yum install devtoolset-7-gcc*
    scl enable devtoolset-7 bash
    which gcc
    gcc --version


