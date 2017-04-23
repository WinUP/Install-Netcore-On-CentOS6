## How to install .NET Core 1.1.1 on CentOS 6.8 64bit

This document will introduce how to install .NET Core 1.1.1 on CentOS 6.8 as a portable framework.

#### Pre-request

* Tar file of .NET Core 1.1.1 for CentOS 7.x
* Source code of GCC 6.3.0
* Source code of GLIBC 2.14
* Source code of libunwind 1.2
* libicu 50_1_2 RHEL 6

#### Preparation

1. Compile GLIBC to any folder (e.g /opt/glibc) by using *./configuration --prefix=xxx*.

2. In purpose to use libstdc++, we need to compile GCC. But you can also use libstdc++.so.6 in GCC source code (not recommended). We need to compile GCC to a folder (e.g /opt/gcc), it will take a very lone time may be 4 hours.

3. Compile libunwind to a folder (e.g /opt/libunwind).

4. Extract libicu to a folder (e.g /opt/libicu).

5. Extract .NET Core 1.1.1 to a folder (e.g /opt/dotnet).

#### Installation

0. This part will use all assumption paths in preparation step.

1. Make a symbol link at */usr/local/bin* of file */opt/dotnet/dotnet*. (Very important, must do this.)

2. Create a bash script:

````bash
    #!/bin/bash

    BASE_DIR=/opt

    export LD_PRELOAD=$BASE_DIR/gcc/lib64/libstdc++.so.6.0.22:$BASE_DIR/glibc/lib/libc.so.6:$LD_PRELOAD
    export LD_LIBRARY_PATH=$BASE_DIR/libunwind/lib:$BASE_DIR/libicu/usr/local/lib:$LD_LIBRARY_PATH

    dotnet $*
````

3. Copy this bash to your application's root directory and use this like original dotnet. Makesure you will use *./dotnet* but not *dotnet*.

4. Enjoy!