### About
Simple wrapper for the PiFace module and latest versions of NodeJS, on top of the C libraries

### Installation
Note: recent Kernel versions need Device-Tree to be disabled in order to use SPI.

1. Install NodeJS

Follow the instructions available here:
https://nodejs.org/en/download/package-manager/

2. Download, build and install the C libraries

```
sudo apt-get install automake libtool git
git clone https://github.com/thomasmacpherson/piface.git
cd piface/c
./autogen.sh && ./configure && make && sudo make install
sudo ldconfig
cd ../scripts
sudo ./spidev-setup
```

3. Install the PiFace NodeJS module

```
npm install piface
```
