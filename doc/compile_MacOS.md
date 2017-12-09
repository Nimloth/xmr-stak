# Compile **xmr-stak** for MacOS

## Dependencies

Assuming you already have [Homebrew](https://brew.sh) installed, the installation of dependencies is pretty straightforward and will generate the `xmr-stak` binary in the `bin/` directory.

### For NVIDIA GPUs

```shell
brew tap caskroom/drivers
brew cask install nvidia-cuda
brew install hwloc libmicrohttpd gcc openssl cmake
cmake . -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl -DOpenCL_ENABLE=OFF
make install
```

[All available CMake options](compile.md#nvidia-build-options)

### For AMD GPUs

> Note: Generally speaking, you have to use the OpenCL stuff Apple ships.
To do that, it is sufficient to install the command line developer tools:

```shell
xcode-select --install
```

A popup should ask if you want to download and install the command line developer tools which ou should confirm.
Please note that this will also install the clang/llvm compile, so there is no need to install gcc.

After having them installed, add necessary requirements and compile.
```shell
brew install hwloc libmicrohttpd openssl cmake
cmake . -DCUDA_ENABLE=OFF -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl
make install
```

> Note: It may be necessary to specify the version of openssl, it was on my system:

```shell
brew install hwloc libmicrohttpd openssl cmake
cmake . -DCUDA_ENABLE=OFF -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl\@1.1
make install
```

### For CPU-only mining

```shell
brew install hwloc libmicrohttpd gcc openssl cmake
cmake . -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl -DCUDA_ENABLE=OFF -DOpenCL_ENABLE=OFF
make install
```

[All available CMake options](compile.md#cpu-build-options)
