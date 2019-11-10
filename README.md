# glow-ubuntu-helpers
Ubuntu OS variant helper install/configure scripts for Pytorch Glow <https://github.com/pytorch/glow>

## Ubuntu 16.04 Xenial Xerius and LLVM 7
Ubuntu 16.04 Xenial Xerius ships with an outdated version of LLVM - see <https://packages.ubuntu.com/xenial/devel/llvm>

Building Glow on Ubuntu 16.04 with LLVM 7 will fail because LLVM 7 distribution from Xenial uses an older C++ ABI.

To update, you can run:

    sudo apt-get install clang clang-8 cmake graphviz libpng-dev \
        libprotobuf-dev llvm-8 llvm-8-dev ninja-build protobuf-compiler wget \
        opencl-headers libgoogle-glog-dev

Then follow the configure/build instructions from <https://github.com/pytorch/glow#configure-and-build>

## Ubuntu 16.04 Xenial Xerius and LLVM 8

To update, you can run:

    sudo apt-get install clang clang-8 cmake graphviz libpng-dev \
        libprotobuf-dev llvm-8 llvm-8-dev ninja-build protobuf-compiler wget \
        opencl-headers libgoogle-glog-dev

Then follow the configure/build instructions from <https://github.com/pytorch/glow#configure-and-build>

## Ubuntu 16.04 Xenial Xerius and LLVM 9

TODO

## Ubuntu 18.04 Bionic Beaver and LLVM 8

Ubuntu 18.04 Xenial Xerius ships with an outdated version of LLVM - see <https://packages.ubuntu.com/bionic/llvm>

To update, you can run:

    sudo apt-get install clang clang-8 cmake graphviz libpng-dev \
        libprotobuf-dev llvm-8 llvm-8-dev ninja-build protobuf-compiler wget \
        opencl-headers libgoogle-glog-de
        
Then follow the configure/build instructions from <https://github.com/pytorch/glow#configure-and-build>

## Ubuntu 18.04 Bionic Beaver and LLVM 9

TODO

## Ubuntu 19.04 Disco Dingo and LLVM 8

Ubuntu 19.04 Disco Dingo ships with LLVM 8 by default - see <https://packages.ubuntu.com/disco/llvm>

If you want to build Glow against LLVM 8, you can simply install the other dependencies:

    sudo apt-get install clang clang-8 cmake graphviz libpng-dev \
        libprotobuf-dev ninja-build protobuf-compiler wget \
        opencl-headers libgoogle-glog-dev

Then follow the configure/build instructions from <https://github.com/pytorch/glow#configure-and-build>

## Ubuntu 19.04 Disco Dingo and LLVM 9

TODO

## General Notes

It may be desirable to use update-alternatives to manage the version of clang/clang++:

sudo update-alternatives --install /usr/bin/clang clang \
    /usr/lib/llvm-8/bin/clang 50
sudo update-alternatives --install /usr/bin/clang++ clang++ \
    /usr/lib/llvm-8/bin/clang++ 50

Glow uses the system default C/C++ compiler (/usr/bin/c++), and so you may also want to switch your default C/C++ compiler to clang:

sudo update-alternatives --config cc
    # Select the option corresponding to /usr/bin/clang ...
sudo update-alternatives --config c++
    # Select the option corresponding to /usr/bin/clang++ ...
Glow should build just fine with gcc (e.g. gcc 5.4), but we mostly use clang and are more attentive to compatibility with clang.

Finally, in order to support the ONNX net serialization format, Glow requires protobuf >= 2.6.1, but the above command may install older version on older Ubuntu (e.g. 14.04). If this is the case, we suggest to look at utils/install_protobuf.sh to install a newer version from source.
