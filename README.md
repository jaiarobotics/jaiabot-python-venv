# Jaiabot Python venv

This repository contains the contents of a [virtual environment](https://docs.python.org/3/library/venv.html) (venv) with the dependencies for the Python code in [Jaiabot](https://github.com/jaiarobotics/jaiabot/).

Use of this virtual environment is optional, you can always install the required Python dependencies directly onto your system using:

```
pip3 install smbus adafruit-circuitpython-busdevice adafruit-circuitpython-register
```

## Creation
This repository was created using:

```
mkdir jaiabot-python-venv
cd jaiabot-python-venv
# generate the venv
python3 -m venv .
# activate it
source bin/activate
# install dependencies
pip3 install smbus adafruit-circuitpython-busdevice adafruit-circuitpython-register
```

### Remove hardcoded paths

Patch activate script:

```
--- a/bin/activate
+++ b/bin/activate
@@ -36,8 +36,7 @@ deactivate () {
 
 # unset irrelevant variables
 deactivate nondestructive
-
-VIRTUAL_ENV="/home/toby/opensource/jaiabot-python-venv"
+VIRTUAL_ENV=$(realpath "$(dirname "$0")/..")
 export VIRTUAL_ENV
 
 _OLD_VIRTUAL_PATH="$PATH"
```

```
# Remove hardcoded python3 (assumes activate used)
for i in `grep -lr jaiabot-python-venv *`; do sed -i 's|#!.*jaiabot-python-venv/bin/python3|#!python3|' $i; done
```

## Use
To use it, simply activate:

```
source jaiabot-python-venv/bin/activate
# then you can run any of the Jaiabot python scripts, e.g.,
jaiabot/build/amd64/bin/jaia_py/adafruit_BNO055/jaiabot_imu.py
```

## Updating

To update, simply activate and re-run the install for one or all of the packages:

```
source jaiabot-python-venv/bin/activate
pip3 install smbus adafruit-circuitpython-busdevice adafruit-circuitpython-register
```