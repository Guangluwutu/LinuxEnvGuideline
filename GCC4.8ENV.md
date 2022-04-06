how to install GCC4.8 in server without root

GCC4.8 usuaully be used for compiling by C++11

step download GCC4.8

```
wget https://ftp.gnu.org/gnu/gcc/gcc-4.8.5/gcc-4.8.5.tar.gz
tar zxvf gcc-4.8.5.tar.gz
```

step require prepare

before install gcc, some tools should be installed first, all supports in gcc dir

install perl & gmp & mpfr & mpc(in path already, do commad to auto install those)

```
cd gcc-4.8.5; ./contrib/download_prerequisites
```

step set prefix

set a indivisual obj dir instead of source dir to build.

```
mkdir gcc-4.8.5-build && cd gcc-4.8.5-build
```

do command `gcc -v` to show your current gcc setting which should be referenced for install new one.for exmaple, i choose language c,c++,objc,obj-c++ only,and stage boostrap skipped(`--enable-checking=release` not used ,`--disable-stage1-checking --enable-checking=no` added),enable support plugin(`--enable-plugin`),use same build name(`--build=x86_64-redhat-linux`)

```
../gcc-4.8.5/configure --prefix=/usr/local/gcc-4.8.5 --mandir=/usr/share/man --infodir=/usr/share/info --with-bugurl=http://bugzilla.redhat.com/bugzilla --enable-bootstrap --enable-shared --enable-threads=posix --with-system-zlib --enable-__cxa_atexit --disable-libunwind-exceptions --enable-gnu-unique-object --enable-languages=c,c++,objc,obj-c++ --disable-dssi --enable-libgcj-multifile --with-ppl --with-cloog --with-tune=generic --with-arch_32=i686 --build=x86_64-redhat-linux --disable-stage1-checking --enable-checking=no --enable-plugin
```

step make & make install(parameter based on your cpu cores)

```
make -j8
```


step test(alternative)

```
yum install dejagnu
make -j8 check-gcc
./contrib/test_summary
```

step install

```
make install
```

step update gcc to new

before we do the step , conseidering 5 folders

step fix python problems

if above happend
```
ldconfig: /usr/local/lib/libisl.so.15.3.0-gdb.py is not an ELF file - it has the wrong magic bytes at the start.
ldconfig: /usr/local/gcc-4.8.5/lib/libstdc++.so.6.0.19-gdb.py is not an ELF file - it has the wrong magic bytes at the start.
```
using cmd

```
find /usr/local/lib64 -iname "*.py" | xargs -rI{} mv {} /usr/share/gdb/auto-load/usr/lib
ldconfig
```

step update /usr/include/c++

```
ln -Tfs /usr/local/gcc-4.8.5/include/c++/4.8.3 /usr/include/c++/4.8.3
```

step update /usr/lib/gcc/x86_64_redhat_linux (which depend on your own folder name ,for exmaple`x86_64_rehat-linux`)

```
ln -Tfs /usr/local/gcc-4.8.5/lib/gcc/x86_64_redhat-linux/4.8.3 /usr/lib/gcc/x86_64_redhat-linux/4.8.3
```

step update lib*/libstdc++/so.6( include lib64 and lib)
```
cp /usr/local/gcc-4.8.5/lib/libstdc++/libstdc++.so.6.0.19 /usr/lib; cd /usr/lib; ln -Tfs libstdc++.so.6.0.19 libstdc++.so.6
cp /usr/local/gcc-4.8.5/lib64/libstdc++/libstdc++.so.6.0.19 /usr/lib64; cd /usr/lib64; ln -Tfs libstdc++.so.6.0.19 libstdc++.so.6
```

step update /usr/libexec

```
ln -Tfs /usr/local/gcc-4.8.5/libexec/gcc/x86_64-redhat-linux/4.8.5 /usr/libexec/gcc/x86_64-redhat-linux/4.8.5
```

step update /usr/bin
```
ln -Tfs /usr/local/gcc-4.8.5/bin/c++ /usr/bin/c++
ln -Tfs /usr/local/gcc-4.8.5/bin/cpp /usr/bin/cpp
ln -Tfs /usr/local/gcc-4.8.5/bin/gcc /usr/bin/gcc
ln -Tfs /usr/local/gcc-4.8.5/bin/g++ /usr/bin/g++
```
problem and soulution:

```
c1plus: error: unrecognized command line option "-std=c++14
```

if make couldn`t use correct gcc,usually happend while you did not set prefix while configure, excution file will install in /usr/local/bin

1.set up g++ path in cmake

```
cmake .. -DCMAKE_C_COMPILER=/usr/local/bin/gcc -DCMAKE_CXX_COMPILER=/usr/local/bin/g++
```

2.edit .bashrc

```
CC=/usr/local/bin/gcc
export CC

CXX=/usr/local/bin/g++
export CXX
```

