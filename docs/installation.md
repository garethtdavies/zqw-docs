# Installing zec-qt-wallet
---

## Download and Install

zec-qt-wallet runs on Windows, macOS and Linux. Follow the instructions below for the platform of your choice. To compile from source see [this section](compile-from-source).

??? info "Windows instructions (click to expand)"

    Download and run the .msi installer and follow the prompts. Alternately, you can download the release binary, unzip it and double click on zec-qt-wallet to start.

??? info "macOS instructions (click to expand)"

    Double-click on the .dmg file to open it, and drag zec-qt-wallet on to the Applications link to install. You will need to give authorization for the program to run.

??? info "Linux instructions (click to expand)"

    If you are on Debian/Ubuntu, please download the `.deb` package and install it.
    ```
    sudo dpkg -i linux-deb-zec-qt-wallet-v0.5.9.deb
    sudo apt install -f
    ```

    Or you can download and run the binaries directly.
    ```
    tar -xvf zec-qt-wallet-v0.5.9.tar.gz
    ./zec-qt-wallet-v0.5.9/zec-qt-wallet
    ``` 

## zcashd
zec-qt-wallet needs a Zcash node running zcashd. If you already have a zcashd node running, zec-qt-wallet will connect to it. 

If you don't have one, zec-qt-wallet will start its embedded zcashd node. 

Additionally, if this is the first time you're running zec-qt-wallet or a zcashd daemon, zec-qt-wallet will download the zcash params (~1.7 GB) and configure `zcash.conf` for you. 

Pass `--no-embedded` to disable the embedded zcashd and force zec-qt-wallet to connect to an external node.

### System requirements

## Compiling from source
zec-qt-wallet is written in C++ 14, and can be compiled with g++/clang++/visual c++. It also depends on Qt5, which you can get from [here](https://www.qt.io/download). Note that if you are compiling from source, you won't get the embedded zcashd by default. You can either run an external zcashd, or compile zcashd as well. 

See the instructions for [setting up a build environment](/setting-up-build-env) and detailed build instructions for each platform [here](/compile-from-source).

## Upgrading