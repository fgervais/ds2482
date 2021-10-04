# 

## Credits

The DS2482 driver is originally from https://github.com/chasmack/seedling.

## Usage Example

```bash
cd project
git submodule add https://github.com/fgervais/ds2482.git
```

```python
import adafruit_ds18x20
import busio

from ds2482.ds2482 import DS2482
from ds2482.onewire import OneWireBus


i2c = busio.I2C(frequency=400000)
ds2482 = DS2482(i2c)
ow_bus = OneWireBus(ds2482)

# This `ow_bus` instance can be used as a normal `adafruit_onewire.bus.OneWireBus`.
# For example, to access a temperature sensor.
#
# https://learn.adafruit.com/using-ds18b20-temperature-sensor-with-circuitpython/circuitpython#usage-2979782-2

devices = ow_bus.scan()
for device in devices:
    print("ROM = {} \tFamily = 0x{:02x}".format([hex(i) for i in device.rom], device.family_code))
ds18b20 = adafruit_ds18x20.DS18X20(ow_bus, devices[0])

print('Temperature: {0:0.3f} °C'.format(ds18b20.temperature))
```
