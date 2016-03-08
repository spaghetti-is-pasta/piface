### About
Simple standalone NodeJS (v4+ or v5+) module for the Raspberry PiFace

### Installation
Note: recent Kernel versions need Device-Tree to be disabled in order to use SPI.

- Install NodeJS

Follow the instructions available here:
https://nodejs.org/en/download/package-manager/

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
    console.log("Pin #" + i + " = " + pfio.digital_read(0));
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
