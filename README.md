# cmake_helloworldDriver
 example of cmake for linux driver
 
 A simple hello world kernel module, that can be build with cmake.
Utilize Kbuild through cmake, and do it in a build directory.


Usage:
1) got clone 
2) create a folder: mkdir build
3) navigate into build: cd build
4) run cmake: cmake ../
5) build it: make



Expected behavior: 

cmake ../ shall do:
```
$ cmake ../
-- The C compiler identification is GNU 11.3.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
my kerneldir path is "/lib/modules/5.15.0-56-generic/build"
-- Configuring done
-- Generating done
-- Build files have been written to: /home/a/Downloads/upd1553lin407a/test2/cmake-kernel-module/build
```
make shall do:
```
make
[100%] Generating hello.ko
[100%] Built target driver
```

Among others the hello.ko is now present. 

See also about linux driver for beginner
https://habr.com/ru/post/342668/
https://habr.com/ru/company/timeweb/blog/680850/

Thoughts and comments are welcome. 
