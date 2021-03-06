# BUILDING ON OSX
### Tested on macOS 10.12-10.15

BitBlocks is based on outdated fork so we should use some old libraries to build it.

## 0: Preparing
- Install [HomeBrew](https://brew.sh/) via Terminal `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
- Install XCode 11 or older
- Get miniupnpc v1.9 ([From GitHub](https://github.com/miniupnp/miniupnp/archive/refs/tags/miniupnpc_1_9.zip)) or older
- Get Boost v1.57 ([From SourceForge](https://sourceforge.net/projects/boost/files/boost/1.57.0/boost_1_57_0.zip/download)) or older
- Get OpenSSL v1.0 ([1.0.1e From GitHub](https://github.com/openssl/openssl/archive/refs/tags/OpenSSL_1_0_1e.zip)), NOT 1.1!!!

## 1: HomeBrew Packages
`brew install berkeley-db@4 qt@5 automake libtool pkg-config libevent openssl git`

## 2: Building libs from sources

**OpenSSL**
```
unzip OpenSSL_1_0_1e.zip
cd openssl-OpenSSL_1_0_1e
./Configure darwin64-x86_64-cc --prefix="/usr/local/opt/openssl\@1.0" --openssldir="/usr/local/opt/openssl\@1.0"
make
make install_sw
brew unlink openssl
```

**Boost**

```
unzip boost_1_57_0.zip
cd boost_1_57_0
./bootstrap.sh
./b2
./b2 install
```

**MiniUPnPc**
```
unzip miniupnpc_1_9.zip
cd miniupnp-miniupnpc_1_9/miniupnpc
INSTALLPREFIX=/usr/local make install
```

## 3: Build BitBlocks Wallet
```
git clone https://github.com/cradio/bitblocks
cd bitblocks/src
make
cd ..
qmake
make
```
It will build static binary by default

Should work... If not -> open issues

## Some issues that may occur
**1: Boost**
```
-n Building Boost.Build engine with toolset darwin... 

Failed to build Boost.Build build engine
Consult 'bootstrap.log' for more details
```
If the last line of ***bootstrap.log*** is like `error: implicit declaration of function '----' is invalid in C99` then probably the problem is that you haven't installed XCode.

If XCode is installed then you should open it and accept EULA, after that do `sudo xcode-select -s /Applications/Xcode.app`

**2: **
