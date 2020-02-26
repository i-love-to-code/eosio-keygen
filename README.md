
![](https://github.com/eosswedenorg/eosio-keygen/workflows/CI/badge.svg)
[![GitHub release](https://img.shields.io/github/v/release/eosswedenorg/eosio-keygen?include_prereleases)](https://github.com/eosswedenorg/eosio-keygen/releases/latest)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# EOSIO Keygen

This program generates public and private keypair for [EOS](https://eos.io/)

## Compile

You will need `openssl` development files (version 1.1 or later) to compile and `cmake` to compile this project.

### Linux/MacOS

#### Dependencies

**Ubuntu:**
```sh
$ apt-get install gcc g++ cmake libssl-dev
```
**For other linux distributions:**

Consult the manual for how to get these installed.

**MacOS:**

You must have a compiler installed. This project is known to build with `Xcode 11.0` but other versions should work.

You need to have opessl and cmake installed also, this can be done with this `brew` command:
```sh
$ brew install openssl cmake
```

#### Build

Run `./build.sh` to trigger cmake.

If you dont want to use the script. you can build with cmake using the following commands:

```sh
$ mkdir build && cd build
$ cmake .. && make
```

**MacOS:** You may need to point `cmake` to `openssl` by passing the argument
`-D OPENSSL_ROOT_DIR=/usr/local/opt/openssl@1.1` if openssl is not under `/usr/local/opt/openssl@1.1` you need to find the correct path.

### Windows

#### Dependencies

Download and install `cmake` from [cmake.org](https://cmake.org) and download
[openssl](https://mirror.firedaemon.com/OpenSSL/openssl-1.1.1e-dev.zip)

unpack `openssl-1.1.1e-dev.zip` somewhere on the filesystem.

You will also need a compiler. [Build Tools for Visual Studio 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16) (Selecting C++ during installation) is recommended.

#### Build.

you need to set `OPENSSL_ROOT_DIR` to the directory where you unpacked
`openssl-1.1.1e-dev.zip` append `x86` if you are on 32-bit system, `x64` for 64-bit.

**NOTE:** `cmake` uses forward slash `/` for path even for windows. so make sure you use that when setting `OPENSSL_ROOT_DIR`

For example:

```
C:\repo> mkdir build
C:\repo> cd build
C:\repo\build> cmake -D OPENSSL_ROOT_DIR="C:/path/to/openssl-1.1/x86" ..
C:\repo\build> cmake --build . --config Release
```

## Compile options

These compile options are available:

| Cmake                      | build.sh          | Description                               |
|--------------------------- | ----------------- | ------------------------------------------|
| -DCMAKE_BUILD_TYPE=`value` | -t `value`        | Type of build 							 |
| -DUSE_THREADS=`OFF`        | --disable-threads | Disable thread support                    |
| -DFORCE_ANSI=`ON`          | --force-ansi      | Force ANSI console colors even on windows |

For more details about options run `./build.sh -l` or `mkdir build && cmake build -LA`

## Install

After the project has been compiled. run `sudo ./install.sh` or the following code if you dont want to use that:

```sh
# inside the build directory
$ sudo make install
```

**Windows:**

It is possible to run `cmake --install .` from `build` directory.
Your DOS shell needs administrator privileges.

## Uninstall

Run `sudo ./uninstall.sh` or remove the files listed in `build/install_manifest.txt` manually.

## Security notice

Keys are generated by `OpenSSL`'s `EC_KEY_generate_key` function. The program will
never expose your keys to anything but the computers memory and output of the
program. You are free to inspect the source code and compile yourself to verify.

However, use this at your own risk. we cannot guarantee that the keys are
cryptographically secure as this depends on OpenSSL's implementation (alto it is
widely used and should be safe)

Please read the `LICENSE` file.

```
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF
CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE
OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

## Author

Henrik Hautakoski - [henrik@eossweden.org](mailto:henrik@eossweden.org)
