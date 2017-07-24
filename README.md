[![Build Status](https://travis-ci.org/torch/distro.svg?branch=master)](https://travis-ci.org/torch/distro)

Self-contained Torch installation
============

#### Please refer to the [Torch installation guide](http://torch.ch/docs/getting-started.html#_) for details on how to make a fresh install of Torch on Linux or MacOS.
#### If on windows with msvc, please refer to this [guide](win-files/README.md) for details on installation and usage.


## Repo content
#### Dependencies
Globally installed dependencies can be installed via:
```bash
bash install-deps
```
MKL should be installed manully, you can download MKL from this [link](https://registrationcenter.intel.com/en/products/postregistration/?sn=33RM-SVW7ZRXR&EmailID=xiaohui.zhao%40intel.com&Sequence=1791078&dnld=t).

Please activate MKL like this:
```bash
export MKL_ROOT=/opt/intel/mkl
export MKL_INCLUDE=$MKL_ROOT/include
export MKL_LIBRARY=$MKL_ROOT/lib/intel64
source /opt/intel/mkl/bin/mklvars.sh intel64
source /opt/intel/bin/compilervars.sh intel64
export CMAKE_INCLUDE_PATH=$MKL_INCLUDE:$CMAKE_INCLUDE_PATH
export CMAKE_LIBRARY_PATH=$MKL_LIBRARY:$CMAKE_LIBRARY_PATH
```


#### Lua and Torch
The self-contained Lua and Torch installations are performed via:
```bash
./install.sh [intel] [avx512] [mkl] [gomp]
```
param:  
 * intel/gnu    using intel compiler, Default using intel openmp.  
 * avx/avx512   forcing compilers(GCC version should be greater than 4.9) to use AVX512F instructions to compile the framework.  
 * mkl/mklml    using mkl or mklml, Default using mklml.
 * gomp/iomp    using gnu openmp. Default using intel openmp.     

By default Torch will install LuaJIT 2.1. If you want other options, you can use the command:
```bash
# If a different version was installed, used ./clean.sh to clean it
TORCH_LUA_VERSION=LUA51 ./install.sh
TORCH_LUA_VERSION=LUA52 ./install.sh
```

## Update
To update your already installed distro to the latest `master` branch of `torch/distro` simply run:
```bash
./update.sh
```

## Cleaning
To remove all the temporary compilation files you can run:
```bash
./clean.sh
```

To remove the installation run:
```bash
# Warning: this will remove your current installation
rm -rf ./install
```
You may also want to remove the `torch-activate` entry from your shell start-up script (`~/.bashrc` or `~/.profile`).

## Test
You can test that all libraries are installed properly by running:
```bash
./test.sh
```

Tested on Ubuntu 14.04, CentOS/RHEL 6.3 and OSX
