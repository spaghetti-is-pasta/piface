### About
Simple wrapper for the <a href="http://www.piface.org.uk/products/piface_digital/" target="_new">PiFace Digital</a> and NodeJS (v4+ or v5+)

### Installation
Note: recent Kernel versions need Device-Tree to be disabled in order to use SPI.

- Install NodeJS

Follow the instructions available here:
https://nodejs.org/en/download/package-manager/

(Optional) Update `npm` and `node-gyp`
```
npm install -g npm@latest
npm install -g node-gyp@latest
```

- Download, build and install the C libraries

```
sudo apt-get install automake libtool git
git clone https://github.com/thomasmacpherson/piface.git
cd piface/c
./autogen.sh && ./configure && make && sudo make install
sudo ldconfig
cd ../scripts
sudo ./spidev-setup
```

- Install the PiFace NodeJS module

```
npm install piface
```

- Usage

```javascript
var pfio = require("piface");

pfio.init();
var i = 0;
for (i = 0; i < 8; i++) {
    console.log("Pin #" + i + " = " + pfio.digital_read(i));
}

i = -1;
function anim() {
    i++;
    console.log("Pin #" + i + " on");
    pfio.digital_write(i, 1);
    if (i < 8) {
        setTimeout(function () {
            console.log("Pin #" + i + " off");
            pfio.digital_write(i, 0);
            if (i < 7) {
                anim();
            } else {
                pfio.deinit();
            }
        }, 250);
    }
}
anim();
```

- Methods

```javascript
pfio.init();
pfio.deinit();
var val = pfio.digital_read(pin); // returns 0 or 1
pfio.digital_write(pin, val);
var val = pfio.read_input(); // returns 0..255
var val = pfio.read_output(pin, val); // returns 0..255
pfio.write_output(val);
```
