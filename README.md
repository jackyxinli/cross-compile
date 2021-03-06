1. arm-none-eabi-gcc  
（ARM architecture，no vendor，not target an operating system，complies with the ARM EABI）  
用于编译 ARM 架构的裸机系统（包括 ARM Linux 的 boot、kernel，不适用编译 Linux 应用 Application），一般适合 ARM7、Cortex-M 和 Cortex-R 内核的芯片使用，所以不支持那些跟操作系统关系密切的函数，比如fork(2)，他使用的是 newlib 这个专用于嵌入式系统的C库。

2. arm-none-linux-gnueabi-gcc  
   arm-linux-gnu-gcc  
(ARM architecture, no vendor, creates binaries that run on the Linux operating system, and uses the GNU EABI)  
主要用于基于ARM架构的Linux系统，可用于编译 ARM 架构的 u-boot、Linux内核、linux应用等。arm-none-linux-gnueabi基于GCC，使用Glibc库，经过 Codesourcery 公司优化过推出的编译器。arm-none-linux-gnueabi-xxx 交叉编译工具的浮点运算非常优秀。一般ARM9、ARM11、Cortex-A 内核，带有 Linux 操作系统的会用到。

# Establish environment of cross compile on fedora 29 or upper

````c
# dnf install arm-none-eabi-gcc
# dnf install arm-none-eabi-newlib
# dnf install gcc-arm-linux-gnu
# dnf install glibc-arm-linux-gnu

# cd ~
# vim .bashrc

C_INCLUDE_PATH=$C_INCLUDE_PATH:/usr/arm-linux-gnu/include
export C_INCLUDE_PATH

# source .bashrc
# cd ~
# curl http://ffmpeg.org/releases/ffmpeg-4.1.4.tar.gz
# tar -zxf ffmpeg-4.1.4.tar.gz
# cd ffmpeg-4.1.4
# ./configure --prefix=/root/arm/ffmpeg --enable-gpl --enable-version3 --enable-nonfree --enable-cross-compile --arch=arm --target-os=linux --cross-prefix=arm-linux-gnu- --cc=arm-linux-gnu-gcc --enable-pthreads --disable-doc --disable-debug --disable-x86asm --disable-static --enable-shared
````

# Establish environment of cross compile on ubuntu 18.04 or upper

````c
# apt install gcc-arm-none-eabi
# apt install arm-linux-gnueabi
# apt install arm-linux-gnueabihf

# cd ~
# curl http://ffmpeg.org/releases/ffmpeg-4.1.4.tar.gz
# tar -zxf ffmpeg-4.1.4.tar.gz
# cd ffmpeg-4.1.4
# ./configure --prefix=/root/arm/ffmpeg --enable-gpl --enable-version3 --enable-nonfree --enable-cross-compile --arch=arm --target-os=linux --cross-prefix=arm-linux-gnueabihf- --cc=arm-linux-gnueabihf-gcc --enable-pthreads --disable-doc --disable-debug --disable-x86asm --disable-static --enable-shared
````